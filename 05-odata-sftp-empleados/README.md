# Extracción de Empleados desde un OData v2 Real de SAP y Entrega por SFTP

iFlow programado que consume el sandbox público de SAP Business Accelerator Hub (SuccessFactors, entidad `User`), convierte la respuesta OData v2 a un archivo de ancho fijo con registros de control y lo entrega por SFTP.

## Arquitectura

```
[Timer] dispara el job
      ↓
[Content Modifier] headers (APIKey externalizada)
      ↓
[Request-Reply] GET OData v2 /User — sandbox.api.sap.com
      ↓
[Groovy] arma el archivo de ancho fijo (Header + Detail + Trailer)
      ↓
[SFTP Receiver] entrega el archivo
```

## Qué demuestra

- Consumo de un OData v2 real de SAP con `$top`, `$select`, `$format` y el sobre `d.results`
- Credenciales fuera del diseño: la API Key es un parámetro externalizado con valor por defecto vacío, así no queda dentro del export que se sube a GitHub
- Detalles de datos reales en Groovy: fechas `/Date(ms)/` de OData v2, campos nulos, truncado a ancho fijo, limpieza de tildes
- Archivo de ancho fijo con Header/Detail/Trailer y conteo de registros como control
- Timer Start Event y SFTP con nombre dinámico y reintentos del adapter

## Limitaciones

- El sandbox se autentica con API Key, no con OAuth2. La configuración de OAuth2 Client Credentials está en [`03-oauth2-sftp-payroll`](../03-oauth2-sftp-payroll), contra un servidor simulado.
- La entidad `User` no trae salarios: es un archivo de empleados, no de nómina.
- Son datos de prueba del sandbox; el contenido y la disponibilidad del sandbox los define SAP.

## Estado

Probado end-to-end contra el sandbox público y un servidor SFTP de prueba.

## Carpetas

- `iflow/`: export del iFlow (.zip de Integration Suite). Antes de exportar, confirmá que el parámetro `SAP_API_KEY` tenga valor por defecto vacío.
- `screenshots/`: capturas del Monitor y de las pruebas

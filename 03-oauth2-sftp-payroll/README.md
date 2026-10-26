# Extracción de Nómina con OAuth2 (simulado) y Entrega por SFTP

iFlow programado que extrae datos de nómina desde un servicio OData **simulado**, autenticado con OAuth2 Client Credentials, los transforma a un archivo de ancho fijo con registros de control, y lo entrega por SFTP.

> **Nota:** el servicio OData y el endpoint de token son mocks (Beeceptor), usados para practicar la configuración del Security Material OAuth2 Client Credentials. Los datos no son reales. La versión que consume un OData real de SAP está en [`05-odata-sftp-empleados`](../05-odata-sftp-empleados).

## Arquitectura

```
[Timer] dispara el job
      ↓
[Request-Reply] GET OData (mock) — auth OAuth2 Client Credentials
      ↓
[Groovy] arma el archivo de ancho fijo (Header + Detail + Trailer)
      ↓
[SFTP Receiver] entrega el archivo
```

## Qué demuestra

- Configuración de Security Material OAuth2 Client Credentials (token endpoint simulado)
- Timer Start Event: integración batch programada, no request-response
- Groovy: padding/truncado exacto por posición, formato numérico con decimales implícitos, limpieza de acentos para compatibilidad con sistemas legacy (`Normalizer`)
- Patrón Header/Detail/Trailer con totales de control (cantidad de registros y suma de salarios), clásico de interfaces batch (archivos bancarios, nómina, EDI)
- SFTP con nombre de archivo dinámico (timestamp) y reintentos configurados a nivel de adapter

## Estado

Probado end-to-end contra mocks y un servidor SFTP de prueba.

## Carpetas

- `iflow/`: export del iFlow (.zip de Integration Suite)
- `screenshots/`: capturas del Monitor y de las pruebas

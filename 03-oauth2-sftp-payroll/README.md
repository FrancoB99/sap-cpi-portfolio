# Extracción de Nómina con OAuth2 y Entrega por SFTP

iFlow programado que extrae datos de nómina desde un sistema tipo SuccessFactors (OData + OAuth2 Client Credentials), los transforma a un archivo de ancho fijo con registros de control, y lo entrega por SFTP.

## Arquitectura

```
[Timer] dispara el job
      ↓
[Request-Reply] GET OData — auth OAuth2 Client Credentials
      ↓
[Groovy] arma el archivo de ancho fijo (Header + Detail + Trailer)
      ↓
[SFTP Receiver] entrega el archivo
```

## Qué demuestra

- Security Material OAuth2 Client Credentials (uno de los temas de seguridad más preguntados en entrevistas CPI)
- Timer Start Event — integración batch programada, no request-response
- Groovy: padding/truncado exacto por posición, formato numérico con decimales implícitos, limpieza de acentos para compatibilidad con sistemas legacy (`Normalizer`)
- Patrón Header/Detail/Trailer con totales de control, clásico de interfaces batch (archivos bancarios, nómina, EDI)
- SFTP con nombre de archivo dinámico (timestamp) y reintentos configurados a nivel de adapter

## Carpetas

- `iflow/` — export del iFlow (.zip de Integration Suite)
- `screenshots/` — capturas del Monitor y de las pruebas

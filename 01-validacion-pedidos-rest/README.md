# Validación y Transformación de Pedidos REST/JSON

iFlow que recibe un pedido de venta vía REST/JSON, lo valida y enriquece, y lo transforma a nomenclatura de campos SAP antes de enviarlo a un sistema backend.

## Arquitectura

```
[Cliente] → HTTPS POST /onprem/orders
      ↓
[Content Modifier] guarda el payload original
      ↓
[Groovy] 1_ValidateAndEnrich — valida campos obligatorios, calcula totales, genera correlationId
      ↓
[Groovy] 2_MapToSapFields — mapea a nomenclatura SAP (Kunnr, Matnr, Menge, Netpr...)
      ↓
[Request-Reply] → Backend
      ↓
[Groovy] 3_ProcessResponse — arma la respuesta final
      ↓
[Cliente] ← respuesta JSON
```

Con Exception Subprocess dedicado para capturar errores de validación y devolver un JSON de error consistente con el código HTTP correspondiente.

## Qué demuestra

- Groovy: `JsonSlurper`/`JsonBuilder` para parseo y construcción de JSON a mano, sin depender del mapping gráfico
- Diferencia entre Properties (uso interno del iFlow) y Headers (viajan al protocolo)
- Trazabilidad con `correlationId` (UUID) propagado entre pasos y expuesto en el Message Processing Log
- Manejo de excepciones custom (`IllegalArgumentException`) capturadas por un Exception Subprocess
- Mapeo de campos de negocio a nomenclatura SAP (`Kunnr`, `Matnr`, `Menge`, `Netpr`, `Netwr`, `Vbeln`)

## Estado

Probado end-to-end contra un backend de pruebas.

## Carpetas

- `iflow/` — export del iFlow (.zip de Integration Suite)
- `screenshots/` — capturas del Monitor y de las pruebas

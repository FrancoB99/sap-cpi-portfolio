# Gateway de Validación Multi-País — Router, Local Integration Process, Externalized Parameters

iFlow que valida identificaciones fiscales de clientes (CUIT/CNPJ/RFC) ruteando dinámicamente según el país, con lógica común reutilizable y configuración externalizada por ambiente.

## Arquitectura

```
[Cliente] → POST /validate-customer
      ↓
[Local Integration Process] Validate-Common — validación estructural reutilizable
      ↓
[Router] según countryCode → AR / BR / MX / Default
      ↓ (las ramas convergen — el Router es exclusivo, no paralelo)
[Groovy] 1_ValidateFormat — aplica la regla de formato según el país (mapa, no scripts duplicados)
      ↓
[Cliente] ← resultado
```

## Qué demuestra

- Router vs Multicast: cuándo usar ruteo excluyente vs. fan-out paralelo
- Local Integration Process para encapsular la validación común dentro del iFlow (para compartir lógica entre iFlows distintos se usaría ProcessDirect o Script Collections)
- Externalized Parameters para transporte Dev/QA/Prod sin tocar el diseño
- Diseño DRY: las 3 ramas del Router convergen a un único script de validación en vez de triplicar lógica

## Estado

Router, Local Integration Process y Externalized Parameters probados. API Management documentado a nivel conceptual, pendiente de implementación práctica.

## Carpetas

- `iflow/` — export del iFlow (.zip de Integration Suite)
- `screenshots/` — capturas del Monitor y de las pruebas

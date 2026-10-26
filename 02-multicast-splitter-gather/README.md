# Fan-Out de Pedidos (Order-to-Cash) — Splitter, Multicast, Gather

iFlow que recibe un batch de pedidos, los procesa en paralelo contra múltiples sistemas (control de stock, chequeo de crédito y notificación), y devuelve un reporte consolidado.

## Arquitectura

```
[Cliente] → POST /batch/orders { orders: [...] }
      ↓
[Splitter] (XPath, sobre XML convertido desde JSON) — un mensaje por pedido
      ↓
[Request-Reply] ntfy.sh — notificación real en tiempo real
      ↓
[Multicast] → WMS (stock) + Finanzas (crédito) en paralelo
      ↓
[Join] → [Gather] correlacionado por orderId — combina las 2 ramas en un XML
      ↓
[Groovy] decide CONFIRMED / ON_HOLD
      ↓ (vuelve al loop del Splitter)
[Gather] externo — junta todos los pedidos procesados
      ↓
[Groovy] arma el reporte final
      ↓
[Cliente] ← reporte consolidado
```

## Qué demuestra

- Patrones EIP: Splitter, Multicast, Join, Gather (en dos niveles: por rama del Multicast y por pedido del Splitter)
- Conversión JSON a XML dentro del iFlow para poder usar el Splitter nativo (el General Splitter solo soporta XPath), manteniendo JSON hacia afuera
- Groovy: `JsonSlurper`, `XmlSlurper`, `StreamingMarkupBuilder`
- Integración con un servicio externo real (ntfy.sh) y con mocks no-code (Beeceptor) para simular sistemas internos (WMS, Finanzas)
- Manejo de fallos parciales: un pedido con crédito bloqueado no tira abajo el batch completo
- Entendimiento de una limitación real de CPI: el Gather solo acepta una línea de entrada, por lo que el Join es obligatorio antes cuando cierra un Multicast con más de una rama

## Carpetas

- `iflow/` — export del iFlow (.zip de Integration Suite)
- `screenshots/` — capturas del Monitor y de las pruebas

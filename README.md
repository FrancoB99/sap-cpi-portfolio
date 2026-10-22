# SAP CPI Portfolio — Franco Blanco

Portfolio de integraciones construidas en SAP Integration Suite (Cloud Integration) como parte de mi transición desde SAP PI/PO. Cada carpeta contiene un iFlow end-to-end con foco en patrones de integración empresarial (EIP) y lógica Groovy.

## Proyectos

| # | Proyecto | Patrones / Skills |
|---|---|---|
| [01](./01-validacion-pedidos-rest) | Validación y transformación de pedidos REST/JSON | Content Modifier, Groovy (JsonSlurper/JsonBuilder), mapeo a nomenclatura SAP, Exception Subprocess |
| [02](./02-multicast-splitter-gather) | Fan-out de pedidos (Order-to-Cash) | Splitter, Multicast, Join, Gather, Groovy (XmlSlurper, StreamingMarkupBuilder), integración con servicios externos reales |
| [03](./03-oauth2-sftp-payroll) | Extracción de nómina con OAuth2 y entrega SFTP | OAuth2 Client Credentials, Security Material, Timer, archivo de ancho fijo con registros de control |
| [04](./04-router-api-management) | Gateway de validación multi-país | Router, Local Integration Process, Externalized Parameters, API Management |

## Stack

SAP Integration Suite (Cloud Integration) · Groovy · REST/JSON · XML · OAuth 2.0 · SFTP

## Sobre este portfolio

Vengo de un perfil SAP PI/PO y arranqué este portfolio para documentar mi transición práctica a SAP Integration Suite (CPI). Cada proyecto incluye su propio README con la arquitectura, qué patrones demuestra y en qué estado está (probado vs. documentado a nivel conceptual).

## Contacto

LinkedIn: [franco-blanco7a03a4217](https://linkedin.com/in/franco-blanco7a03a4217)

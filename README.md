# SAP CPI Portfolio — Franco Blanco

Portfolio de integraciones construidas en SAP Integration Suite (Cloud Integration) como parte de mi transición desde SAP PI/PO. Cada carpeta contiene un iFlow end-to-end con foco en patrones de integración empresarial (EIP) y lógica Groovy.

## Proyectos

| # | Proyecto | Patrones / Skills |
|---|---|---|
| [01](./01-validacion-pedidos-rest) | Validación y transformación de pedidos REST/JSON | Content Modifier, Groovy (JsonSlurper/JsonBuilder), mapeo a nomenclatura SAP, Exception Subprocess |
| [02](./02-multicast-splitter-gather) | Fan-out de pedidos (Order-to-Cash) | Splitter, Multicast, Join, Gather, conversión JSON/XML, Groovy (XmlSlurper, StreamingMarkupBuilder), servicio externo real (ntfy.sh) |
| [03](./03-oauth2-sftp-payroll) | Extracción batch con OAuth2 (simulado) y entrega SFTP | Security Material OAuth2 Client Credentials contra un servidor simulado, Timer, archivo de ancho fijo con registros de control |
| [04](./04-router-api-management) | Gateway de validación multi-país | Router, Local Integration Process, Externalized Parameters |
| [05](./05-odata-sftp-empleados) | Extracción de empleados desde un OData v2 real de SAP | OData v2 (SuccessFactors sandbox), API Key externalizada, fechas `/Date(ms)/`, archivo de ancho fijo, SFTP |

## Stack

SAP Integration Suite (Cloud Integration) · Groovy · REST/JSON · OData v2 · XML · OAuth 2.0 · SFTP

## Sobre este portfolio

Vengo de un perfil SAP PI/PO y armé este portfolio para documentar mi transición práctica a SAP Integration Suite (CPI). Cada proyecto incluye su propio README con la arquitectura, qué patrones demuestra y en qué estado está (probado vs. simulado). Donde un sistema es simulado (mocks) o hay una limitación, está indicado en el README del proyecto.

## Contacto

LinkedIn: [franco-blanco7a03a4217](https://linkedin.com/in/franco-blanco7a03a4217)

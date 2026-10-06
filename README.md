# Té Negro Estudio — pedidos directos

App de una sola página para tomar pedidos por WhatsApp **sin comisión de marketplace**.

## Qué es

Un archivo HTML autocontenido. Sin build, sin servidor, sin dependencias externas.

- Catálogo con personalización: tamaño, hielo, azúcar, tipo de leche, toppings
- Carrito que persiste en `localStorage`
- Zonas de envío con costo y tiempo, envío gratis desde un umbral
- Checkout que entrega el pedido ya desglosado por `wa.me`
- Código de recompra automático
- Panel de negocio: ventas del día, ticket promedio, comisión evitada y comparativa de
  costo por método de cobro

## Estado actual

**Modo prueba encendido.** El botón no manda nada: muestra en pantalla el mensaje que se
enviaría. Falta cargar el WhatsApp y la CLABE reales en el bloque `CONFIG`.

## Configuración

Todo vive en el bloque `CONFIG`, al inicio del `<script>`:

| Campo | Qué es |
|---|---|
| `modoPrueba` | `true` no envía nada. `false` abre WhatsApp de verdad. |
| `negocio.whatsapp` | `52` + 10 dígitos, sin espacios ni signos |
| `pagos.clabe` | Tu CLABE, **18 dígitos exactos** |
| `pagos.banco`, `pagos.titular` | Se muestran al elegir transferencia |
| `envio.zonas` | Colonias, costo y tiempo de entrega |
| `MENU` | Productos y precios base (vaso de 16 oz) |

## Reglas que no se deben romper

- **Nunca cobrar recargo por pagar con tarjeta.** Es ilegal en México (art. 7 Bis de la Ley
  Federal de Protección al Consumidor). El parámetro es un **descuento** por efectivo o
  transferencia, y así se queda.
- Con ticket chico, **Clip** (3.6% + IVA, sin cargo fijo) sale más barato que un link de pago
  que cobra un fijo por transacción.
- Sin `negocio.whatsapp` cargado, la app **bloquea el envío** en vez de abrir WhatsApp.

## Publicar

Es estático: cualquier hosting sirve. GitHub Pages, Netlify Drop o Vercel.

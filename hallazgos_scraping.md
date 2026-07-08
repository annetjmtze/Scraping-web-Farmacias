# Hallazgos de scraping - Día 2

## Farmacias del Ahorro
- **URL**: https://www.fahorro.com/paracetamol-500-mg-oral-20-tabletas.html
- **Precio en HTML estático**: Sí
- **Selector**: `[data-price-type="oldPrice"] .price`
- **Precio**: $31.00

## Farmacias Guadalajara - Problema de scraping

- **URL**: https://www.farmaciasguadalajara.com/medicina/analgesicos/paracetamol-650-mg--24-tabletas-pharmalife.-1028081.html
- **Problema**: Timeout en todas las peticiones con `requests` (incluso con User-Agent realista y timeout de 30s).
- **Posible causa**: Protección anti-bot (Cloudflare), bloqueo de IP o necesidad de JavaScript.
- **Tiempo invertido**: >30 min.
- **Decisión**: Se documenta y se pasa a la siguiente tarea, ya que se tienen precios de Farmacias del Ahorro y Benavides.

## Farmacias Benavides
- **URL del producto**: https://www.benavides.com.mx/paracetamol-500-mg-20-tabletas (o la que uses)
- **¿Precio en HTML estático?**: No visible en el DOM, pero sí dentro de un script con datos de GA4 (JSON).
- **Método de extracción**: Se parsea el objeto `dl4Objects` para obtener el precio del producto principal.
- **Selector / ubicación**: `<script>` que contiene `dl4Objects` → `ecommerce.items[0].price`.
- **Observaciones**: El precio se extrae exitosamente desde el script. No se encontró información de promociones.
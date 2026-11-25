# moby.lat

Landing de moby: publicamos las propiedades de agentes inmobiliarios en grupos de Facebook, sin pagar anuncios.

Sitio estático. Todo va en la raíz del dominio `https://moby.lat/`:

- `index.html`: la página.
- `img/`: imágenes (WebP), favicon e íconos.
- `og.jpg`: imagen para compartir en redes (1200×630).
- `robots.txt`: permite buscadores y motores de IA.
- `sitemap.xml` y `llms.txt`.

## Configuración

Al final de `index.html`, el objeto `CONFIG` tiene el número de WhatsApp (`whatsapp`) y un `formEndpoint` opcional para el formulario de demo. Sin endpoint, el formulario arma un mensaje de WhatsApp.

La página lee `utm_source`, `utm_medium`, `utm_campaign`, `utm_content`, `utm_term` y `ref` para saber de dónde llega cada visita (por ejemplo, desde las landings de un cliente).

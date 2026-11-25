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

Si configuras `formEndpoint`, agrega su dominio a `connect-src` en la política de seguridad (`Content-Security-Policy`) de `customHttp.yml`; si no, el navegador bloquea el envío.

La página lee `utm_source`, `utm_medium`, `utm_campaign`, `utm_content`, `utm_term` y `ref` para saber de dónde llega cada visita (por ejemplo, desde las landings de un cliente).

## Publicar con AWS Amplify Hosting

- `amplify.yml`: no hay build; copia los archivos públicos a `dist/` y Amplify sirve esa carpeta. Así `README.md` y los archivos de configuración no quedan publicados.
- `customHttp.yml`: encabezados de seguridad, caché y tipos de archivo (`llms.txt` y `robots.txt` como texto, `sitemap.xml` como XML, imágenes WebP).

Pasos en la consola de Amplify:

1. En AWS Amplify, **Create new app** → **GitHub** → autoriza a Amplify y elige el repo `1nueve/moby`, rama `main`.
2. En la configuración del build, Amplify detecta `amplify.yml`. Déjalo así y crea la app. Cada push a `main` publica una versión nueva.
3. Revisa la URL de prueba que da Amplify (`https://main.xxxx.amplifyapp.com`).
4. En **Hosting → Custom domains** → **Add domain**, escribe `moby.lat`.
   - Si el dominio está en Route 53, Amplify crea los registros solo.
   - Si está en otro proveedor, Amplify te da un registro CNAME para validar el certificado y los registros para `moby.lat` y `www.moby.lat`. Agrégalos en tu proveedor de DNS.
5. Deja activada la redirección de `www.moby.lat` a `moby.lat`, para que la dirección principal coincida con la del SEO (`https://moby.lat/`).
6. Cuando el dominio aparezca como disponible, da de alta `https://moby.lat/` en Google Search Console y envía `https://moby.lat/sitemap.xml`.

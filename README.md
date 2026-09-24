# KSTmedia — sitio web

Sitio multi-página, código listo para VS Code, GitHub y Vercel. HTML, CSS y JS separados, sin frameworks ni dependencias ni build.

## Estructura

```
index.html                                    → Inicio (hero + vídeo + teasers)
servicios.html                                 → Ficha de Google, SEO técnico, Google Ads (#ficha-google, #seo-tecnico, #google-ads)
kstmedia.html                                  → Sobre Sergio, foto de busto
blog.html                                      → Listado de artículos
preguntas-frecuentes.html                      → 8 FAQ + schema FAQPage
contacto.html                                  → Calendario de reservas (Calendly) + auditoría gratuita
aviso-legal.html                               → Identificación del titular (LSSI)
privacidad.html                                → Política de privacidad (RGPD)
cookies.html                                   → Política de cookies
404.html                                       → Página de error (no indexable, la usan GitHub Pages/Vercel automáticamente)
blog/
  ficha-google-business-profile-checklist.html
  seo-local-o-google-ads.html
  por-que-google-prioriza-eeat.html
  cuanto-tarda-seo-local.html
styles.css                                     → identidad visual
script.js                                      → menú móvil + año dinámico
robots.txt / sitemap.xml                       → indexación
assets/                                        → logo, fotos, favicon, imágenes de servicio
```

Cada página comparte la misma cabecera (con el botón de Contacto siempre visible), el botón flotante de WhatsApp, y un banner de llamada a la acción antes del pie, para que la conversión esté presente en todas las páginas, no solo en Contacto.

Al no usar un generador de sitios, el header y el footer están repetidos en cada archivo HTML. Es la forma estándar de hacerlo en un sitio estático sin build. Si el sitio crece mucho más (más de ~15 páginas), valora migrar a un generador estático (Astro, Eleventy) que sí permite plantillas compartidas — no es necesario hoy.

## Antes de publicar — checklist

- [x] **Logo**: `assets/logo.svg`.
- [x] **Foto de Sergio**: `assets/foto-sergio.jpg`, formato busto (retrato de pecho para arriba). Se usa en `kstmedia.html` y en la firma de autor de cada artículo del blog. Comprimida a ~113 KB sin pérdida visible de calidad.
- [x] **Vídeo del hero**: alojado en Wistia (`sromeromjob.wistia.com/s/q2k7fukxv2ezv27`) e incrustado en `index.html` mediante `<iframe>`. Ya no se sirve un `.mp4` local — evita que un archivo de vídeo de gran tamaño viaje dentro del repositorio de GitHub. Ver sección siguiente.
- [x] **WhatsApp**: ya configurado con tu número real (+34 711 565 112) en el botón flotante de todas las páginas y en `contacto.html`.
- [x] **Calendario de reservas**: ya conectado a tu Calendly real (`calendly.com/medkst/llamada-auditoria-gratuita`) en `contacto.html` y en todos los botones "Reserva tu auditoría gratuita" del sitio. Ver sección siguiente.
- [x] **Dominio real**: ya configurado con `https://www.medkst.com` en `canonical`, Open Graph, JSON-LD, `robots.txt` y `sitemap.xml`.
- [x] **Favicon**: `assets/favicon.svg` y `assets/apple-touch-icon.png` (180×180 px) ya están puestos.
- [x] **Imagen Open Graph**: `assets/og-image.jpg` (1200×630 px) ya está puesta.
- [x] **Página de error**: `404.html` creada, con `noindex` y accesos directos a Inicio/Servicios/WhatsApp.
- [ ] **Tipografía Ford Antenna**: no está en Google Fonts (uso restringido de Ford Motor Company). Si tienes los archivos con licencia, cópialos a `assets/fonts/` y descomenta el `@font-face` al inicio de `styles.css`.
- [x] **Páginas legales**: `aviso-legal.html`, `privacidad.html` y `cookies.html` ya creadas con tus datos reales (Sergio Romero Martín, NIF 47657397V). Revísalas tú o con un asesor antes de publicar — son una base sólida pero no sustituyen la revisión de un profesional si tu actividad crece o cambia.
- [ ] **Herramientas de medición**: cuando actives Google Analytics, Meta Pixel o el seguimiento de conversiones de Google Ads, añade antes un banner de consentimiento de cookies (obligatorio por ley) y actualiza `cookies.html` con el detalle de cada cookie. Avísame cuando llegue ese momento y te lo preparo.

## Vídeo del hero (Wistia)

`index.html` incrusta tu vídeo mediante un `<iframe>` que apunta a `fast.wistia.net/embed/iframe/q2k7fukxv2ezv27`. Ya no hay ningún `.mp4` dentro de `assets/` — si en algún momento cambias de vídeo en Wistia, o lo mueves a otro proveedor, solo hay que actualizar esa URL en `index.html` (busca `wistia`).

## Reserva de la auditoría gratuita (Calendly)

`contacto.html` tiene incrustado tu calendario real de **Calendly** (`calendly.com/medkst/llamada-auditoria-gratuita`) mediante su widget oficial (`assets.calendly.com/assets/external/widget.js`), así que cada visita puede reservar directamente un hueco en tu agenda sin pasar por un formulario ni por tu email.

Los botones "Reserva/Reservar tu auditoría gratuita" del resto del sitio (inicio, servicios, KSTmedia, blog, preguntas frecuentes) enlazan a la página `contacto.html`, donde está el calendario incrustado — así el usuario ve antes el contexto (qué incluye la llamada, opción de WhatsApp) antes de reservar. Solo `contacto.html` abre el widget de Calendly directamente.

Cosas a tener en cuenta:

1. Si cambias el nombre de tu evento en Calendly, la URL cambiará — avísame para actualizarla (está solo en `contacto.html`).
2. En el panel de Calendly puedes configurar recordatorios automáticos por email/SMS, límites de reservas por día y la zona horaria que se muestra a cada visitante.
3. Calendly puede instalar sus propias cookies técnicas al cargar el calendario; esto ya está reflejado en `cookies.html` y `privacidad.html`.

## Desarrollo local

Sin build. Abre `index.html` con **Live Server** en VS Code, o:

```bash
npx serve .
```

## Despliegue en Vercel

1. Sube esta carpeta a un repositorio de GitHub.
2. En [vercel.com](https://vercel.com), "Add New Project" → importa el repositorio.
3. Framework Preset: **Other** (HTML estático, sin build command ni output directory).
4. Deploy. Vercel sirve `index.html` y el resto de páginas directamente por su nombre de archivo.
5. Conecta tu dominio real en Vercel → Settings → Domains, y actualiza las URLs del checklist de arriba.

## Notas de SEO técnico

- Un único `<h1>` por página, con la keyword principal de esa página.
- Jerarquía `h1 → h2 → h3` sin saltos en todas las páginas, incluidos los artículos del blog.
- `title` y `meta description` únicos por página, dentro de los límites recomendados.
- Cada artículo del blog es una página real e indexable (no un ancla), con su propio `BlogPosting` + `BreadcrumbList` en JSON-LD, fecha, autor con enlace a `kstmedia.html`, y un CTA final a la página de servicio relacionada — así el tráfico informativo (blog) puede convertir en tráfico transaccional (servicios).
- `preguntas-frecuentes.html` incluye `FAQPage` en JSON-LD con las 8 preguntas, para citación por IA (GEO).
- `kstmedia.html` incluye `Person` en JSON-LD (autoridad del autor).
- Vídeo del hero servido desde Wistia (`loading="lazy"` en el `iframe`), fuera del repositorio para no pesar el proyecto.
- `prefers-reduced-motion` respetado; menú móvil accesible por teclado.
- Tablas largas (`privacidad.html`, `cookies.html`, `aviso-legal.html` y artículos del blog) van envueltas en `.table-scroll` para que se puedan desplazar horizontalmente en móvil sin romper el ancho de la página.
- `vercel.json` redirige `/index.html` a `/` (301) para evitar contenido duplicado entre ambas URLs — la home solo existe en `/`, que es la que declara la etiqueta canonical.
- `llms.txt` en la raíz del sitio: resumen del negocio y enlace a cada página/artículo, en el formato que leen los crawlers de IA (GEO) — recomendado por la auditoría de Katapulta.
- Schema `Organization`/`ProfessionalService` en `index.html`: ahora incluye `logo` (`assets/logo.png`, generado a partir de `logo.svg` para el Knowledge Panel) y `sameAs` con tu LinkedIn (`linkedin.com/in/sergiokstm`). Si añades Instagram o Facebook, dímelo y los incorporo a `sameAs`.

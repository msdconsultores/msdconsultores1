# msdconsultores1

Mirror estático **autosuficiente** de [msdconsultores.com](https://www.msdconsultores.com/),
generado con Playwright (render JS) y reescritura completa de URLs a rutas locales.

## Páginas

- `index.html` — Inicio
- `servicios.html` — Servicios
- `contacto.html` — Contacto
- `book-online.html` — Reserva online (estática)
- `p.html` — Página adicional
- `service-page/asistencia-tecnica-presencial.html`
- `service-page/asistencia-tecnica-remota.html`

## Estructura

- `assets/` — 223 recursos (CSS, imágenes, fuentes...) descargados localmente y referenciados con rutas relativas.
- 0 dependencias externas a Wix CDN en el HTML.
- Bloques `<script>` eliminados (snapshot post-render).
- Bloques `@font-face` con URLs a Wix eliminados; las CSS variables de fuente caen al fallback `arial, helvetica, sans-serif`.

## Limitaciones del snapshot estático

- "Reservar online" (Wix Bookings) ya no funciona como tal: la pantalla se ve, pero no agenda nada.
- Formularios apuntan a `https://formspree.io/f/REEMPLAZAR_ENDPOINT`. Sustituir por el endpoint real de [Formspree](https://formspree.io).
- Sin animaciones JS ni interacciones complejas (sliders, accordions dinámicos).
- Texto y diseño visual conservados.

## Servir localmente

```bash
npx serve .
# o
python -m http.server 8000
```

## GitHub Pages

Settings → Pages → Branch: `main` / `/ (root)` → guardar.
URL pública: `https://msdconsultores.github.io/msdconsultores1/`

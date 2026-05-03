# msdconsultores1

Mirror estático del sitio web **[msdconsultores.com](https://www.msdconsultores.com/)** generado con `wget --mirror`.

## Contenido

Este repositorio contiene una copia HTML estática de las páginas públicas del sitio:

- `index.html` — Página principal
- `servicios.html` — Servicios
- `contacto.html` — Contacto
- `book-online.html` — Reserva online
- `p.html` — Página adicional
- `service-page/asistencia-técnica-presencial.html`
- `service-page/asistencia-técnica-remota.html`

## Notas técnicas

El sitio original está construido sobre **Wix**, que renderiza la mayor parte de su contenido (estilos, imágenes, scripts y fuentes) de forma dinámica desde sus CDNs (`static.wixstatic.com`, `static.parastorage.com`, `siteassets.parastorage.com`).

Por ese motivo:

- El HTML descargado contiene el contenido de texto y las URLs absolutas a los recursos en los CDNs de Wix.
- Para que las páginas se vean correctamente al abrirlas en un navegador, es necesario tener conexión a Internet (el navegador cargará CSS/JS/imágenes directamente desde los servidores de Wix).
- Sin Internet, solo se conservará el texto y la estructura HTML, pero los estilos no se aplicarán.

## Cómo se generó

```bash
wget --mirror \
     --convert-links \
     --adjust-extension \
     --page-requisites \
     --span-hosts \
     --domains=msdconsultores.com,www.msdconsultores.com,static.parastorage.com,static.wixstatic.com,siteassets.parastorage.com,fonts.gstatic.com,fonts.googleapis.com \
     --user-agent="Mozilla/5.0" \
     -e robots=off \
     https://www.msdconsultores.com/
```

## GitHub Pages

Como el `index.html` está en la raíz, se puede activar GitHub Pages desde *Settings → Pages → Branch: main / root* y servirá esta copia estática.

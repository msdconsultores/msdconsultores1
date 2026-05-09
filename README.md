# msdconsultores1

Sitio web estático **autosuficiente** de [MSD Consultores](https://www.msdconsultores.com/), generado a partir del Wix original con render JS y servido a través de GitHub Pages.

## Estado

- 7 páginas HTML (Inicio, Servicios, Contacto, Reserva, Política, dos service-page).
- 235 assets locales en `assets/` (CSS, JS, imágenes, fuentes).
- **0 dependencias externas** a CDNs de Wix en el HTML.
- Bloques `<script>` y `@font-face` externos eliminados.
- `<link rel="canonical">` y Open Graph apuntan a `https://www.msdconsultores.com/...`.
- `CNAME` configurado para servir el dominio `www.msdconsultores.com`.

## Estructura

```
.
├── index.html              # Inicio
├── servicios.html
├── contacto.html
├── book-online.html
├── p.html                  # Política de privacidad
├── service-page/
│   ├── asistencia-técnica-presencial.html
│   └── asistencia-técnica-remota.html
├── assets/                 # Imágenes, CSS, JS, fuentes
├── 404.html                # Página de error
├── CNAME                   # Dominio personalizado
├── robots.txt
├── sitemap.xml
└── .nojekyll               # Evita procesado Jekyll en GitHub Pages
```

## Migración del dominio msdconsultores.com a GitHub Pages

Cuando vayas a apagar Wix, sigue estos pasos en orden:

### 1. Configurar GitHub Pages para usar tu dominio

1. https://github.com/msdconsultores/msdconsultores1/settings/pages
2. En **"Custom domain"**, escribe `www.msdconsultores.com` y pulsa **Save**.
3. Marca **"Enforce HTTPS"** (estará disponible una vez DNS apunte correctamente).

### 2. Cambiar los registros DNS

En el panel del registrador de tu dominio (donde tienes contratado `msdconsultores.com`), aplica:

**Apex (msdconsultores.com → www con redirección automática):**
```
Tipo  Nombre  Valor
A     @       185.199.108.153
A     @       185.199.109.153
A     @       185.199.110.153
A     @       185.199.111.153
```

**Subdominio www (lo que sirve realmente la web):**
```
Tipo   Nombre  Valor
CNAME  www     msdconsultores.github.io
```

Borra cualquier registro A/AAAA/CNAME previo apuntando a Wix (suelen ser CNAMEs a `*.wix.com` o A records de su rango).

### 3. Esperar propagación

DNS tarda entre 5 minutos y 48 horas en propagarse. Comprueba con:
```
nslookup www.msdconsultores.com
nslookup msdconsultores.com
```
Deben devolver IPs de GitHub (`185.199.108.0/22`).

### 4. Verificar HTTPS

Una vez propagado, GitHub Pages emitirá un certificado Let's Encrypt automáticamente. Marca "Enforce HTTPS" en Settings → Pages si no se marcó solo.

### 5. Desactivar Wix

Cuando confirmes que `https://www.msdconsultores.com/` carga este repo, ya puedes cancelar Wix.

## Limitaciones del snapshot estático

- **Reservar online** (Wix Bookings): pantalla visible, sin backend de reservas. Si necesitas mantener esa funcionalidad, hay que enchufarla a otro servicio (Calendly, Cal.com, etc.).
- **Formularios**: apuntan a `https://formspree.io/f/REEMPLAZAR_ENDPOINT`. Sustituir por el endpoint real de [Formspree](https://formspree.io) cuando lo crees.
- **Sin animaciones JS** complejas: el snapshot post-render conserva el aspecto visual estático pero no las interacciones avanzadas.

## Servir localmente para pruebas

```bash
npx serve .
# o
python -m http.server 8000
```

## Generación

Capturado con Playwright (`snapshot.js`) + Node fetch (`fetch-missing.js`) sobre el sitio Wix original. Los scripts de generación viven en `C:\scr\msd\`.

# Aires — Portafolio de Laura Aires — Brief de Contexto

Este proyecto viene de una sesión previa en Claude.ai (chat). Aquí está todo el contexto necesario para continuar sin perder decisiones ya tomadas.

**Ubicación (actualizado 2026-08-05):** el proyecto vive ahora en `C:\Users\laura\Documents\aires-portfolio` — se movió desde `Downloads` a pedido de Laura, para no perderlo si vacía la carpeta de Descargas. Puede quedar una copia vieja en `C:\Users\laura\Downloads\aires-portfolio` — es solo un remanente, **la copia real y con el historial de git es la de `Documents`**. Si una sesión nueva de Claude Code abre por defecto la de Downloads, hay que reabrirla apuntando a la de `Documents`.

## Quién es la clienta
Laura Aires — diseñadora gráfica sénior y directora creativa, 16 años de experiencia (Bogotá y Caracas). Actualmente Lead Designer en Backbone Technology. Construyendo su marca personal "Aires" para reemplazar su portafolio desactualizado de Behance (behance.net/lauraaires).

## Sistema de marca (YA APROBADO — no cambiar sin confirmar con ella)

**Colores:**
```css
--ink:      #0B0B1E;   /* fondo base */
--void:     #16152C;   /* superficies, tarjetas */
--iris:     #6C5CE0;   /* acento primario */
--sky:      #5B8FF0;   /* acento secundario */
--aqua:     #4FD8DC;   /* detalle, eyebrows, iconos */
--orchid:   #C773E0;   /* chispa, momentos puntuales */
--mist:     #A9A6C4;   /* texto secundario */
--paper:    #F3F1FA;   /* texto principal */
```
Paleta extraída de sus propias imágenes de referencia (texturas tipo "ondas de tela") + su isotipo existente.

**Tipografía** (Google Fonts):
- **Sora** — display/headings (peso 600-800). NO usar Unbounded (se probó y no le gustó — muy "juguetona"). NO usar tipografías serif.
- **Archivo** — cuerpo de texto (peso 300-500)
- **Space Grotesk** — eyebrows, labels, datos, fechas (peso 500-600)

**Concepto de marca:** "Aires" = brisa/movimiento. El elemento de firma visual es el MOVIMIENTO: fondos con degradados que fluyen lento (blobs con blur + animación CSS sutil), nunca elementos rígidos o esquinas duras. Fondo oscuro (dark mode) en todo el sitio.

**Logo:** tiene 3 versiones en `assets/images/`:
- `logotipo-blanco.png` — para fondos oscuros (nav, footer)
- `logotipo-gradiente.png` — a color, para showcase de marca
- `isotipo.png` — solo el símbolo, para fondos claros

**Foto de perfil:** tratamiento circular con anillo degradado cónico (iris→sky→aqua→orchid). Ver `.photo-ring` / `.about-ring` en el CSS existente.

**Iconografía:** línea (no rellenos), trazo 1.5-1.75px, esquinas y remates redondeados, grid 24px. Estilo tipo Lucide/Phosphor — coherente con las terminales redondas del isotipo. Evitar íconos 3D, degradados internos, o glassmorphism.

## Qué ya está construido

En `styleguide/index.html` y `site/index.html` (ambos self-contained, imágenes en base64):

1. **Guía de estilo** (`styleguide/index.html`) — referencia viva de todo el sistema: paleta, tipografía, tratamiento de movimiento, logo, iconografía, componentes (botones, tarjetas).
2. **Home** (`site/index.html`) — **reconstruido completo el 2026-08-04** (Laura trajo una versión nueva desde otra carpeta/sesión, ejecutada a partir de `CODE_PROMPT_HOME_REBUILD.md`, y la fusionamos como base actual). Estructura actual, en orden:
   - **Nav** — logo blanco + links (Proyectos, Servicios) + CTA Contacto.
   - **Hero con video** — `assets/video/hero-loop.mp4` de fondo (autoplay, muted, loop, playsinline) con viñeta/fog para legibilidad + grain. Headline "Fluir. Crear. Transformar." con degradado parcial. Sin eyebrow (se quitó en este rebuild).
   - **Proyectos** — mosaico bento de 4 tarjetas (1 grande + 3 medianas), tilt 3D al hover siguiendo el cursor + zoom sutil de imagen. Placeholders con las texturas `wave-0X.jpg`, nota visible de que son temporales.
   - **Servicios** — combina disciplinas + herramientas: a la izquierda pila de tarjetas 3D arrastrable (`.stage`/`.deck`, basada en `demos/3d-card-stack.html`) con las **6 disciplinas** (UX/UI, Redes Sociales, Audiovisual, Fotografía, Transformación con IA, Branding — actualizado 2026-08-05, cada tarjeta enlaza a `servicios.html`); a la derecha texto + badges de herramientas (Photoshop, Illustrator, After Effects, Premiere, Lightroom, Figma, Adobe XD, Sketch, IA Generativa).
   - **Bio** — foto editorial rectangular (`portrait-laura-sm.jpg`) + headline + bio + nombre completo "Laura Aires Cabada" + rol + link LinkedIn + stats (16+ años, 100+ marcas, 900+ proyectos).
   - **Testimonios** — sección nueva, 3 tarjetas placeholder (5 estrellas + cita + nombre/cargo) claramente marcadas para reemplazar con recomendaciones reales de LinkedIn.
   - **Contacto** — email + teléfono (+57 350 632 4136) + link LinkedIn (placeholder de URL).
   - **Footer** — logo + año.
   - **Animación**: sistema `.reveal` por IntersectionObserver (fade + slide + scale + blur sutil), con entrada escalonada en cascada por elemento en mosaico/testimonios/badges (no como bloque único). El hero anima su propio contenido al cargar (sin depender de scroll). Tilt 3D en tarjetas de proyecto, drag/autoplay en la pila de disciplinas. Glow que sigue el cursor (`.cursor-glow`, oculto en touch/mobile). Video del hero a 0.6x de velocidad (`playbackRate`, vía JS — no se reencodeó el archivo). Todo vanilla JS, respeta `prefers-reduced-motion`.
   - **Botón flotante de WhatsApp** (`.wa-float`) — fijo abajo a la derecha, enlaza a `https://wa.me/573506324136`, presente en todas las páginas del sitio.
   - **Nota:** la categoría "Mailing" seguía presente en el rebuild externo original — se quitó; el 2026-08-05 Laura pidió expandir a 6 disciplinas con nombres nuevos (ver arriba), reemplazando el set anterior de 5.

Todo el HTML/CSS es vanilla (sin framework) — decisión deliberada por simplicidad, dado que es un sitio mayormente estático sin lógica compleja. Si crees que conviene migrar a un framework (Astro, Next, etc.) para las páginas internas, coméntalo con ella antes de decidir — no asumas.

**`demos/3d-card-stack.html`** — prototipo standalone del efecto de pila de tarjetas 3D, usado como referencia/base para la sección Servicios. No es parte del sitio final, es solo un demo de trabajo.

3. **Proyectos** (`site/trabajo.html`) — página general de trabajo (construida 2026-08-05, referencia visual: backbone.digital/nuestro-trabajo, sin tabs de filtro por categoría). Banner de video (mismo `hero-loop.mp4` del Home, reemplazar cuando Laura entregue su propio video/imagen), sección de galería con **fondo claro** (`--paper`, ruptura intencional del dark mode solo en esta sección, pedida por Laura) con grid de tarjetas placeholder (imagen + categoría + nombre), tilt 3D al hover. Banner de cierre en degradado oscuro que enlaza a Servicios. Contacto al final. Placeholders con las texturas `wave-0X.jpg`/`fluid-*.jpg`, cada tarjeta enlaza a `proyecto.html`.
4. **Proyecto individual** (`site/proyecto.html`) — plantilla genérica de case study (construida 2026-08-05, referencia: backbone.digital/nuestro-trabajo/celestyal-cruises-copy, simplificada). Banner con imagen de fondo (no video) + breadcrumb + título + descripción corta, fila de tags/pills de servicios usados (ej. "Diseño Web", "Branding"), luego una galería de mockups a pantalla casi completa (bloques full-width alternados con pares de 2 columnas) con poco texto — pensada para que el trabajo visual cargue el peso, ya que Laura no tiene mucho texto por proyecto (mucho trabajo es de agencia). Enlace de vuelta a Proyectos. Contacto al final. **Es una plantilla única reutilizada** — todavía no hay una página por proyecto individual.
5. **Servicios** (`site/servicios.html`) — construida 2026-08-05, **rediseñada el mismo día** tras feedback de Laura. Banner con copy definitivo ("De la idea a una experiencia bien construida"). Lista editorial en zigzag (`.svc-list`/`.svc-row`, fondo claro `--paper`) con **5 servicios** — Branding, Redes Sociales, Audiovisual, Fotografía, Creatividad con IA — cada fila alterna icono izq/der, ícono circular con halo de gradiente animado (pulso + flotación sutil), sin numeración visible, reveal direccional (entra desde izquierda o derecha según la fila, no solo fade). **Nota: esto ya no incluye "UX/UI"** — el set anterior de 6 (con UX/UI) quedó reemplazado por este de 5 con copy real; el deck de disciplinas del Home todavía tiene el set viejo de 6, pendiente de confirmar con Laura si debe sincronizarse (ver Pendientes). Debajo, "Por qué trabajar conmigo" con subtítulo + intro + 4 ventajas con copy final de Laura (De principio a fin / Diseño con esencia / IA con mirada humana / Experiencia sin fronteras). Contacto al final.

**Nav en las 4 páginas (2026-08-05):** logo siempre enlaza a `index.html`. Menú hamburguesa (`.nav-burger` / `#navMobile`) a partir de 720px de ancho — overlay a pantalla completa con Inicio/Proyectos/Servicios/Contacto, animado con stagger.

## Sitemap completo (actualizado 2026-08-05)

- `site/index.html` — Home ✅
- `site/trabajo.html` — Proyectos (listado general) ✅
- `site/proyecto.html` — Plantilla de proyecto individual ✅ (una sola plantilla, sin páginas por proyecto todavía)
- `site/servicios.html` — Servicios ✅

**Cambio de rumbo:** el plan anterior de 5-6 páginas internas, una por disciplina (`/web-ui`, `/redes-sociales`, etc.), quedó reemplazado por este esquema de Proyectos + Servicios + plantilla de proyecto — más parecido a un portafolio de estudio que a un menú por disciplina. No se construyeron las páginas por disciplina.

## Pendiente / bloqueadores

- **Imágenes/video reales** — para el mosaico de Home, el banner y grid de `trabajo.html`, y los mockups de `proyecto.html`. Todo marcado con nota visible de placeholder.
- **Contenido real por proyecto** — `proyecto.html` es una plantilla única; cuando Laura mande material de proyectos concretos, hay que decidir si se duplica el archivo por proyecto o se pasa a un sistema con datos (fuera de alcance por ahora, es sitio estático).
- **Testimonios reales** — 3 recomendaciones de LinkedIn para reemplazar las tarjetas placeholder en Home.
- **Redes sociales** — falta la URL real de LinkedIn (y confirmar si agrega Instagram) en Bio, Contacto y footer.
- **Deploy — YA EN VIVO (2026-08-05).** Repo en GitHub: `github.com/lauraaires89-lab/Airescreative`, conectado a Vercel con auto-deploy (cada push a `main` se publica solo). Como el sitio real vive en `site/*.html` con `assets/` en la raíz del repo, `/` redirige (redirect real, no rewrite — ver nota abajo) a `/site/index.html`; `vercel.json` tiene esa regla, `_redirects` es la misma regla por si algún día se usa Netlify en vez de Vercel.
  - **Importante para futuros cambios:** si algún día se reestructuran las carpetas, revisar que `vercel.json` siga apuntando bien — usa un **redirect** (cambia la URL del navegador a `/site/...`) y no un **rewrite** (mantiene la URL en `/`), porque con rewrite los links relativos internos (`trabajo.html`, `servicios.html`, etc.) se rompían con 404 al no resolver contra `/site/`.
- **Firebase Hosting — también en vivo (2026-09-01).** Proyecto Firebase `Airescreative` (ID real: `airescreative-4a39e`). URL: `https://airescreative-4a39e.web.app`. Mismo patrón que Vercel: `firebase.json` sirve desde la raíz del repo (`"public": "."`) con un redirect 302 de `/` a `/site/index.html`, e ignora `contenido-nuevo/`, archivos `.md`, `.git`, etc. `.firebaserc` fija el proyecto por defecto. Este deploy es **manual** (no automático como Vercel) — para publicar cambios hay que correr `firebase deploy --only hosting` desde la raíz del repo después de cada `git push`.
  - **Firebase CLI:** el instalador standalone de Windows ("firepit") tiene un bug en este entorno (falla con `SyntaxError: Unexpected end of JSON input` en su chequeo de bienvenida) — no usar ese método. En su lugar hay un Node.js portátil en `C:\Users\laura\dev-tools\node-v20.18.1-win-x64` y Firebase CLI instalado vía npm en `C:\Users\laura\dev-tools\npm-global`. Para usarlo en una sesión nueva: `export PATH="/c/Users/laura/dev-tools/node-v20.18.1-win-x64:/c/Users/laura/dev-tools/npm-global:$PATH"` y luego `firebase deploy --only hosting`. La sesión de login (`lauraaires89@gmail.com`) queda guardada, no hay que volver a autenticar salvo que expire.
- **Dominio propio conectado (2026-09-01).** Laura compró `airescreative.com` en **Namecheap** y lo conectó a Firebase Hosting (no a Vercel — eligió Firebase como el definitivo). Configuración en Namecheap → Advanced DNS:
  - `A` @ → `199.36.158.100` (verificado, el dominio principal ya sirve el sitio)
  - `TXT` @ → `hosting-site=airescreative-4a39e` (verificación de propiedad)
  - `CNAME` www → `airescreative-4a39e.web.app` (agregado, pendiente de propagación/verificación en Firebase al momento de escribir esto — para que `www.airescreative.com` redirija al dominio raíz)
  - Se eliminó el `A` record viejo (`192.64.119.188`, parking de Namecheap) y el "URL Redirect Record" por defecto que traía el dominio.
  - Todo esto se gestiona desde Firebase Console → Hosting → dominios personalizados (no hay comando de CLI para agregar dominios custom, es solo por la consola web).

## Cómo prefiere trabajar Laura
No es técnica — no espera tocar código. Da dirección visual y contenido (imágenes, textos, gustos/disgustos), espera que Claude construya y ajuste. Le gusta ver resultados rápido y iterar con feedback directo y específico.

## Assets disponibles
Carpeta `assets/images/`: logo (3 versiones), isotipo, foto de perfil, 3 texturas de referencia ("wave-01/02/03.jpg"), 3 texturas fluid ("fluid-back/mid/front.jpg").
Carpeta `assets/video/`: `hero-loop.mp4` (video de fondo del hero) + `hero-poster.jpg` (poster/fallback).
Carpeta `assets/fonts/`: Archivo, Sora, Space Grotesk (.ttf, para uso en Illustrator/Photoshop si los necesita — el sitio web usa Google Fonts vía CDN, no estos archivos locales).

# PROMPT PARA CLAUDE CODE — Reconstruir Home completo

Pega esto como un solo mensaje en la sesión de Claude Code que ya tiene el proyecto `aires-portfolio` abierto.

---

Lee primero `PROJECT_BRIEF.md` para el sistema de marca completo (colores, tipografía, concepto). No lo repito todo acá, solo lo que cambia o se agrega.

Vamos a reconstruir `site/index.html` completo con esta estructura, en este orden exacto. Referencia de dirección: un reel de Instagram de un portafolio (usuario ruchitdesigns) — mismo tipo de estructura y nivel de pulido, pero en nuestra paleta y sin ilustración de personaje.

## 1. Nav
Igual a como está — logo blanco + links + CTA contacto. Sin cambios.

## 2. Hero
Impactante, pantalla completa, con la atmósfera animada que ya existe (blobs + wave texture + grain). SIN mascota ni ilustración de personaje — el hero es 100% tipográfico + atmósfera.
- Eyebrow: "Laura Aires — Directora Creativa"
- Headline grande (Sora, con degradado parcial como ya está)
- Subheadline corto
- Dos CTAs: "Ver trabajo" (primario) / "Hablemos" (ghost)
- Nota: voy a mandar imágenes propias para esta sección más adelante — deja el layout listo para recibir una imagen o video de fondo/lateral si hace falta, pero no bloquees la construcción esperando eso.

## 3. Últimos Proyectos (máximo 4)
Grid tipo mosaico/bento (NO todas las tarjetas del mismo tamaño — variar 1 grande + 3 medianas, o 2x2 con una ocupando doble ancho), con ligera perspectiva 3D en hover: al pasar el mouse, la tarjeta se inclina siguiendo la posición del cursor (`transform: perspective() rotateX() rotateY()` calculado con JS on mousemove) y la imagen hace zoom sutil. Cada tarjeta: imagen de portada, nombre de cliente, categoría/tag, link a detalle (aunque la página de detalle no exista todavía, deja el `href` listo).
- Contenido: 4 proyectos placeholder por ahora (voy a crear un proyecto/carpeta con todo el material y te lo paso) — usa las texturas de `assets/images/wave-0X.jpg` como imagen temporal y marca claramente con una nota visible que son placeholders.
- CTA al final de la sección: "Ver todo el trabajo" (aunque la página de "todo el trabajo" no exista aún, déjalo listo).

## 4. Por Tipo de Trabajo
Las 6 disciplinas, usando el efecto de pila de tarjetas 3D que ya prototipé en `demos/3d-card-stack.html` — impórtalo y adáptalo a esta sección (reutiliza ese código, no lo reinventes). Cambios respecto al prototipo:
- Debe responder también al mouse/drag, no solo rotar sola con setInterval — que el usuario pueda arrastrar o hacer click en los dots para navegar.
- Al hacer click en una tarjeta, debe llevar a la página de esa disciplina (`/web-ui`, `/redes-sociales`, `/video`, `/fotografia`, `/ia`, `/mailing` — aunque no existan aún, deja los `href` listos).
- Mismas 6 categorías, iconos y textos que ya están en el prototipo.

## 5. Herramientas y Skills
Contenido ya existe en el CV — reutiliza exactamente estas categorías (ya están en `site/index.html` actual, no las reescribas):
- Diseño & Motion: Photoshop, Illustrator, After Effects, Premiere, Lightroom
- Producto & UX: Figma, Adobe XD, Sketch
- IA & Producción Generativa: imágenes y video de alto impacto visual, flujos basados en nodos, modelos conversacionales integrados a la estrategia creativa

Puedes mantener el layout de 3 paneles que ya existe, o mejorarlo visualmente si tienes una idea más fuerte — pero no cambies el contenido.

## 6. Biografía
Como la referencia del video: foto grande (no necesariamente circular esta vez — prueba con un formato más editorial, rectangular con esquinas redondeadas, ocupando buen espacio) a un lado, headline corto tipo "Diseño con memoria, movimiento y una pizca de IA" (o algo en esa línea — puedes proponer variantes), párrafo de bio debajo, nombre + título, e iconos de redes sociales pequeños.
- Foto: usa `assets/images/portrait-laura-sm.jpg` por ahora.
- Reutiliza el texto de bio que ya existe en la sección "Sobre mí" actual, solo cambia el tratamiento visual para que se sienta más como la referencia (más grande, más protagonista, menos "tarjeta pequeña").
- Incluye los mismos 3 datos numéricos (16+ años, 6 disciplinas, 2 países) pero intégralos con más fuerza visual.

## 7. Testimonios
Sección nueva. Grid o carrusel de tarjetas con: cita (texto), calificación (5 estrellas, ícono outline relleno con `--aqua` o `--iris`), nombre de la persona, cargo/empresa.
- Voy a sacar el contenido real de mis recomendaciones de LinkedIn — por ahora deja 3 tarjetas con contenido placeholder claramente marcado (ej. "Cita de testimonio — reemplazar con contenido real de LinkedIn"), mismo estilo visual que el resto del sitio (fondo `--void`, borde `--line`).

## 8. Contacto
Mantén la sección de contacto actual (headline + email como CTA), pero agrega:
- Teléfono
- Iconos/links de redes sociales (Instagram, LinkedIn — dejar como placeholder de URL, yo las relleno después)

## 9. Footer de cierre
Como la referencia del video: un wordmark gigante de cierre antes del footer chico final — "AIRES" o "LAURA AIRES" en Sora ExtraBold, ocupando casi todo el ancho, con el degradado de marca (iris→sky→aqua). Debajo, footer pequeño normal (logo + ubicación + año).

---

## Reglas generales para toda la construcción
- Reutiliza el sistema de tokens CSS que ya existe (`--ink`, `--void`, `--iris`, `--sky`, `--aqua`, `--orchid`, `--mist`, `--paper`) — no inventes colores nuevos.
- Tipografía: Sora (headings), Archivo (cuerpo), Space Grotesk (labels/datos) — ya cargadas vía Google Fonts CDN en el `<head>`.
- Mantén el archivo autocontenido (imágenes en base64 o rutas relativas dentro del proyecto, nunca URLs externas rotas).
- Todo el movimiento debe ser sutil y lento (nada abrupto) — coherente con el concepto de marca "Aires" = brisa/movimiento.
- Responsive: que se vea bien en mobile, aunque el efecto 3D de la pila de tarjetas puede simplificarse a swipe simple en pantallas chicas si el drag con mouse no aplica.
- Antes de darlo por terminado, revisa tu propio resultado (screenshot si tu entorno lo permite) contra esta lista de 9 secciones y confirma que estén todas, en orden, sin la sección de FAQs (esa se elimina por completo, no va en el sitio).

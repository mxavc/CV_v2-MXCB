# Heurísticas de Nielsen aplicadas

Cada fila describe una decisión concreta y verificable, y dónde está implementada. Se citan selectores e identificadores (no números de línea) para que la tabla siga siendo válida al editar los archivos.

**Concepto visual (versión 2):** «Del laboratorio al código». El CV se presenta como una ficha de espécimen de laboratorio sobre papel milimetrado con acentos de editor de código: la foto va dentro de una «placa de Petri», las habilidades forman una tabla periódica y las tarjetas usan sombras sólidas desplazadas.

| # | Heurística | Implementación | Archivo y selector |
|---|---|---|---|
| 1 | Visibilidad del estado del sistema | Al hacer scroll, el enlace de la sección visible se resalta (fondo lima, borde y subrayado) y recibe `aria-current="true"`. | `js/main.js` (`IntersectionObserver` de `.nav-link`); `css/styles.css` `.nav-link[aria-current="true"]` |
| 1 | | Barra de progreso de lectura en el borde superior de la ventana. | `index.html` `.scroll-progress`; `js/main.js` `onScroll()` |
| 1 | | Estados claros de hover, active y foco: los botones se elevan con una sombra sólida y se «hunden» al pulsarlos. | `css/styles.css` `:focus-visible`, `.btn:hover`, `.btn:active`, `.nav-link:hover` |
| 1 | | Al copiar el email aparece «Copiado ✓» en una región `role="status" aria-live="polite"`, que se borra a los 3 s. | `index.html` `#copy-status`; `js/main.js` `showStatus()` |
| 1 | | El botón de tema muestra la acción disponible («Modo claro» / «Modo oscuro») y su ícono. | `js/main.js` `renderTheme()` |
| 2 | Coincidencia con el mundo real | Secciones convencionales de un CV, numeradas 01–06 como en un índice: Perfil, Experiencia, Educación, Proyectos, Habilidades y Contacto. | `index.html` `.section-head` y `.nav-num` |
| 2 | | Metáforas del mundo del autor (biología): «Muestra n.º 001», «fig. 01», placa de Petri, tabla periódica de habilidades con símbolo, número y familia. | `index.html` `.hero`, `.periodic` |
| 2 | | Fechas en formato local («nov. 2019 – dic. 2021») con `<time datetime>`. Español (`lang="es"`). WhatsApp en formato legible («+593 99 990 5758»). | `index.html` `.entry-meta`, `#contacto` |
| 3 | Control y libertad del usuario | Botón flotante «Volver arriba», que aparece al bajar 600 px. Sin JS siempre está visible. | `index.html` `.to-top`; `css/styles.css` `.js .to-top:not(.is-visible)` |
| 3 | | Tema reversible: si la elección coincide con la del sistema, se borra la preferencia y se vuelve a seguir al sistema. | `js/main.js` (clic en `#theme-toggle`) |
| 3 | | Los enlaces externos llevan el ícono ↗, el texto oculto «(abre en pestaña nueva)», `target="_blank"` y `rel="noopener noreferrer"`. | `index.html` `.icon-ext` + `.sr-only` |
| 4 | Consistencia y estándares | Un único componente `article.entry` (meta, título, organización y lista) para experiencia, educación y proyectos; las tarjetas comparten `.card`. | `css/styles.css` `.entry-*`, `.card` |
| 4 | | Mismo lenguaje visual en todo el sitio: borde de 2 px en tinta, sombra sólida desplazada, píldoras redondeadas, etiquetas en monoespaciada. | `css/styles.css` `.btn`, `.card`, `.fab`, `.sticker`, `.section-num` |
| 4 | | Convenciones web: el logotipo «Mc» lleva al inicio, enlaces subrayados, `mailto:`, `wa.me`, landmarks `header`/`nav`/`main`/`footer`, un único `h1` y jerarquía h1→h2→h3. | `index.html` `.brand` |
| 5 | Prevención de errores | Correos, LinkedIn y WhatsApp copiados literalmente de los datos originales; `wa.me` en formato internacional sin `+` ni espacios. | `index.html` `#contacto`, `.whatsapp-fab` |
| 5 | | El botón de imprimir explica qué hace y en qué termina («Elige «Guardar como PDF»…»). | `index.html` `#print-btn` |
| 5 | | Los controles que dependen de JS se ocultan si JS no carga; las animaciones de aparición solo ocultan contenido si el navegador puede volver a mostrarlo. | `css/styles.css` `.no-js .js-only`, `[data-reveal]`; `js/main.js` |
| 6 | Reconocer antes que recordar | Las secciones están siempre a la vista: riel lateral fijo en escritorio (≥ 1100 px), cabecera fija en tablet y fila desplazable en móvil. `scroll-padding-top` evita que la cabecera tape el destino. | `css/styles.css` `.site-header` y sus `@media`; `js/main.js` (`--header-h`) |
| 6 | | Todos los íconos van con texto visible; los SVG llevan `aria-hidden="true"`. Las habilidades muestran símbolo **y** nombre completo, y cada familia tiene título y color. | `index.html` `.element`, `.family-name` |
| 7 | Flexibilidad y eficiencia | Skip link «Saltar al contenido», visible al recibir foco. | `index.html` `.skip-link` |
| 7 | | Anclas compartibles por sección (`#`) junto a cada `h2`. | `index.html` `.anchor` |
| 7 | | Atajos de contacto: email y LinkedIn como botones en la portada; WhatsApp flotante en cualquier punto del scroll. | `index.html` `.quick-contact`, `.whatsapp-fab` |
| 7 | | Imprimir o guardar como PDF desde la cabecera (o Ctrl+P). | `index.html` `#print-btn`; `js/main.js` |
| 8 | Diseño estético y minimalista | Paleta reducida: tinta verde-negra, papel y un único acento lima (siempre como fondo, nunca como texto sobre claro). Los colores de familia solo aparecen en habilidades e intereses. Todo vive en variables de `:root`. | `css/styles.css` §1 Tokens |
| 8 | | Tipografía solo del sistema (sin descargas): sans de display muy pesada para títulos y monoespaciada para metadatos. | `css/styles.css` `--font-display`, `--font-mono` |
| 8 | | Movimiento con propósito y discreto: anillo de la placa que gira lento y bloques que aparecen al entrar en pantalla. | `css/styles.css` §8 |
| 9 | Reconocer, diagnosticar y recuperarse de errores | `404.html` explica el error, muestra la ruta solicitada y ofrece «Ir al inicio del CV». Estilos en línea para funcionar en cualquier ruta. | `404.html` |
| 9 | | Si el portapapeles falla, el email queda seleccionado y se indica «pulsa Ctrl+C (⌘+C en Mac)». | `js/main.js` `copyFailed()`; `css/styles.css` `.copy-status.is-error` |
| 10 | Ayuda y documentación | `title` y `aria-label` descriptivos en todos los controles. Las abreviaturas llevan `<abbr title>` (p. ej. PCR). | `index.html` |
| 10 | | Sección Contacto explícita con instrucciones («La forma más rápida de contactarme es por correo»). | `index.html` `#contacto` |
| 10 | | `README.md` explica la estructura, cómo editar y cómo publicar. | `README.md` |

## Accesibilidad (WCAG 2.2 AA), transversal

- **Contraste:** texto principal ≈ 15:1 sobre papel; texto secundario `#4a5650` ≈ 7:1; enlaces `#0b6150` ≈ 6.6:1. El lima solo se usa como fondo con texto en tinta (≈ 14:1). En oscuro, texto `#e6ede8` y enlaces `#8de3c8` sobre `#0d1311`. Al editar colores, vuelve a comprobar que todo siga en ≥ 4.5:1.
- **Teclado:** foco visible de 3 px en todos los controles; orden de tabulación según el documento.
- **Tamaño de los objetivos táctiles:** botones y botones flotantes de 44 px de alto (40 px el de copiar).
- **Movimiento:** `prefers-reduced-motion: reduce` desactiva el giro, el pulso, las apariciones y el scroll suave.
- **Impresión:** blanco y negro, una columna, sin navegación, botones ni decoración; foto en escala de grises y URL externas visibles.

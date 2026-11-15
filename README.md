# Gastronomía en femenino

Sitio web estático sobre mujeres que han marcado la gastronomía: chefs, cocineras y divulgadoras, con fichas biográficas, recetas, galerías de imágenes y vídeo.

Lo desarrollé en las prácticas (PEC) de la asignatura **Herramientas HTML y CSS II** (M4.257) del Máster en Desarrollo de Aplicaciones Web de la UOC. El proyecto creció a lo largo de tres prácticas: maquetación semántica y accesible, optimización de imágenes y animación SVG, y, por último, optimización del rendimiento web.

🔗 **Web publicada:** https://gastronomia-en-femenino.netlify.app/

## Páginas

| Página | Contenido |
| --- | --- |
| `index.html` | Portada con banner recortado mediante `clip-path` y fichas destacadas |
| `categoria.html` | Listado de mujeres destacadas en tarjetas |
| `det1.html` | Ficha de Montse Guillén: biografía, receta, galería y vídeo |
| `det2.html` | Ficha de María Gómez (Magoga): biografía, receta, galería y vídeo |
| `links.html` | Fuentes consultadas y créditos de textos e imágenes |

## Tecnologías

- **HTML5** semántico y **CSS3** (Flexbox, Grid, `@keyframes`, `clip-path`, `aspect-ratio`)
- **JavaScript** sin dependencias: menú hamburguesa, `aria-current`, galería modal y fachada del vídeo de YouTube
- **[Parcel 2](https://parceljs.org/)** como empaquetador, con:
  - `posthtml-include` y `posthtml-expressions` para componentes reutilizables (cabecera, pie y bloques `<picture>`)
  - `htmlnano`, `cssnano` y `terser` para minificar
  - **sharp** para generar las imágenes en WebP y JPG a varios tamaños
- **SVG** dibujado en Inkscape y optimizado con SVGOMG (logotipo animado, favicon y máscara del recorte)
- Despliegue continuo en **Netlify**

## Aspectos destacados

**Imágenes responsive.** Se aplican las tres técnicas: cambio de resolución con `srcset` y `sizes`, densidad de píxeles (1x, 2x y 3x) y dirección de arte con `<picture>` y `media`, que sirve una imagen panorámica en escritorio y una cuadrada en móvil. Los componentes `picture-std`, `picture-std-high` y `picture-art` generan el marcado automáticamente.

**Optimización de imágenes.** Con sharp, el peso total de las imágenes bajó de 14,5 MB a unos 2,5 MB en WebP. Se mantienen JPG optimizados como respaldo para navegadores antiguos.

**Animación y SVG.** El logotipo está vectorizado e insertado *inline* con una animación de entrada. El banner de la portada usa un `clip-path` con `clipPathUnits="objectBoundingBox"`, de modo que el recorte se adapta al tamaño del contenedor. El favicon SVG cambia de aspecto con `prefers-color-scheme: dark`.

**Rendimiento.** Se aplicaron estas mejoras:
- `loading="lazy"` en todo lo que no se ve al cargar la página, y `fetchpriority="high"` en la imagen principal (LCP)
- script cargado con `defer`
- fuentes Playfair Display alojadas en el propio sitio (`.woff2` con `preload` y `font-display: swap`)
- solo los estilos de hover.css que realmente se usan, en lugar de la librería completa
- fachada ligera para el vídeo de YouTube
- `requestAnimationFrame` en la galería para evitar reflujos forzados

Resultado en PageSpeed Insights:

| Página | Móvil (antes → después) | Escritorio (antes → después) |
| --- | --- | --- |
| index | 89 → 100 | 99 → 100 |
| categoria | 87 → 100 | 97 → 100 |
| det1 | 56 → 100 | 83 → 100 |
| det2 | 59 → 100 | 99 → 100 |
| links | 90 → 100 | 99 → 100 |

En las páginas de detalle, con red 3G emulada, el tiempo de carga bajó de unos 20 s a unos 1,4 s.

**Accesibilidad y validación.** El HTML y el CSS pasan sin errores los validadores del W3C, y la herramienta WAVE no detecta errores de accesibilidad (WCAG). Las imágenes tienen `alt` y `lang`, y sus dimensiones están reservadas para evitar saltos de diseño (CLS).

## Estructura

```
├── src_P2/
│   ├── index.html, categoria.html, det1.html, det2.html, links.html
│   ├── includes/        # header, footer y componentes <picture>
│   ├── css/estilos.css
│   ├── js/script.js
│   ├── fonts/           # Playfair Display (.woff2)
│   └── img/
├── .posthtmlrc          # configuración de PostHTML (includes, variables, htmlnano)
├── sharp.config.json    # calidad de compresión de las imágenes
└── package.json
```

## Uso en local

Requiere [Node.js](https://nodejs.org/).

```bash
npm install
npm start          # servidor de desarrollo con recarga automática
npm run build      # genera la versión de producción en dist/
```

## Licencia

El **código** se publica con licencia [MIT](LICENSE).

Los **textos, fotografías y vídeos** que aparecen en el sitio pertenecen a sus autores y se usan solo con fines académicos. **La licencia MIT no los cubre.** Los créditos de cada recurso están en la página [Fuentes](https://gastronomia-en-femenino.netlify.app/links.html).

---

Pedro Otálora Giménez · Máster en Desarrollo de Aplicaciones Web (UOC)

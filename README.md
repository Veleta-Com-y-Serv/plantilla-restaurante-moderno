# Plantilla NoExpertise · Restaurante moderno

Web limpia y a todo el ancho para restaurantes de hoy: fotos grandes, carta, menú del día y reservas.

- Sectores: restaurante, bistro, gastrobar, cocina-de-autor, arroceria, asador. Estilo: limpio. Plan mínimo: gratis. Orden 640.
- Secciones: hero, sobre, especialidades, carta, galeria, reservas, horario-ubicacion, opiniones, preguntas, contacto (y `texto` para apartados nuevos).
- Diseño a ancho completo: portada con la foto a pantalla entera y la cabecera transparente encima, «La casa» con foto a sangre, especialidades como fotos de borde a borde sobre banda oscura, carta con el menú del día sobre el color de acento e índice de categorías, mosaico de fotos sin márgenes, reservas con foto y formulario, horario con la fachada y el mapa bajo demanda, opiniones en cita grande, contacto partido, pie oscuro y barra fija «Llamar / Reservar» en el móvil. Serif del sistema en titulares y sans del sistema en el texto. Detalle en `DISEÑO.md`.
- Ejemplo: Olmo, restaurante ficticio de cocina de mercado en Valladolid (teléfonos y correo de muestra).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD (`Restaurant`) y preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Varias páginas (opcional, `paginas:` en la raíz de `site.yaml`): Inicio + una página por entrada (`{ ruta, titulo, secciones: "a; b" }`, hasta 6) con el menú hecho solo; reparto recomendado en `template.yaml → paginas` (Carta, La casa, Reservas). Sin la clave, una sola página larga.
- Sin fichas por elemento ni páginas por zona (la carta son platos).
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en `CLAUDE.md`; fotos en `fotos.json` (14).

## Campos propios

| Sección | Campos |
|---|---|
| `hero` | `imagen`, `cta`, `cta_secundario`, `items` [{titulo}] (línea de detalles) |
| `sobre` | `declaracion`, `texto`, `imagen`, `items` [{titulo, texto}], `cta` |
| `especialidades` | `platos` [{nombre, texto, precio, imagen}], `cta` |
| `carta` | `imagen`, `marca_destacado`, `menu_dia` {titulo, precio, texto}, `platos` [{nombre, texto, precio, categoria, destacado}], `cta` |
| `galeria` | `galeria` [rutas], `cta` |
| `reservas` | `imagen`, `items` [{titulo, texto}], `cta`, `nota` |
| `horario-ubicacion` | `imagen`, `mapa` (sí/no), `horario` [{dia, horas}] |
| `opiniones` | `testimonios` [{texto, autor, nota}] |
| `preguntas` | `preguntas` [{pregunta, respuesta}] |

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) dibujadas para esta plantilla, sin licencias de terceros.

# Plantilla «Restaurante moderno» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **limpio**.
Todo en castellano de España, frases cortas, sin jerga. Brief de diseño completo en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = tinta de las bandas oscuras y del contacto, acento = botones, menú del día y detalles, fondo = hueso, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y Tailwind los expone como `bg-primario`, `text-acento`… Los derivados (`--oscuro` del pie y de la barra del móvil, `--claro`, `--hueso`, `--linea`, `--tenue`, `--acento-legible`) se calculan con `color-mix` en `src/styles/global.css`. El texto sobre primario, oscuro y acento se elige solo (claro u oscuro según el color).
- **Tipografías y aspecto general**: `src/styles/global.css` (serif del sistema en peso normal para títulos, sans del sistema para texto, botones píldora `.btn`/`.btn-sec`/`.btn--claro`, bandas `.banda--fondo|clara|hueso|oscura|acento`, mitades a sangre `.mitades`). Fuentes del sistema: no añadas fuentes externas.
- **Bandas**: `src/components/ui/Banda.astro` pinta una sección de borde a borde con el contenido en `.contenedor` (96 rem, 16 px de margen en móvil). Las mitades foto/texto (`.mitades`, `.mitad-texto`, `.mitad-foto`) dejan la foto tocando el borde de la ventana y alinean el texto con el contenedor.
- **Imágenes**: en `public/`. Fotos en `public/fotos/` (descritas en `fotos.json`); si una foto de `/fotos/` falta, `Imagen.astro` muestra `/placeholders/<mismo nombre>.svg`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Personas: siempre `/placeholders/persona.svg`, nunca caras generadas.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = nombre en texto en serif.
- **Cabecera y pie**: cabecera fija; si la página empieza por la portada con foto, va transparente encima de la foto hasta que se baja. El pie enseña el nombre enorme, el horario, la dirección, el contacto, el menú y las redes; en el móvil, barra fija con «Llamar» y el botón de la cabecera. «Web creada con NoExpertise»: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`, en el orden de `site.yaml`.
- `hero` → `secciones/hero.astro`: foto a pantalla entera, título enorme, dos botones y la línea de detalles (`items`).
- `sobre` → `secciones/sobre.astro`: foto a sangre a la izquierda; `declaracion`, párrafos y valores numerados (`items`).
- `especialidades` → `secciones/especialidades.astro`: banda oscura y `platos` como fotos a sangre con nombre, texto y precio encima.
- `carta` → `secciones/carta.astro`: menú del día (`menu_dia` sobre el acento junto a `imagen`), índice de categorías y `platos` por categoría.
- `galeria` → `secciones/galeria.astro`: mosaico a sangre, la primera foto doble, y botón a Instagram.
- `reservas` → `secciones/reservas.astro`: foto a sangre, pasos, WhatsApp y teléfono, `nota` y formulario de reserva.
- `horario-ubicacion` → `secciones/horario-ubicacion.astro`: horario, dirección y «Cómo llegar»; fachada (`imagen`) o plano dibujado y, con `mapa: true`, Google Maps al pulsar.
- `opiniones` → `secciones/opiniones.astro`: cita grande y el resto en columnas.
- `preguntas` → `secciones/preguntas.astro`: acordeón `details/summary`; sin preguntas no se pinta.
- `contacto` → `secciones/contacto.astro`: mitad oscura con las vías de contacto y mitad clara con el formulario.
- `texto` → `secciones/texto.astro`: apartado genérico (`tipo: texto`), con foto a sangre si lleva `imagen`.

## Campos propios de esta plantilla (además del esquema común)
- `hero`: `cta` y `cta_secundario` (sin `cta` el botón llama; sin `cta_secundario`, «Cómo llegar» al mapa); `items` = detalles cortos (solo `titulo`). Sin `imagen`, banda del color primario.
- `sobre`: `texto` largo (párrafos separados por una línea en blanco), `imagen` vertical, `declaracion` (frase corta en cursiva) e `items` (`titulo` + `texto`).
- `especialidades.platos` [{nombre, texto, precio, imagen}]: de 1 a 6 platos; sin `imagen`, tarjeta de color; sin `precio`, sin precio.
- `carta.platos` [{nombre, texto, precio, categoria, destacado}]: se agrupan por `categoria` en el orden en que aparecen (con más de una, índice arriba). `precio` SIEMPRE como cadena (`"9,50 €"`); vacío = sin puntos ni precio. `destacado: true` pone la marca (`carta.marca_destacado`, por defecto «Recomendado»).
- `carta.menu_dia` {titulo, precio, texto}: el menú del día; `texto` con una línea por cosa (`|` en YAML). Sin `titulo` ni `texto`, no aparece. `carta.imagen`: foto junto al menú (sin menú, franja panorámica).
- `galeria`: `galeria` (6 fotos llenan el mosaico; cualquier número vale) y `cta` (sin él, el botón va a `redes.instagram`).
- `reservas`: `imagen`, `items` (pasos), `cta` (normalmente WhatsApp; sin él, el WhatsApp o el teléfono de contacto) y `nota`. El formulario de reserva (día, hora, personas) sale siempre.
- `horario-ubicacion`: `horario` [{dia, horas}] (sin él, `contacto.horario`; «Cerrado» sale apagado), `imagen` (fachada) y `mapa` (true = botón «Ver el mapa aquí»; el mapa no se carga hasta que se pulsa).
- `opiniones.testimonios` [{texto, autor, nota}]: `nota` opcional (de dónde viene). Sin opiniones, la sección no se pinta. Sin estrellas ni notas.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`. La cabecera solo va transparente si la primera sección es la portada con foto; si no, es sólida.
3. **Cambiar textos, platos, precios, horarios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas. Precios siempre entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Para agrupar platos usa `categoria`; para varios datos, una cadena. Máximo 24 elementos por lista.
5. **Nunca inventes** precios, cifras ni opiniones: si el cliente no los da, déjalos vacíos (los componentes lo soportan).
6. **Página nueva**: crea `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`, con bandas (`.banda .banda--oscura`…) como `src/pages/aviso-legal.astro`; enlázala en `site.yaml → menu`.
7. **Apartado nuevo**: añade `secciones.<id>` en `site.yaml` con `tipo:` = `texto`, `carta`, `especialidades`, `galeria`, `reservas`… (el diseño que quiera reutilizar). `src/pages/index.astro` lo recoge solo; no lo toques.
8. **No tocar** `src/pages/index.astro`, `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
9. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real (solo hay el de la cabecera y el del botón del mapa), bandas a todo el ancho, 16 px de margen lateral del texto, botones de 44 px de alto como mínimo, sin scroll horizontal en móvil. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""`.
10. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`; al publicar, la plataforma lo conecta a su servidor. No cambies el marcado de `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento)
- Esta plantilla no tiene listas con página propia (`src/data/fichas.ts` vacío: la carta son platos) ni páginas por zona.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas).

## Varias páginas
- `paginas:` (raíz de site.yaml, opcional): `[{ ruta, titulo, secciones: "carta" }]`, como mucho 6, cada sección en una sola página y nunca `hero`. Con ella la web pasa a Inicio (hero + lo que no esté en ninguna página) y una página por entrada (`/carta/`…); el menú se hace solo con las páginas (las entradas `/#…` de `menu` no salen) y los enlaces `/#id` del site.yaml se cambian solos por la dirección de su sección. Sin ella, una sola página larga. Una orden «haz la web de varias páginas» = escribir `paginas`; nunca crees páginas a mano para eso. Reparto recomendado en `template.yaml → paginas` (Carta, La casa, Reservas).
- No tocar `src/lib/multipagina.ts`, `src/pages/index.astro` ni `src/pages/[...pagina].astro` (comunes a todas las plantillas). En un componente, un enlace fijo a una sección va con `enlace('/#contacto')` (de `src/lib/multipagina.ts`).

# Restaurante moderno: brief de diseño

Plantilla `restaurante-moderno` creada el 06/11/2026 a partir de `cafeteria-brunch` con `php artisan plantillas:nueva`
y rediseñada entera (de la base solo queda la estructura técnica). Encargo de Roberto: «La plantilla que utilizas para
restaurantes no me termina de gustar. Crea otra más limpia, con ancho completo y más actual.» No sustituye a
`restaurante` (sigue en el catálogo); es la opción limpia y actual. Este fichero se queda en el repo: es lo que lee
quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: restaurantes de cocina de mercado, bistrós, gastrobares, arrocerías, asadores y cocina de autor.
  Su cliente entra para ver la carta, el menú del día, el horario y reservar.
- **Qué tiene que conseguir la web**: que apetezca en un segundo (foto grande) y reservar sin buscar: «Reservar mesa»
  en la cabecera, en la portada y en la barra fija del móvil (con «Llamar»); WhatsApp, teléfono o formulario.
- **Tono y estilo** (`estilo: limpio`): limpio, tranquilo y actual. Sí: webs editoriales de restaurante de hoy (mucho
  aire, foto a sangre, serif grande en peso normal, filetes finos). No: la elegancia oscura y ornamentada de
  `restaurante`, la cartelería cálida de `cafeteria-brunch` ni las cajas centradas estrechas con tarjetas.
- **Ancho completo**: todas las secciones son bandas de borde a borde; fotos a sangre en la portada (pantalla entera),
  en las mitades 50/50, en las especialidades y en el mosaico; contenido hasta 96 rem con 16 px de margen en móvil.

## Concepto visual

- **Paleta de ejemplo**: primario `#1f2b25` (verde tinta: bandas oscuras y contacto), acento `#b5472f` (terracota:
  botones, menú del día, detalles), fondo `#f6f3ed` (hueso), texto `#1b1d1a`. Derivados con `color-mix`: `--oscuro`
  (pie y barra del móvil), `--claro`, `--hueso`, `--linea`, `--tenue` y `--acento-legible`.
- **Colores del cliente**: el texto sobre el primario, el oscuro y el acento se elige solo (blanco roto o casi negro
  según lo claro que sea el color, con «color relativo» `oklch(from …)` dentro de `@supports`; sin soporte, blanco).
  El acento usado como texto sobre fondo claro nunca pasa de un tono medio. Probado con primario y acento claros.
- **Tipografía** del sistema, sin descargas: serif de titulares en peso normal (`Sitka Banner`, `Iowan Old Style`,
  `Palatino Linotype`, Georgia…) a gran tamaño y con interletra cerrada; sans del sistema para el texto; antetítulos en
  versalitas espaciadas con una raya fina.
- **Forma**: botones píldora, filetes de 1 px, números «01 02 03» en serif del color de acento, puntos guía hasta el
  precio en la carta. Nada de sombras salvo la de la cabecera al bajar.
- **Ritmo de bandas**: portada a sangre → la casa (foto | texto) → especialidades (banda oscura + fotos a sangre) →
  carta (menú del día foto | acento y platos por categorías) → mosaico de fotos → reservas (foto | formulario) →
  horario (texto | fachada con mapa) → opiniones → preguntas → contacto (oscuro | formulario) → pie oscuro.

## Apartados (en orden)

1. `hero`: foto a pantalla entera con degradado; antetítulo, título enorme, párrafo, dos botones y una línea con los
   `items` (detalles cortos). La cabecera va transparente encima hasta que se baja (CSS `:has`).
2. `sobre` («La casa»): foto a sangre a la izquierda; `declaracion` en cursiva con filete de acento, párrafos e
   `items` numerados.
3. `especialidades`: banda oscura y `platos` [{nombre, texto, precio, imagen}] como fotos a sangre con el nombre encima.
4. `carta`: `menu_dia` sobre el acento junto a la foto (`imagen`), índice de categorías fijo al bajar y `platos`
   [{nombre, texto, precio, categoria, destacado}] en dos columnas; el precio solo sale si viene.
5. `galeria` («Fotos»): mosaico a sangre, la primera foto doble; sin huecos en la última fila.
6. `reservas`: foto a sangre, pasos, WhatsApp/teléfono, `nota` y formulario de reserva (día, hora, personas).
7. `horario-ubicacion`: horario con filetes, dirección, «Cómo llegar»; a la derecha la fachada (o un plano dibujado) y,
   con `mapa: true`, «Ver el mapa aquí», que carga Google Maps solo al pulsarlo.
8. `opiniones`: cita grande y el resto en columnas (desmarcada por defecto en la plataforma).
9. `preguntas`: título a la izquierda y acordeón a la derecha.
10. `contacto`: partido a sangre (vías en el primario | formulario en claro).

## Fotos (`fotos.json`, 14)

Generadas con IA (Gemini 2.5 Flash Image) y recortadas a su hueco: comedor contemporáneo en un casco antiguo (portada),
cocina abierta con brasa, mesa cenital para compartir, arroz meloso, lubina a la brasa, torrija, barra de terrazo, ensalada
de tomates, terraza, parrilla con brochetas y solomillo, pan y aceite, tarta de queso, mesa para dos con vela y fachada a
la hora azul. Luz cálida natural, roble claro y cerámica mate, sin texto legible, sin logotipos, sin personas
reconocibles y sin cabezas de animales. Revisadas una a una.

## Qué no hacer

- Volver a la caja centrada estrecha, al hero oscuro ornamentado de `restaurante` o a la tipografía redondeada de
  `cafeteria-brunch`.
- Fuentes externas, dependencias nuevas o JavaScript más allá del de la cabecera y el botón del mapa.
- Precios, cifras u opiniones fijos en los componentes: todo sale de `site.yaml` y los componentes pintan bien vacíos.
- Cargar el mapa de Google sin que el visitante lo pida (cookies de terceros).

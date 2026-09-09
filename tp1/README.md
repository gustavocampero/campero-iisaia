# TP 1 — Selector de fecha de nacimiento Bad UI

Un formulario para crear una cuenta donde nombre y apellido se completan normalmente, pero elegir la fecha de nacimiento exige recorrer un slider de 3001 años, llegar al día mediante saltos y embocar una pelota en el recipiente del mes correcto. Funciona bien y usarlo es incómodo, que era la idea.

## Cómo se ejecuta

Doble click en `index.html`. Es un solo archivo HTML, sin dependencias ni instalación.

## Qué me propuse construir

Una Bad UI concentrada en una tarea cotidiana: ingresar una fecha de nacimiento. El resto del registro tenía que comportarse como un formulario convencional para que la dificultad no viniera de una página caótica, sino de tres controles deliberadamente inadecuados para elegir día, mes y año.

El resultado salió en siete prompts dentro de una sola conversación de OpenCode. Cada iteración conservó lo que ya funcionaba y corrigió una parte concreta del selector.

## Decisiones que tomé yo

**La fecha es la única parte hostil.** Nombre y apellido usan inputs de texto normales. Envolver el selector dentro de una creación de cuenta hace que la incomodidad interrumpa una tarea reconocible, en vez de presentar una demostración aislada que nadie necesita completar.

**El día se alcanza con saltos de 2 y 5.** No hay calendario ni input numérico: solo botones `-5`, `-2`, `+2` y `+5`. Como ambos incrementos son coprimos, todos los días entre 1 y 31 siguen siendo alcanzables, aunque llegar al valor exacto requiera pensar una secuencia.

**El mes se elige con puntería.** Los 12 meses son recipientes alineados en una sola fila. Para seleccionar uno hay que arrastrar la pelota hacia atrás, definir fuerza y dirección al mismo tiempo y soltarla. La trayectoria usa velocidad, gravedad y colisiones; no es una animación con destino prefijado.

**La pelota y los recipientes están en el DOM.** No usé `<canvas>` ni una librería de física. La posición y velocidad viven en JavaScript, pero la pelota y cada recipiente siguen siendo elementos inspeccionables posicionados con CSS. La simulación se actualiza con `requestAnimationFrame`.

**Los bordes rebotan, no deciden.** Golpear una pared lateral o inferior invierte únicamente la componente de velocidad correspondiente y pierde energía mediante un coeficiente de restitución. Un impacto no selecciona un mes ni termina el intento: el mes se confirma solo cuando el centro de la pelota entra en el interior del recipiente.

**El año conserva los 3001 valores.** El rango va de 0 a 3000 con `step="1"`. Para que cada año tenga una posición física seleccionable con mouse, la pista mide 6400 píxeles y se recorre horizontalmente dentro de su tarjeta. Sigue siendo una mala forma de ingresar un año, pero no descarta valores por falta de resolución.

**El formulario tiene dos estados.** En `formulario` se editan los datos y la fecha; en `confirmado` se oculta el formulario y se muestra el resumen. El submit no recarga la página y reutiliza directamente el estado existente del selector.

## Qué salió mal y cómo lo corregí

La primera versión resolvió toda la fecha, pero el mes era apenas una grilla de botones mezclados. Servía como Bad UI, aunque todavía no expresaba la idea de puntería que terminó definiendo el trabajo.

El primer pedido de convertir el mes en un juego tampoco fue suficientemente preciso. Había una pelota y 12 objetivos, pero los recipientes no estaban en una única fila y el lanzamiento no tenía una física parecida a Angry Birds. El siguiente prompt tuvo que especificar Pointer Events, vector de arrastre, velocidad inicial, gravedad y `requestAnimationFrame`.

La primera simulación física terminaba el lanzamiento apenas la pelota tocaba un borde. El resultado era técnicamente “ninguno”, pero visualmente la pelota parecía quedar congelada sobre el recipiente. Además, la potencia máxima no alcanzaba cómodamente hasta Diciembre. Lo corregí separando tres eventos distintos: entrada válida, impacto contra una pared y salida del área. También agregué rebote inelástico, corrección de penetración, enfriamiento entre colisiones y subpasos para evitar atravesar bordes a alta velocidad.

El slider corto del año tenía otro problema más serio que la incomodidad: 3001 valores compartían muy pocos píxeles y algunos años no podían seleccionarse de forma precisa con el mouse. La primera ampliación tampoco quedó contenida porque CSS Grid tomó el ancho de la pista como tamaño intrínseco de la tarjeta. La solución final fue una pista de 6400 píxeles dentro de un contenedor desplazable y una restricción de ancho en la sección.

Lo que mejor funcionó en los prompts fue pedir cambios acotados. Frases como “no modificar el selector del día” o “modificar únicamente la mecánica del mes” evitaron reescribir partes ya probadas mientras cambiaban la estructura, la física y finalmente la página anfitriona.

## Prompts

El registro completo de la conversación está en [prompts.md](prompts.md). Los prompts que más pesaron fueron el tercero, que convirtió la puntería en una simulación física concreta, y el cuarto, que separó correctamente rebotes, aciertos y lanzamientos fallidos.

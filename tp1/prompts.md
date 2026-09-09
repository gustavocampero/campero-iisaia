# Prompts — TP 1

El registro del proceso, en orden. Siete prompts en una sola conversación de OpenCode. El artefacto quedó terminado en el séptimo.

---

## 1 — Prompt inicial

```
Construí una interfaz para ingresar una fecha de nacimiento de forma deliberadamente incómoda, pero completamente funcional.

Estructura:

* <header> con el título "Ingrese su fecha de nacimiento" y una breve indicación para que el usuario complete día, mes y año.
* <main> con tres bloques:
  - Un bloque para el año con:
    - un <input type="range"> entre 1900 y 2100.
    - un texto que muestre el año seleccionado actualmente.
  - Un bloque para el mes con:
    - una grilla de 12 <button>, uno por cada mes.
    - los meses deben aparecer en un orden aleatorio cada vez que se carga la página.
    - el mes seleccionado debe quedar visualmente marcado.
  - Un bloque para el día con:
    - un número grande que muestre el día seleccionado.
    - cuatro <button>: "-5" y "-2" a la izquierda del número. "+2" y "+5" a la derecha.
* <footer> con:
  - un texto que muestre la fecha completa seleccionada hasta el momento.
  - la pregunta "¿Es correcta esta fecha?".
  - un <button> "Sí".
  - un <button> "No".
  - un espacio para mostrar el mensaje final de confirmación.

Estilo:

* Diseño simple y limpio, como si fuera un formulario normal.
* Fondo claro y tipografía sans-serif.
* Cada bloque del <main> debe estar visualmente separado.
* Los botones de los meses deben tener el mismo tamaño y distribuirse en una grilla.
* El mes seleccionado debe distinguirse del resto.
* El día seleccionado debe tener bastante protagonismo visual.
* No usar animaciones ni efectos visuales exagerados.
* La mala experiencia de usuario debe surgir de la forma de ingresar los datos, no de que la interfaz sea visualmente caótica.

Comportamiento:

* Estado:

  * año seleccionado.
  * mes seleccionado.
  * día seleccionado.
* El año se modifica únicamente usando el slider.
* Al cargar la página, los 12 meses se mezclan en un orden aleatorio.
* Al hacer click en un mes, ese mes pasa a ser el seleccionado.
* El día comienza en 1.
* Los botones "-5", "-2", "+2" y "+5" modifican el día seleccionado.
* El día siempre debe mantenerse entre 1 y 31.
* Si una operación intenta llevarlo por debajo de 1 o por encima de 31, no debe realizarse.
* La fecha completa del footer debe actualizarse automáticamente cada vez que cambia el año, mes o día.
* El botón "Sí" confirma la fecha y muestra un mensaje indicando cuál fue la fecha ingresada.
* El botón "No" no borra nada y permite seguir modificando la fecha.
* No agregar comportamientos molestos adicionales como botones que se mueven, delays, elementos que cambian de posición o confirmaciones extra.

Constraints:

* Un solo archivo HTML, con el CSS en un <style> y el JS en un <script>.
* Vanilla JS, sin frameworks ni dependencias externas.
* Usar elementos HTML estándar.
* No usar <canvas>.
* Todo el estado y la interacción deben resolverse en el DOM.
```

**Qué intentaba lograr:** generar la primera versión completa del selector de fecha de nacimiento Bad UI en un único HTML, definiendo desde el principio la estructura semántica, el estilo visual, el comportamiento de cada selector y las restricciones técnicas del trabajo.

**Qué devolvió:** una interfaz funcional con un slider para elegir el año entre 1900 y 2100, los 12 meses como botones ordenados aleatoriamente, y un selector de día controlado únicamente mediante los botones -5, -2, +2 y +5. También agregó un resumen de la fecha seleccionada y los botones de confirmación. Respetó los constraints principales: un solo archivo HTML, Vanilla JS, sin dependencias externas y todo resuelto mediante elementos del DOM.

**Qué hice con eso:** lo acepté como primera versión. La estructura general y el comportamiento coincidían con la idea planteada, así que lo usé como base para continuar iterando sobre la experiencia Bad UI y ajustar detalles visuales o de interacción en los siguientes prompts.

---

## 2 — Convertir el mes en un juego de puntería

```
Modificá la versión actual del selector de fecha de nacimiento Bad UI manteniendo sin cambios el funcionamiento del día.

* Modificar la sección del año:
  * mantener un <input type="range">.
  * cambiar su rango para que vaya desde el año 0 hasta el año 3000.
  * mantener visible el año seleccionado actualmente.
* Reemplazar completamente la sección actual del mes por un juego de puntería:
  * un área horizontal de juego.
  * en el extremo izquierdo debe haber una pelota lista para lanzar.
  * en el lado derecho debe haber 12 contenedores, uno por cada mes del año.
  * cada contenedor debe estar identificado claramente con el nombre de un mes.
  * los 12 contenedores deben estar visibles al mismo tiempo.

Estilo:

* Hacer que el slider del año sea notablemente más corto que antes, para que seleccionar un valor exacto entre 0 y 3000 sea incómodo.
* El área del mes debe parecer un pequeño juego integrado dentro del formulario.
* La pelota debe distinguirse claramente de los contenedores.
* Los contenedores de los meses deben tener tamaño suficiente para que sea posible embocar la pelota, pero no tan grandes como para que resulte trivial.
* No agregar animaciones decorativas innecesarias ni efectos visuales que no estén relacionados con la mecánica.

Comportamiento:

* Año:
  * el slider debe permitir seleccionar únicamente valores enteros entre 0 y 3000.
  * el valor mostrado debe actualizarse en tiempo real al mover el slider.
* Mes:
  * el usuario debe seleccionar el mes lanzando la pelota desde el lado izquierdo hacia uno de los 12 contenedores.
  * el lanzamiento debe depender de la interacción del usuario, no ser completamente aleatorio.
  * permitir que el usuario apunte y defina la dirección o fuerza del lanzamiento mediante mouse o pointer events.
  * al lanzar, la pelota debe desplazarse desde su posición inicial hacia la derecha.
  * si la pelota entra o impacta correctamente en uno de los contenedores, ese mes pasa a ser el mes seleccionado.
  * si la pelota no entra en ningún contenedor, no se selecciona ningún mes.
  * después de cada lanzamiento, la pelota debe volver a su posición inicial para permitir otro intento.
  * indicar visualmente cuál es el mes seleccionado.
```

**Qué intentaba lograr:** modificar la primera versión manteniendo el selector del día, empeorando la precisión del selector de año al ampliar su rango de 0 a 3000 y reducir el tamaño del slider, y reemplazando la selección del mes por un pequeño juego de puntería en el que el usuario tuviera que lanzar una pelota hacia uno de 12 contenedores.

**Qué devolvió:** mantuvo correctamente el funcionamiento del día y modificó el slider del año como se pidió. Para el mes generó un área de juego con una pelota y 12 contenedores, pero la mecánica de lanzamiento y la disposición de los meses no quedaron como esperaba.

**Qué hice con eso:** mantuve los cambios del día y del año, pero decidí iterar nuevamente sobre el selector de mes. Los 12 contenedores tienen que estar alineados uno al lado del otro y el lanzamiento debe funcionar de forma similar a Angry Birds: el usuario arrastra la pelota desde su posición inicial para controlar simultáneamente la dirección y la fuerza, la suelta y la pelota sigue una trayectoria física hasta caer o impactar en uno de los contenedores. El mes solo debe seleccionarse si la pelota entra en su contenedor correspondiente.

---

## 3 — Implementar el lanzamiento tipo Angry Birds

```
Modificá únicamente la sección del mes de la versión actual. No cambies el selector del día, el selector del año, el header, el footer ni el resto de la interfaz.

Estructura:

* Dentro de esa sección debe haber un área de juego horizontal.
* En el extremo izquierdo del área debe estar la pelota en su posición inicial.
* En la parte inferior derecha del área deben estar los 12 contenedores de los meses.
* Los 12 contenedores deben estar alineados horizontalmente, uno al lado del otro, formando una única fila.
* Cada contenedor debe mostrar claramente el nombre o abreviatura del mes correspondiente, de Enero a Diciembre.
* Agregar un indicador visual sencillo que muestre cuál es el mes seleccionado actualmente.

Estilo:

* Mantener el estilo general existente.
* El área de juego debe tener espacio suficiente para que la pelota pueda describir una trayectoria antes de llegar a los contenedores.
* Los 12 contenedores deben tener el mismo ancho y alto.
* Los contenedores deben estar pegados o muy próximos entre sí, como una fila de recipientes.
* La pelota debe verse claramente y tener un tamaño proporcional al de los contenedores.
* No agregar botones extra para lanzar.
* No agregar controles separados de fuerza o dirección.

Comportamiento:

* El lanzamiento debe funcionar con una mecánica similar a Angry Birds.
* El usuario debe hacer click o pointer down sobre la pelota y arrastrarla hacia atrás desde su posición inicial.
* Mientras arrastra:

  * mostrar la pelota siguiendo el cursor dentro de un rango limitado.
  * usar la distancia de arrastre para determinar la fuerza del lanzamiento.
  * usar el ángulo del arrastre para determinar la dirección del lanzamiento.
* Al soltar la pelota:

  * calcular una velocidad inicial a partir del vector de arrastre, pero en sentido opuesto.
  * iniciar el movimiento de la pelota.
  * aplicar gravedad en cada actualización.
  * actualizar continuamente las posiciones horizontal y vertical.
  * la trayectoria debe ser parabólica y depender realmente de la dirección y fuerza elegidas por el usuario.
* Usar requestAnimationFrame para animar el movimiento.
* Detectar colisiones entre la pelota y los contenedores.
* El mes solo se selecciona cuando la pelota entra en el interior de uno de los contenedores.
* Si la pelota golpea un borde, pasa por encima o cae fuera de los contenedores, no se selecciona ningún mes.
* Una vez terminado el lanzamiento, esperar un momento breve y devolver la pelota a su posición inicial para permitir un nuevo intento.
* Si la pelota entra en un contenedor:

  * seleccionar ese mes.
  * actualizar el resumen de la fecha existente.
  * marcar visualmente el contenedor correspondiente.
  * luego devolver la pelota a la posición inicial.
* La pelota no debe poder volver a arrastrarse mientras está en movimiento.

Implementación:

* Guardar para la pelota:

  * posición x e y.
  * velocidad x e y.
  * estado de arrastre.
  * estado de lanzamiento.
* Calcular la fuerza según la distancia entre la posición inicial de la pelota y el punto hasta donde fue arrastrada.
* Limitar la distancia máxima de arrastre para evitar velocidades absurdas.
* Aplicar una gravedad constante durante el vuelo.
* Resolver las colisiones usando las posiciones y dimensiones reales de la pelota y los contenedores en el DOM.

Constraints:

* Modificar el mismo archivo HTML existente.
* Vanilla JS, sin frameworks ni dependencias externas.
* No usar librerías de física.
* No usar <canvas>.
* La pelota y los contenedores deben seguir siendo elementos del DOM posicionados con CSS.
* Usar Pointer Events para que el arrastre y el lanzamiento funcionen correctamente con mouse.
* No modificar ninguna otra parte de la aplicación que no sea necesaria para implementar correctamente esta mecánica.

```

**Qué intentaba lograr:** corregir únicamente la mecánica de selección del mes. La idea era que los 12 meses estuvieran alineados en una sola fila de contenedores y que la pelota se lanzara con una interacción similar a Angry Birds, donde el usuario controla dirección y fuerza arrastrando y soltando. Para eso utilize una sesion diferente para traducir la idea que tenia yo en un lenguaje mejorado para usar de prompt.

**Qué devolvió:** OpenCode reorganizó los 12 contenedores en una única fila e implementó el lanzamiento con Pointer Events, fuerza según la distancia de arrastre, velocidad inicial, gravedad, trayectoria parabólica mediante `requestAnimationFrame` y detección de colisiones con elementos del DOM.

**Qué hice con eso:** probé la mecánica y conservé la solución como nueva base. La interacción ya respondía a la dirección y fuerza elegidas por el usuario, pero detecté dos problemas: los impactos contra los bordes detenían el lanzamiento inmediatamente y la fuerza máxima no permitía llegar cómodamente hasta Diciembre.

---

## 4 — Corregir rebotes y alcance del lanzamiento

```
Modificá únicamente la mecánica del juego del mes en la versión actual. No cambies el selector del día, el selector del año, el header, el footer ni el resto de la interfaz.

Problemas actuales:

* Cuando la pelota impacta contra el borde superior o lateral de un contenedor, queda detenida ahí y el resultado termina siendo "ninguno".
* La fuerza máxima del lanzamiento no alcanza para llegar cómodamente hasta Diciembre.

Cambios requeridos:

Estructura:

* Mantener los 12 contenedores alineados horizontalmente, uno al lado del otro.
* Mantener la pelota y el área de juego actuales.
* No agregar controles nuevos ni cambiar la disposición general.

Estilo:

* Mantener el diseño actual.
* No cambiar tamaños ni posiciones salvo que sea estrictamente necesario para corregir la física.
* No agregar indicadores visuales extra para fuerza o dirección.

Comportamiento:

* Mantener la mecánica actual de arrastrar y soltar la pelota.
* Aumentar la fuerza máxima posible del lanzamiento para que sea posible:

  * llegar hasta el contenedor de Diciembre.
  * sobrepasar completamente Diciembre si el usuario aplica demasiada fuerza.
* La fuerza debe seguir dependiendo de la distancia de arrastre.
* Ajustar el multiplicador de velocidad o la distancia máxima de arrastre según sea necesario.

Colisiones con contenedores:

* No considerar automáticamente como fallo una colisión contra el borde de un contenedor.
* Si la pelota golpea el borde superior o lateral entre dos contenedores:

  * debe producirse un rebote pequeño.
  * reducir parte de la velocidad para simular pérdida de energía.
  * la pelota debe continuar moviéndose bajo el efecto de la gravedad.
  * permitir que después del rebote pueda caer dentro del contenedor que queda inmediatamente detrás según su trayectoria.
* No dejar la pelota congelada sobre los bordes.
* Un impacto contra un borde no debe seleccionar ningún mes por sí solo.
* El mes se selecciona únicamente cuando el centro de la pelota queda efectivamente dentro del área interior de un contenedor.

Rebote:

* Implementar un rebote leve, no perfectamente elástico.
* Al chocar:

  * invertir solo la componente de velocidad correspondiente al eje del impacto.
  * multiplicarla por un coeficiente de restitución menor que 1.
  * conservar parcialmente la velocidad restante para que la pelota siga avanzando.
* Evitar rebotes infinitos o vibraciones sobre los bordes.
* Si la velocidad queda demasiado baja, permitir que la gravedad termine haciendo caer la pelota.

Resultado "ninguno":

* Mostrar "ninguno" únicamente cuando el lanzamiento termina sin que la pelota haya entrado en ningún contenedor.
* Esto incluye:

  * caer antes del primer contenedor.
  * pasar por encima de todos.
  * pasar completamente a la derecha de Diciembre.
  * salir de los límites del área de juego.
* Si la pelota sobrepasa Diciembre, debe continuar su movimiento hasta salir del área antes de marcar "ninguno".
* No marcar "ninguno" inmediatamente después de una colisión con un borde.

Implementación:

* Mantener requestAnimationFrame para la simulación.
* Mantener posición x/y y velocidad x/y de la pelota.
* Incorporar una respuesta de colisión con coeficiente de restitución para los bordes.
* Separar claramente:

  * detección de impacto contra bordes.
  * detección de entrada válida dentro de un contenedor.
  * detección de fin de lanzamiento sin selección.
* Evitar que una misma colisión se procese muchas veces en frames consecutivos generando vibración.
* Si hace falta, desplazar ligeramente la pelota fuera del borde después de resolver la colisión.

Constraints:

* Modificar el mismo archivo HTML existente.
* Vanilla JS, sin frameworks ni librerías de física.
* No usar <canvas>.
* Mantener la pelota y los contenedores como elementos del DOM.
* No modificar ninguna parte de la aplicación que no sea necesaria para estos ajustes.
```

**Qué intentaba lograr:** solucionar dos fallas concretas de la primera versión física: que un roce con un recipiente no terminara inmediatamente el intento y que toda la fila, incluido Diciembre, quedara dentro del alcance útil del lanzamiento.

**Qué devolvió:** OpenCode aumentó la potencia máxima, separó la detección de entrada válida de la detección de impactos y agregó rebotes inelásticos con pérdida de energía. También incorporó corrección de penetración, un intervalo de enfriamiento para evitar vibraciones y subpasos de simulación para prevenir que la pelota atravesara bordes a alta velocidad.

**Qué hice con eso:** verifiqué lanzamientos que entraban en Diciembre, otros que lo sobrepasaban por completo y rebotes contra divisores. Conservé la mecánica corregida porque el resultado "ninguno" pasó a mostrarse únicamente al finalizar realmente un intento fallido.

---

## 5 — Darle resolución física al slider del año

```
Estructura:

* Mantener la sección actual del año con un `<input type="range">`.
* Mantener el rango entre 0 y 3000.
* Mantener visible el valor del año seleccionado.
* No modificar las secciones del mes ni del día.

Estilo:

* Aumentar el ancho del slider respecto de la versión actual.
* El slider debe seguir siendo más incómodo que un selector de fecha convencional, pero suficientemente grande como para que todos los años entre 0 y 3000 puedan seleccionarse con el mouse.
* Mantener el estilo visual general de la interfaz.
* No agregar inputs de texto, botones `+/-` ni otros métodos alternativos para elegir el año.

Comportamiento:

* El slider debe permitir seleccionar cualquier año entero entre 0 y 3000.
* El valor debe actualizarse en tiempo real mientras el usuario mueve el slider.
* La selección con mouse debe ser precisa y permitir llegar tanto al año 0 como al 3000.
* No cambiar el comportamiento actual del resto de la aplicación.

Implementación:

* Ajustar el ancho CSS del `<input type="range">` hasta que haya suficiente resolución física para seleccionar todos los valores.
* Mantener `min="0"`, `max="3000"` y `step="1"`.
* Verificar que no exista ningún redondeo, escalado CSS o lógica JavaScript que impida acceder a ciertos valores intermedios.
* Mantener la actualización del estado del año usando el evento actual del slider.
```

**Qué intentaba lograr:** conservar la incomodidad de recorrer 3001 valores con un slider, pero eliminar un problema técnico: una pista demasiado corta hacía que distintos años compartieran la misma posición física y algunos no pudieran elegirse con precisión usando el mouse.

**Qué devolvió:** OpenCode amplió la pista a 6400 píxeles dentro de un contenedor con desplazamiento horizontal. También limitó el ancho intrínseco de la sección para que la pista no ensanchara la página ni alterara la distribución del resto de la interfaz.

**Qué hice con eso:** comprobé con mouse los extremos 0 y 3000, los valores adyacentes 1 y 2999 y varios años intermedios. Acepté el cambio porque todos quedaron accesibles sin agregar una forma alternativa de entrada.

---

## 6 — Inicializar el año en 0

```
Estructura:

* Mantener la sección actual del año con el mismo `<input type="range">`.
* Mantener el rango entre 0 y 3000.
* Mantener visible el valor del año seleccionado.
* No modificar las secciones del mes ni del día.

Estilo:

* Mantener exactamente el tamaño y el estilo actual del slider.
* No cambiar la distribución visual de la interfaz.
* No agregar controles nuevos.

Comportamiento:

* Al cargar o recargar la página, el año seleccionado debe comenzar siempre en 0.
* El slider debe aparecer inicialmente posicionado en el extremo correspondiente al año 0.
* El texto que muestra el año seleccionado también debe mostrar 0 desde el inicio.
* Después de la carga, el usuario debe poder seguir seleccionando cualquier año entre 0 y 3000 normalmente.
* No conservar el valor seleccionado de una carga anterior.
* No cambiar ningún otro comportamiento de la aplicación.

Implementación:

* Inicializar el estado del año explícitamente en `0`.
* Asegurar que el `<input type="range">` tenga `value="0"` al iniciar.
* Si existe lógica JavaScript que asigna un valor inicial distinto, modificarla para que use 0.
* Al inicializar la interfaz, sincronizar el valor del slider, el estado interno y el texto mostrado para que los tres comiencen en 0.
```

**Qué intentaba lograr:** hacer que el selector de año tuviera un estado inicial consistente y empezara siempre en 0 al cargar o recargar la página.

**Qué devolvió:** OpenCode ajustó la inicialización del slider para que el valor inicial fuera 0 y sincronizó ese valor con el estado interno y con el texto visible del año seleccionado.

**Qué hice con eso:** acepté el cambio. El slider mantiene el rango de 0 a 3000 y su funcionamiento anterior, pero ahora siempre arranca en el extremo izquierdo con el año 0 seleccionado, sin conservar valores de una carga previa.

---

## 7 — Integrar el selector en un formulario de registro

```
Envolvé el selector de fecha de nacimiento actual dentro de un formulario para crear una cuenta de usuario.

Estructura:

* <header> con el título "Crear cuenta" y una breve descripción.
* <main> con un <form> que pida:
  - nombre, con un <input type="text"> normal.
  - apellido, con un <input type="text"> normal.
  - fecha de nacimiento, usando exactamente el selector Bad UI actual.
* El selector de fecha debe conservar sus tres partes:

  * día con los botones actuales.
  * mes con el juego de lanzamiento de pelota actual.
  * año con el slider actual de 0 a 3000.
* Al final del formulario, agregar un <button> "Crear cuenta".
* <footer> con un texto simple de ayuda o contacto.

Estilo:

* Hacer que toda la página parezca un formulario de registro convencional.
* Los campos de nombre y apellido deben verse normales, simples y fáciles de usar.
* Mantener el estilo actual del selector de fecha dentro del formulario.
* Integrar visualmente la sección de fecha con el resto del formulario sin cambiar su mecánica.
* No agregar nuevas molestias a los campos de nombre y apellido.
* La parte deliberadamente mala de la interfaz debe seguir siendo únicamente la selección de fecha de nacimiento.

Comportamiento:

* Agregar un estado `paso` con dos valores: `"formulario"` y `"confirmado"`.
* Arrancar en `"formulario"`.
* En `"formulario"` se muestran los campos de nombre, apellido y el selector completo de fecha de nacimiento.
* El usuario debe poder escribir nombre y apellido de forma normal.
* Mantener sin cambios toda la lógica actual del selector de fecha.
* Al enviar el formulario:

  * verificar que nombre y apellido no estén vacíos.
  * verificar que exista una fecha seleccionada válida según el estado actual del selector.
  * si falta algún dato, mantener el formulario visible y mostrar un mensaje simple.
  * si todos los datos están completos, cambiar `paso` a `"confirmado"`.
* En `"confirmado"` ocultar el formulario y mostrar un resumen con:

  * nombre.
  * apellido.
  * fecha de nacimiento seleccionada.
  * un mensaje indicando que la cuenta fue creada correctamente.
* No reiniciar ni modificar automáticamente la fecha mientras el usuario completa el formulario.

Implementación:

* Reutilizar el estado actual de día, mes y año.
* Agregar estado para nombre, apellido y `paso`.
* Mantener intacta la lógica interna del juego del mes, del selector del día y del slider del año.
* Interceptar el submit del <form> con JavaScript para evitar recargar la página.
* Usar los valores actuales del formulario y del selector de fecha para construir la vista de confirmación.
* No duplicar la lógica existente del selector de fecha: integrarla dentro del formulario actual.
```

**Qué intentaba lograr:** dejar de presentar el selector de fecha como una página aislada y convertirlo en una parte de un formulario más convencional. Elegí un registro de usuario para que nombre y apellido se completen de forma normal y el contraste con la selección de fecha Bad UI sea más evidente.

**Qué devolvió:** OpenCode integró el selector existente dentro de un formulario de creación de cuenta, agregó campos normales para nombre y apellido y mantuvo sin cambios la lógica del día, mes y año. También agregó un estado de flujo entre formulario y confirmación, validación básica de campos completos y una vista final con el nombre, apellido y fecha seleccionada.

**Qué hice con eso:** acepté el resultado como versión final del TP. La elección de fecha quedó integrada como una parte deliberadamente incómoda dentro de una tarea común y reconocible, mientras que el resto del formulario funciona de manera normal. Esto hace que la mala interfaz se concentre en un único problema y que el contraste sea más claro.

---

## Conversación completa

Una sola conversación de OpenCode, sin reiniciar el hilo. El artefacto final está contenido en un único archivo HTML con CSS y JavaScript embebidos. El artefacto final tiene 987 líneas en un archivo.

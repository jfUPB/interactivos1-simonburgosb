# ACTIVIDAD 4:
## ¿Por qué es útil enviar los datos como un objeto JSON en lugar de una cadena como "mouseX,mouseY"?
Enviar los datos como un objeto JSON es más claro y estructurado, permitiendo un acceso fácil y directo a los valores. Además, es más flexible, ya que se puede extender fácilmente con más propiedades en el futuro. También es un formato estándar y fácil de manejar en la mayoría de los lenguajes y plataformas.
## ¿Qué pasaría si quitaras la comprobación del threshold? ¿Cómo afectaría al rendimiento o la fluidez de la interacción?
Si se quitara la comprobación del threshold, se enviarían mensajes por cada pequeño movimiento, lo que saturaría la red, consumiría más recursos y podría generar latencia y retrasos en la experiencia de usuario, afectando negativamente el rendimiento y la fluidez de la interacción.
## ¿Cómo adaptarías este código si quisieras que también respondiera al clic del ratón en un computador (para pruebas)?
Para responder a clics del ratón, se puede usar mouseMoved() y mousePressed() de p5.js, que son funciones similares a las táctiles. mouseMoved() detecta el movimiento del ratón, y mousePressed() detecta el clic, permitiendo que el código funcione también en computadoras.
## ¿Por qué es importante usar JSON.parse() dentro de un bloque try…catch?
Usar try…catch asegura que el programa maneje posibles errores si la cadena JSON es incorrecta. Esto evita que el programa se detenga abruptamente y permite seguir ejecutándose incluso si hay errores al parsear los datos.
## Si los canvas del móvil y del escritorio tuvieran tamaños diferentes (ej: móvil 300x300, escritorio 600x600), ¿cómo modificarías el código del escritorio para que la posición del círculo rojo refleje proporcionalmente la posición del toque en el móvil?
Si los tamaños de los canvas son diferentes, se usa map() para ajustar las coordenadas del móvil a las del escritorio, asegurando que el toque se represente proporcionalmente en el canvas de escritorio.
## ¿Qué tendrías que cambiar en el código del escritorio si el servidor, en lugar de retransmitir el evento como ‘message’, lo enviara como ‘updateDesktop’?
Si el servidor cambia el nombre del evento, solo se necesita modificar el listener en el código del escritorio para escuchar el nuevo evento ('updateDesktop' en lugar de 'message') y seguir procesando los datos de la misma manera.
## Propósito de mobile/sketch.js y desktop/sketch.js:
* mobile/sketch.js: Captura los movimientos táctiles y envía las coordenadas del toque al servidor en formato JSON, utilizando un umbral de movimiento para evitar enviar datos innecesarios.
* desktop/sketch.js: Recibe las coordenadas del toque del servidor, las convierte de JSON a objeto y actualiza la posición de un círculo en el lienzo según esas coordenadas.
## Función touchMoved en móvil: 
Detecta el movimiento del dedo y, si supera un umbral de 5 píxeles o es el primer toque, crea un objeto con las coordenadas del toque, lo convierte a JSON con JSON.stringify y lo envía al servidor.
## Recepción en escritorio: 
El cliente de escritorio recibe el mensaje del servidor, convierte la cadena JSON a objeto con JSON.parse, y si el tipo es 'touch', actualiza la posición del círculo en el lienzo con las nuevas coordenadas del toque.

# Actividad 1

## Comunicación entre micro:bit y p5.js
El micro:bit y el sketch de p5.js se comunican mediante una conexión serial usando la biblioteca p5.webserial.js. El micro:bit envía datos de su acelerómetro y el estado de sus botones a través de uart.write(), y el código en p5.js lee esta información y la usa para dibujar en la pantalla.

Datos enviados por el micro:bit
El micro:bit transmite los siguientes valores a través de UART en una sola línea de texto, separados por comas:
1.	xValue: Valor del acelerómetro en el eje X.
2.	yValue: Valor del acelerómetro en el eje Y.
3.	aState: Estado del botón A (true o false).
4.	bState: Estado del botón B (true o false).


## Estructura del protocolo ASCII
El protocolo ASCII usado es simple: los valores se separan por comas y cada conjunto de datos termina con un salto de línea (\n). Esto facilita la lectura en p5.js, ya que se pueden dividir los valores con split(",") y convertirlos a números o booleanos.

### Formato general:
``` py
<xValue>,<yValue>,<aState>,<bState>\n
``` 
### Donde:
* <xValue> y <yValue> son enteros (valores del acelerómetro).
* <aState> y <bState> son valores booleanos (true o false).

## Lectura y transformación de los datos en p5.js
En p5.js, la comunicación serial ocurre en la función draw(). La lectura de datos sigue estos pasos:

1.	Verifica si hay datos disponibles en port.availableBytes().
2.	Lee una línea completa con port.readUntil("\n").
3.	Limpia los datos usando trim().
4.	Divide la línea en valores individuales con split(",").
5.	Convierte los valores a los tipos adecuados:
o	xValue y yValue se convierten a enteros.
o	aState y bState se convierten a booleanos (true o false).
6.	Transforma los valores del acelerómetro en coordenadas de la pantalla, centrando los valores en el windowWidth y windowHeight.

## Código relevante en draw():
``` js
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    } else {
      print("No se están recibiendo 4 datos del micro:bit");
    }
  }
}
```
Aquí, microBitX y microBitY se usan para posicionar elementos en la pantalla con base en los datos del acelerómetro.

## Eventos "A pressed" y "B released" en p5.js

Los eventos se generan comparando el estado actual de los botones con su estado anterior. Esto permite detectar cuando un botón ha sido presionado (pressed) o soltado (released).
* "A pressed": Se detecta cuando microBitAState cambia de false a true. Esto significa que el botón A acaba de ser presionado. En este momento:

  * Se genera un tamaño aleatorio para un nuevo dibujo.Se guardan las coordenadas actuales del micro:bit.
* "B released": Se detecta cuando microBitBState cambia de true a false. Esto significa que el botón B acaba de ser soltado. En este caso:
  * Se asigna un color aleatorio para el siguiente trazo.

## Código en updateButtonStates():
``` js
function updateButtonStates(newAState, newBState) {
  if (newAState === true && prevmicroBitAState === false) {
    lineModuleSize = random(50, 160);
    clickPosX = microBitX;
    clickPosY = microBitY;
    print("A pressed");
  }

  if (newBState === false && prevmicroBitBState === true) {
    c = color(random(255), random(255), random(255), random(80, 100));
    print("B released");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}
```

Esto garantiza que los eventos solo se activen cuando hay un cambio real en los estados de los botones.

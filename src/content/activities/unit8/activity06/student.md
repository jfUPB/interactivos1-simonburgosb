# ACTIVIDAD 6:
## Fragmentos clave de código - Cliente p5.js
### Estado y actualización desde Serial y Socket
``` js
let tiltX = 0, tiltY = 0;
let mobileTouch = { touchX: 0, touchY: 0 };
let colorFactor = 0;

function serialEvent() {
  let data = serial.readLine().trim();
  if (data && data.includes("tiltX")) {
    let parts = data.split(",");
    tiltX = parseInt(parts[0].split(":")[1]);
    tiltY = parseInt(parts[1].split(":")[1]);
  }
}

socket.on("mobileInputForwarded", (data) => {
  mobileTouch = data;
});
```
### Lógica principal del Process
``` js
function processInputs() {
  // Normaliza los valores
  let xMapped = map(tiltX, -90, 90, 0, width);
  let yMapped = map(tiltY, -90, 90, 0, height);
  let touchDist = dist(mobileTouch.touchX, mobileTouch.touchY, width / 2, height / 2);

  // Lógica: si el usuario gira mucho el micro:bit Y toca el centro => aumenta intensidad visual
  if (touchDist < 100 && abs(tiltX) > 30 && abs(tiltY) > 30) {
    colorFactor += 5;
  } else {
    colorFactor *= 0.98;
  }
  colorFactor = constrain(colorFactor, 0, 255);
}
``` 
### Output visual en draw()
``` js
function draw() {
  background(0);
  processInputs();

  // Fondo reactivo
  fill(0, colorFactor, colorFactor, 80);
  rect(0, 0, width, height);

  // Visualización del micro:bit
  fill(255);
  ellipse(map(tiltX, -90, 90, 0, width), map(tiltY, -90, 90, 0, height), 30);

  // Toque del móvil
  fill(255, 0, 0);
  ellipse(mobileTouch.touchX, mobileTouch.touchY, 20);
}
``` 

## Comportamiento final
### ¿Lograste implementar tu lógica?
Sí. El sketch combina de forma fluida:

* El micro:bit controla la posición de un punto blanco (tiltX/Y).
* El móvil, al tocar cerca del centro, activa efectos visuales si el micro:bit está girado (interacción combinada).
* El resultado es un canvas que "respira" con color turquesa según esa interacción.

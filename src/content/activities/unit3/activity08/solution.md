# Control remoto Micro:bit 

``` js
let port;
let connectBtn;

function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(32);
  
  port = createSerial();
  connectBtn = createButton('Connect to micro:bit');
  connectBtn.position(80, 350);
  connectBtn.mousePressed(connectBtnClick);
}

let tiempo = 20;
let estado = "CONFIG";
let seqDesac = ["A", "B", "A", "B"];
let seqPropia = [];
let lastFrameTime = 0;

function draw() {
  background(220);
  
  if (estado === "CONFIG") {
    text("CONFIGURACIÓN", width / 2, height / 2 - 50);
    text("Tiempo: " + tiempo, width / 2, height / 2);
  } else if (estado === "ARMADO") {
    text("ARMADO", width / 2, height / 2 - 50);
    text("Tiempo: " + tiempo, width / 2, height / 2);
    
    if (millis() - lastFrameTime >= 1000 && tiempo > 0) {
      tiempo--;
      lastFrameTime = millis();
    }
    if (tiempo <= 0) {
      estado = "EXPLOSION";
    }
  } else if (estado === "EXPLOSION") {
    text("💀 EXPLOSIÓN 💀", width / 2, height / 2);
  }

  if (!port.opened()) {
    connectBtn.html('Connect to micro:bit');
  } else {
    connectBtn.html('Disconnect');
  }
  serialEvent();
}

function manejarConfig(key) {
  if (key === 'A') {
    tiempo = min(60, tiempo + 1);
  } else if (key === 'B') {
    tiempo = max(10, tiempo - 1);
  } else if (key === 'S') {
    estado = "ARMADO";
    lastFrameTime = millis();
    seqPropia = [];
  }
}

function manejarArmado(key) {
  if (key === 'A' || key === 'B') {
    if (seqPropia.length >= 4) {
      seqPropia.shift(); 
    }
    seqPropia.push(key);
    
    if (seqPropia.length === seqDesac.length) {
      if (JSON.stringify(seqPropia) === JSON.stringify(seqDesac)) {
        estado = "CONFIG";
        tiempo = 20;
      }
    }
  }
}

function manejarExplosion(key) {
  if (key == 'T') {
    estado = "CONFIG";
    tiempo = 20;
  }
}

  function keyPressed() {
  if (estado == "CONFIG") {
    manejarConfig(key);
  } else if (estado == "ARMADO") {
    manejarArmado(key);
  } else if (estado == "EXPLOSION") {
    manejarExplosion(key);
  }
}



function serialEvent() {
  if(port.availableBytes() > 0){
    let data = port.read(1);
    if (data == 'A' && estado == "CONFIG") {
    tiempo = min(60, tiempo + 1);
  } else if (data == 'B' && estado == "CONFIG") {
    tiempo = max(10, tiempo - 1);
  } else if (data == 'S' && estado == "CONFIG") {
    estado = "ARMADO";
  } else if (estado == "ARMADO") {
    if (data == 'A' || data == 'B') {
    if (seqPropia.length >= 4) {
      seqPropia.shift(); // Elimina el primer elemento si ya hay 4
    }
    seqPropia.push(data);
    if (seqPropia.length === seqDesac.length) {
      if (JSON.stringify(seqPropia) === JSON.stringify(seqDesac)) {
        estado = "CONFIG";
        tiempo = 20;
      }
  }
  }
  } else if (data == 'T' && estado == "EXPLOSION") {
    estado = "CONFIG";
    tiempo = 20;
  }
}
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open('MicroPython', 115200);
  } else {
    port.close();
  }
}

```

``` py
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A')
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')
        sleep(500)
    if accelerometer.was_gesture('shake'):
        uart.write('S')
        sleep(500)
    if pin_logo.is_touched():
        uart.write('T')
        sleep(500)
```

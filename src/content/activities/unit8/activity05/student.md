# ACTIVIDAD 5:
## server.js (Servidor Node.js como puente simple)
``` js
const express = require("express");
const http = require("http");
const socket = require("socket.io");

const app = express();
const server = http.createServer(app);
const io = socket(server);

app.use(express.static("public"));

io.on("connection", (socket) => {
  console.log("Cliente conectado");

  socket.on("mobileInput", (data) => {
    console.log("Datos del móvil:", data);
    io.emit("mobileInputForwarded", data); // reenviar sin procesar
  });
});

server.listen(3000, () => {
  console.log("Servidor corriendo en http://localhost:3000");
});
```
## Código micro:bit 
``` py 
from microbit import *

while True:
    x = accelerometer.get_x()
    y = accelerometer.get_y()
    print("tiltX:{} , tiltY:{}".format(x, y))
    sleep(100)
``` 
## Cliente móvil – public/mobile/sketch.js
``` js
let socket;

function setup() {
  createCanvas(400, 400);
  socket = io(); // conecta automáticamente al servidor

  // Simulación: enviar posición de toque
  canvas.addEventListener("touchstart", (e) => {
    let touch = e.touches[0];
    let data = {
      touchX: touch.clientX,
      touchY: touch.clientY
    };
    socket.emit("mobileInput", data);
  });
}
``` 
## Cliente p5.js – public/desktop/sketch.js
``` js
let socket;
let serial;
let tiltX = 0, tiltY = 0;
let mobileTouch = null;

function setup() {
  createCanvas(600, 600);
  background(0);

  // Conexión Socket.IO
  socket = io();
  socket.on("mobileInputForwarded", (data) => {
    console.log("Datos del móvil recibidos:", data);
    mobileTouch = data;
  });

  // Web Serial
  serial = new p5.SerialPort();
  serial.on("data", serialEvent);
  serial.open("/dev/ttyUSB0"); // AJUSTAR el puerto si es necesario
}

function serialEvent() {
  let data = serial.readLine();
  if (data.length > 0) {
    console.log("Datos del micro:bit:", data);
    let parts = data.trim().split(",");
    tiltX = parseInt(parts[0].split(":")[1]);
    tiltY = parseInt(parts[1].split(":")[1]);
  }
}

function draw() {
  background(0);
  fill(255);
  text(`TiltX: ${tiltX}`, 10, 20);
  text(`TiltY: ${tiltY}`, 10, 40);
  if (mobileTouch) {
    text(`TouchX: ${mobileTouch.touchX}`, 10, 60);
    text(`TouchY: ${mobileTouch.touchY}`, 10, 80);
  }
}
```

Datos del micro:bit: tiltX:12,tiltY:-5
Datos del móvil recibidos: { touchX: 173, touchY: 392 }


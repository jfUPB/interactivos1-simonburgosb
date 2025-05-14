# ACTIVIDAD 4:
## Diagrama de Arquitectura Técnica
┌────────────┐        Serial (Web Serial API)        ┌────────────────────┐
│  Micro:bit │ ────────────────────────────────────> │ Cliente p5.js      │
└────────────┘                                        │ (Computador)      │
                                                     │ - Proceso (Process)│
┌────────────┐        Socket.IO (JSON)               │ - Salida (Output)  │
│   Móvil    │ ────────────────────────────────────> │                   │
└────────────┘                                        └────────────────────┘
       │                                                 ▲
       │                                                 │
       ▼                                                 │
┌────────────────┐   Socket.IO (JSON - retransmisión)    │
│ Servidor Node.js│──────────────────────────────────────┘
│  (Puente)      │
└────────────────┘
## Protocolos de Datos
### Micro:bit → Cliente p5.js (Serial)
* Formato: ASCII plano.
* Ejemplo de mensaje: "tiltX:23,tiltY:-15\n"
* Parseo: Separar por , y : para obtener valores numéricos.

### Móvil → Servidor Node.js (Socket.IO)
* Evento: "mobile-touch"
* Formato JSON

### Servidor Node.js → Cliente p5.js (Socket.IO)
* Evento retransmitido: "mobile-touch"
* Formato: El mismo JSON que recibió, sin modificaciones.Socket.IO


## server.js 
``` js
io.on("connection", socket => {
  socket.on("mobile-touch", data => {
    io.emit("mobile-touch", data); // retransmite sin procesar
  });
});
```
## sketch.js
``` js
// VARIABLES
let tiltX = 0, tiltY = 0;
let touchX = null, touchY = null;
let emotionalState = "neutral";

// SETUP
function setup() {
  createCanvas(600, 600);

  // Conexión Serial
  serial = new p5.SerialPort();
  serial.open("/dev/ttyUSB0");
  serial.on("data", serialEvent);

  // Conexión Socket.IO
  socket = io();
  socket.on("mobile-touch", handleMobileTouch);
}

// EVENTO SERIAL
function serialEvent() {
  let data = serial.readLine();
  let parts = data.split(",");
  tiltX = parseInt(parts[0].split(":")[1]);
  tiltY = parseInt(parts[1].split(":")[1]);
}

// EVENTO SOCKET.IO
function handleMobileTouch(data) {
  touchX = data.touchX;
  touchY = data.touchY;
}

// DIBUJO / PROCESO
function draw() {
  background(30);

  // Lógica del Proceso
  let intensity = dist(tiltX, tiltY, 0, 0);
  let disturbed = touchX !== null;
  
  if (intensity > 30) {
    emotionalState = "agitated";
  } else if (disturbed) {
    emotionalState = "alert";
  } else {
    emotionalState = "calm";
  }

  // Salida Visual
  drawCreature(emotionalState);
}

// Función de Visualización
function drawCreature(state) {
  noStroke();
  if (state === "calm") fill(0, 200, 255);
  else if (state === "alert") fill(255, 255, 0);
  else if (state === "agitated") fill(255, 50, 50);
  ellipse(width/2, height/2, 150);
}
``` 

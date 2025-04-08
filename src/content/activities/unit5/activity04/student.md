# Actividad 4

https://openprocessing.org/sketch/create  

``` js
let port;
let microBitConnected = false;
let microBitX = 100 / 2;
let microBitY = 100 / 2;
let serialBuffer = [];

function setup() {
  createCanvas(500, 500);
  background(100);

  port = createSerial();
  
  let connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(10, 10);
  connectBtn.mousePressed(() => {
    if (!port.opened()) {
      port.open("MicroPython", 115200);
    } else {
      port.close();
    }
  });
}

function draw() {
  background(100);

  if (!port.opened()) {
    microBitConnected = false;
  } else {
    microBitConnected = true;
    readSerialData();
  }

  fill(255);
  circle(microBitX, microBitY, 20);
}

function readSerialData() {
  let available = port.availableBytes();
  if (available > 0) {
    let newData = port.readBytes(available);
    serialBuffer = serialBuffer.concat(newData);
  }

  while (serialBuffer.length >= 8) {
    if (serialBuffer[0] !== 0xAA) {
      serialBuffer.shift(); // Eliminar bytes hasta encontrar el header
      continue;
    }

    if (serialBuffer.length < 8) break; // Esperar a que lleguen más bytes

    let packet = serialBuffer.slice(0, 8);
    serialBuffer.splice(0, 8); // Eliminar el paquete del buffer

    let dataBytes = packet.slice(1, 7);
    let receivedChecksum = packet[7];
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;

    if (computedChecksum !== receivedChecksum) {
      console.log("Checksum error");
      continue;
    }

    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0) + width / 2;
    microBitY = view.getInt16(2) + height / 2;
  }
}
```
https://editor.p5js.org/simonburgosb/sketches/fpaSYkEA2

https://drive.google.com/file/d/1AY1dUd8ErLFcl1mGLeNXJ2dio0QEy8N8/view?usp=drivesdk 

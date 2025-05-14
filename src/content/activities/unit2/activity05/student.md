# Lectura de puertos seriales

## Codigo

``` js
function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(130, 260);
    connectBtn.mousePressed(connectBtnClick);

    let sendBtn = createButton('Send happy');
    sendBtn.position(40, 300);
    sendBtn.mousePressed(() => sendData('h'));
    
    let sendBtn2 = createButton('Send duck');
    sendBtn2.position(135, 300);
    sendBtn2.mousePressed(() => sendData('w'));
    
    let sendBtn3 = createButton('Send no');
    sendBtn3.position(220, 300);
    sendBtn3.mousePressed(() => sendData('r'));
    
    let sendBtn4 = createButton('Send sad');
    sendBtn4.position(295, 300);
    sendBtn4.mousePressed(() => sendData('g'));
    
    fill('white');
    ellipse(width / 2, height / 2, 100, 100);
}

function draw() {
    if (port.availableBytes() > 0) {
        let dataRx = port.read(1);
        background(220);
        fill('black');
        textSize(32);
        textAlign(CENTER, CENTER);
        text(dataRx, width / 2, height / 2);
    }

    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    } else {
        connectBtn.html('Disconnect');
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

function sendData(char) {
    port.write(char);
}

```

``` py
from microbit import *
import utime

while True:
    if uart.any(): 
        data = uart.read(1) 
        if data:
            char = data.decode('utf-8')  
            display.show(char)  
            utime.sleep(1)
            display.clear()  
```

 ## Documentación del proceso:
  
 * Investigación: Se exploró el uso del puerto serial en micro:bit para recibir caracteres y mostrarlos en la pantalla LED.
 * Se realizo la función sendData para manejar diferentes caracteres de forma dinámica.
 * Se probó la recepción de datos y la visualización en la pantalla LED.
 * Se verificó que la conexión con micro:bit sea estable y que los datos se muestren correctamente.
 

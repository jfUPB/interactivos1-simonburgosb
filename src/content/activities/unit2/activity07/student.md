# Sonidos

``` js
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    let sendBtn = createButton('Send Sound A');
    sendBtn.position(220, 300);
    sendBtn.mousePressed(() => sendData('A'));
    let sendBtn2 = createButton('Send Sound B');
    sendBtn2.position(320, 300);
    sendBtn2.mousePressed(() => sendData('B'));
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
    connectBtn.html(port.opened() ? 'Disconnect' : 'Connect to micro:bit');
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
import music

while True:
    if uart.any():  # Verifica si hay datos en el buffer serial
        data = uart.read(1)  # Lee un carácter
        if data:
            char = data.decode('utf-8')  # Decodifica el carácter recibido
            if char == 'A':
                music.play(music.BA_DING)  # Reproduce un sonido
            elif char == 'B':
                music.play(music.POWER_UP)  # Reproduce otro sonido
            display.show(char)  # Muestra el carácter en la pantalla LED
            sleep(500)
            display.clear()
```

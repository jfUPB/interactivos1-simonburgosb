# Manipulando Entradas Digitales

## ¿Qué querías comprobar?

Queria comprobar que pasa cuando se leen los botones A, B y el boton virtual del logo. 

## ¿Cuál fue tu hipótesis?

Al hacer uso de botones estos son leidos por el puerto USB y dependiendo de la accion esta se realizara. 

## Los códigos involucrados en el experimento

``` py
from microbit import *

while True:
    if button_a.is_pressed():
        display.show("A")
    elif button_b.is_pressed():
        display.show("B")
    elif pin_logo.is_touched():
        display.show("L")  # L de "logo"
    else:
        display.clear()
```

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

    let sendBtn = createButton('Send Love');
    sendBtn.position(220, 300);
    sendBtn.mousePressed(sendBtnClick);

    fill('white');
    ellipse(width / 2, height / 2, 100, 100);
}

function draw() {
    if (port.availableBytes() > 0) {
        let dataRx = port.read(1);

        if (dataRx == 'A') {
            fill('red');  // Si se presiona el botón A
        } 
        else if (dataRx == 'B') {
            fill('yellow');  // Si se presiona el botón B
        } 
        else if (dataRx == 'L') {
            fill('blue');  // Si se toca el logo
        } 
        else {
            fill('green');  // Estado por defecto
        }

        background(220);
        ellipse(width / 2, height / 2, 100, 100);
        fill('black');
        textSize(20);
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

function sendBtnClick() {
    port.write('h');
}
```
## Descripción de los resultados

Cuando se presione el botón A, B o el logo, se mostrara un circulo en patalla y cambia de color

## Análisis de esos resultados

El MicroPython usa is_pressed() y pin_logo.is_touched() para detectar los eventos.

En p5.js, el micro:bit envía datos a la computadora a través de Bluetooth o un puerto serie, permitiendo actualizar la interfaz.

## Conclusiones

Es posible detectar los estados de los botones A, B y el logo del micro:bit tanto en el mismo dispositivo como en una computadora usando MicroPython y p5.js.

Esta técnica se puede utilizar en juegos, interfaces y proyectos interactivos.

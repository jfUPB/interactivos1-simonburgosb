# Codigo del programa 

Este moviemto se puede hacer posible gracias a que el programa lee la informacion ingresada por el puerto usb en primera posicion y segunda posicion las cuales son los botones a y b respectivamente para que depsues se llame a la funcion de trasladar el circulo. El codigo en micro:bit quedo igual al del profe. 

``` js
let port;
let connectBtn;

let x;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    fill('white');
    circle(50,50,50);
  
    x = 20
}

function draw() {

    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
        if(dataRx == 'A'){
            x = x+20
            translate(x, 0);
        }
        else if(dataRx == 'B'){
            x = x - 20
            translate(x, 0);
        }
      background(220);
      fill('white');
      circle(50,50,50);
    }


    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    }
    else {
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

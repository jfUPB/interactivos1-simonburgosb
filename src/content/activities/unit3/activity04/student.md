# Sketch p5.js

``` js
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(130, 260);
    connectBtn.mousePressed(connectBtnClick);
    
    let sendA = createButton('Send A');
    sendA.position(40, 300);
    sendA.mousePressed(() => port.write('A'));
    
    let sendB = createButton('Send B');
    sendB.position(135, 300);
    sendB.mousePressed(() => port.write('B'));
    
    let sendS = createButton('Send Shake');
    sendS.position(220, 300);
    sendS.mousePressed(() => port.write('S'));
    
    let sendT = createButton('Send Touch');
    sendT.position(320, 300);
    sendT.mousePressed(() => port.write('T'));
    
}

function draw() {
    

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
```

# ACTIVIDAD 5:
## Cambios en mobile/sketch.js
### ¿Qué datos se envían ahora?
* x, y: Coordenadas del toque.
* color: Color de la partícula como arreglo [r, g, b].
* useStroke: Booleano que indica si se usa stroke().
### ¿Cuándo y cómo se envían?
Se envían cada vez que el usuario mueve el dedo en pantalla, si supera cierto umbral para evitar saturar el servidor.

Fragmento clave: envío del mensaje

``` js
let touchData = {
  type: 'touch',
  x: mouseX,
  y: mouseY,
  color: hexToRGB(colorPicker.value()),
  useStroke: strokeCheckbox.checked()
};

socket.emit('message', JSON.stringify(touchData));
```
## Cambios en desktop/sketch.js
### ¿Cómo se reciben e interpretan los datos?
Se usa socket.on('message', ...) para recibir los datos. Se parsea el JSON, se verifica que sea de tipo 'touch', y luego se usan los datos para crear una partícula en la posición recibida, con el color y stroke definidos por el móvil.
### ¿Qué se modificó?
* Se agregó la recepción de color y useStroke.
* Se modificó la clase Particle para aceptar estos parámetros y usarlos en display().

Fragmento clave: recepción de datos
``` js
socket.on('message', (data) => {
  try {
    let parsedData = JSON.parse(data);
    if (parsedData && parsedData.type === 'touch') {
      let { x, y, color, useStroke } = parsedData;
      particles.push(new Particle(x, y, color, useStroke));
    }
  } catch (e) {
    console.error("Error parsing JSON:", e);
  }
});
```

Fragmento clave: modificación del constructor de la clase Particle

``` js
constructor(x, y, color = [150, 100, 255], useStroke = false) {
  this.pos = createVector(x, y);
  this.color = color;
  this.useStroke = useStroke;
  // ... otros atributos
}
```

Fragmento clave: uso de color y stroke en display()
``` js
if (this.useStroke) stroke(255);
else noStroke();


fill(this.color[0], this.color[1], this.color[2], this.lifespan);
ellipse(this.pos.x, this.pos.y, this.size);
```
## Cambios en server.js
No fue necesario cambiarlo si ya reenvía mensajes usando socket.broadcast.emit('message', data).
https://drive.google.com/file/d/1H8CphBJLeb8c5k5l3Ay1_eJhT0vIFrlj/view?usp=sharing 

## Server js: 
``` js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');

const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;

app.use(express.static('public'));

io.on('connection', (socket) => {
    console.log('New client connected');
    socket.on('message', (message) => {
        console.log(`Received message => ${message}`);
        socket.broadcast.emit('message', message);
    });

    socket.on('disconnect', () => {
        console.log('Client disconnected');
    });
});

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
```

## Sketch (desktop):
``` js
let socket;
let particles = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(0, 20);

  // Conectarse al servidor
  socket = io();

  socket.on('connect', () => {
    console.log('Connected to server');
  });

  // Recibe datos del móvil
  socket.on('message', (data) => {
    try {
      let parsedData = JSON.parse(data);
      if (parsedData.type === 'touch') {
        let { x, y, color, useStroke } = parsedData;
        particles.push(new Particle(x, y, color, useStroke));
      }
    } catch (e) {
      console.error('Error parsing JSON:', e);
    }
  });
}

function draw() {
  for (let i = particles.length - 1; i >= 0; i--) {
    particles[i].update();
    particles[i].display();
    if (particles[i].isDead()) {
      particles.splice(i, 1);
    }
  }

  if (particles.length === 0) background(0, 20);
}

class Particle {
  constructor(x, y, color = [150, 100, 255], useStroke = false) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.lifespan = 255;
    this.size = random(5, 20);
    this.noiseOffset = random(1000);
    this.color = color;
    this.useStroke = useStroke;
}

  update() {
    let angle = noise(this.pos.x * 0.005, this.pos.y * 0.005, this.noiseOffset) * TWO_PI * 2;
    let force = p5.Vector.fromAngle(angle);
    force.mult(0.5);
    this.vel.add(force);
    this.vel.limit(4);
    this.pos.add(this.vel);
    this.lifespan -= 3;
  }

  display() {
    if (this.useStroke) {
      stroke(255, this.lifespan);
    } else {
      noStroke();
    }
    fill(this.color[0], this.color[1], this.color[2], this.lifespan);
    ellipse(this.pos.x, this.pos.y, this.size);
  }

  isDead() {
    return this.lifespan < 0;
  }
}

function keyPressed() { 
  console.log(`particle size: ${particles.length}`);
}
```

## Sketch.js (Mobile)

``` js
let socket;
let particles = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(0, 20);

  // Conectarse al servidor
  socket = io();

  socket.on('connect', () => {
    console.log('Connected to server');
  });

  // Recibe datos del móvil
  socket.on('message', (data) => {
    try {
      let parsedData = JSON.parse(data);
      if (parsedData.type === 'touch') {
        let { x, y, color, useStroke } = parsedData;
        particles.push(new Particle(x, y, color, useStroke));
      }
    } catch (e) {
      console.error('Error parsing JSON:', e);
    }
  });
}

function draw() {
  for (let i = particles.length - 1; i >= 0; i--) {
    particles[i].update();
    particles[i].display();
    if (particles[i].isDead()) {
      particles.splice(i, 1);
    }
  }

  if (particles.length === 0) background(0, 20);
}

class Particle {
  constructor(x, y, color = [150, 100, 255], useStroke = false) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.lifespan = 255;
    this.size = random(5, 20);
    this.noiseOffset = random(1000);
    this.color = color;
    this.useStroke = useStroke;
}

  update() {
    let angle = noise(this.pos.x * 0.005, this.pos.y * 0.005, this.noiseOffset) * TWO_PI * 2;
    let force = p5.Vector.fromAngle(angle);
    force.mult(0.5);
    this.vel.add(force);
    this.vel.limit(4);
    this.pos.add(this.vel);
    this.lifespan -= 3;
  }

  display() {
    if (this.useStroke) {
      stroke(255, this.lifespan);
    } else {
      noStroke();
    }
    fill(this.color[0], this.color[1], this.color[2], this.lifespan);
    ellipse(this.pos.x, this.pos.y, this.size);
  }

  isDead() {
    return this.lifespan < 0;
  }
}

function keyPressed() { 
  console.log(`particle size: ${particles.length}`);
}
```

# Actividad 5

## server.js:
``` js
const express = require('express');
const app = express();
const http = require('http').createServer(app);
const io = require('socket.io')(http);
const path = require('path');

app.use(express.static('views'));

app.get('/page1', (req, res) => {
    res.sendFile(path.join(__dirname, 'views/page1.html'));
});

app.get('/page2', (req, res) => {
    res.sendFile(path.join(__dirname, 'views/page2.html'));
});

let scores = { player1: 0, player2: 0 };

io.on('connection', (socket) => {
    console.log('A user connected:', socket.id);

    socket.on('click', (player) => {
        scores[player]++;
        io.emit('scoreUpdate', scores);

        if (scores[player] >= 20) {
            io.emit('winner', player);
            scores = { player1: 0, player2: 0 };
        }
    });
});

http.listen(3000, () => {
    console.log('Server running on http://localhost:3000');
});
``` 

## page1.js y page2.js:
``` js
// Conexión al servidor
let socket = io();

function sendClick(){
    socket.emit("click", "player2");
}

socket.on('scoreUpdate', (scores) => {
    document.getElementById('scores').innerText = `P1: ${scores.player1} | P2: ${scores.player2}`;
});

socket.on('winner', (player) => {
    document.getElementById('winner').innerText = `El ganador es ${player}`;
});
```

## page1.html y page2.html:
``` html
<!DOCTYPE html>
<html>
<head>
    <title>Guerra de clicks</title>
</head>
<body>
    <h1>Player 1</h1>
    <button onclick="sendClick()">Enviar</button>
    <h2 id = "scores">Esperando datos</h2>
    <h2 id = "winner">...</h2>

    <script src="/socket.io/socket.io.js"></script>
    <script src="page1.js"></script> <!-- o page2.js según el caso -->
</body>
</html>

```

## Resumen de la modificación creativa:
Creé un juego simple llamado "ClickWar", donde dos jugadores compiten haciendo clic en sus pantallas. Cada jugador ve su propio puntaje y el del oponente en tiempo real, utilizando Node.js, Express y Socket.IO para la comunicación entre las páginas. Al alcanzar 20 clics, el juego se reinicia y muestra un mensaje de victoria.
## Reflexión sobre el proceso de modificación:
* Lo fácil: Fue sencillo implementar la lógica básica del conteo de clics y actualizar la interfaz en tiempo real con Socket.IO.
* Lo difícil: La sincronización entre los dos clientes, asegurando que ambos jugadores pudieran ver el puntaje del otro en tiempo real sin problemas de conexión o retrasos.
* Lo aprendido: Aprendí a gestionar la comunicación bidireccional entre los clientes y el servidor, usando eventos como socket.emit() y socket.broadcast.emit() para transmitir datos en tiempo real. También entendí mejor cómo manejar la lógica del juego en el servidor para asegurar que ambas partes tengan la misma información sincronizada.

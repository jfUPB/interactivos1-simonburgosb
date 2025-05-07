# ACTIVIDAD 6:
## Función del servidor Node.js: 
El servidor Node.js centraliza la comunicación entre los clientes, gestionando los datos y evitando que los clientes se comuniquen directamente entre sí.
## Diferencia entre socket.emit() y socket.broadcast.emit(): 
socket.emit() envía un mensaje solo al cliente que emite, mientras que socket.broadcast.emit() lo envía a todos los demás clientes, excepto al emisor.
## Comparación con comunicación serial:
* Ventaja de Node.js/Socket.IO: Comunicación bidireccional y en tiempo real.
* Desventaja de Node.js/Socket.IO: Requiere infraestructura y conexión a Internet.
* Ventaja de comunicación serial: Simplicidad y no depende de red.
* Desventaja de comunicación serial: Limitado a corto alcance y aplicaciones simples.
## Rol del protocolo HTTP y Socket.IO:
HTTP maneja las solicitudes iniciales del cliente, mientras que Socket.IO mantiene la conexión activa para la comunicación en tiempo real.
## Lo más sorprendente sobre la comunicación en red:
La simplicidad y eficiencia de Socket.IO para gestionar eventos en tiempo real entre múltiples clientes, sin necesidad de lidiar con las complejidades de WebSockets o protocolos más bajos.

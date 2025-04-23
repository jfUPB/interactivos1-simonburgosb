# ACTIVIDAD 1:
## ¿Por qué necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local del computador para que el celular se conecte?
* https://mc9pdc6g-3000.use2.devtunnels.ms/ 
Porque http://localhost:3000 solo funciona dentro del mismo dispositivo ( computador).
En cambio, la URL generada por Dev Tunnels es una dirección pública accesible desde cualquier dispositivo conectado a internet, como tu celular. Así garantizas que ambos (computador y celular) se puedan comunicar correctamente, sin importar la red.
## ¿Qué hace npm install y npm start?
* npm install:
Descarga e instala todas las dependencias del proyecto definidas en el archivo package.json, como express y socket.io.
Solo se necesita ejecutar una vez, al principio.
* npm start:
Esto inicia el servidor Node.js para que comience a aceptar conexiones.

## ¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?
Sí, se observan mensajes similares pero con diferentes identificadores de cliente.
New client connected
Received message => {"type":"touch","x":128.494140625,"y":326.802734375}
Client disconnected

## Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?
* Sí, funcionó la interacción correctamente: al mover el dedo en el celular, el círculo rojo en el navegador del computador se movía en tiempo real siguiendo el toque.
* Latencia: En general, la respuesta fue fluida, aunque no es tan instantánea
## ¿Cerraste el puerto? ¿Por qué es importante hacerlo?
Sí, cerré el puerto.
Es muy importante cerrar el puerto una vez terminas de hacer pruebas por tenemas de conexión y evitar mayor uso de los recursos del computador

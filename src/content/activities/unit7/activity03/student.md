# ACTIVIDAD 3: 
## Función de express.static('public') en el servidor
* Función: express.static('public') sirve para que el servidor pueda buscar archivos estáticos desde la carpeta public. Esto incluye archivos como HTML, CSS, imágenes y scripts. Cuando un navegador solicita un archivo, el servidor busca y responde con el archivo correspondiente desde la carpeta public.
* Comparación con app.get('/ruta', ...): En la Unidad 6, usamos app.get() para definir rutas específicas para cada archivo o conjunto de archivos, lo que requería más configuración manual.
## Flujo de un mensaje táctil
* Envío del mensaje desde el móvil: El evento que envía los datos del toque desde el móvil es touchMoved(). Dentro de esta función, se recopilan las coordenadas x y y del toque y se envían a través de Socket.IO como un mensaje.
* Recepción del mensaje en el servidor: El servidor escucha el evento 'message' con socket.on('message',).
* Acción del servidor: El servidor, tras recibir el mensaje, lo retransmite a todos los demás clientes conectados usando socket.broadcast.emit('message', message)..
* Envío del mensaje al escritorio: El servidor utiliza socket.broadcast.emit para enviar el mensaje a todos los demás clientes. Si un cliente móvil envía el mensaje, el servidor lo reenvía a los clientes de escritorio.
* Uso de socket.broadcast.emit: Se usa broadcast.emit en lugar de io.emit o socket.emit porque broadcast.emit envía el mensaje a todos los clientes menos al que lo envió. Usar socket.emit enviaría el mensaje solo al cliente que lo originó, mientras que io.emit enviaría el mensaje a todos los clientes, incluyendo al que lo envió.
## ¿Quién recibiría el mensaje retransmitido?
Los dos computadores de escritorio recibirían el mensaje retransmitido por el servidor. Esto se debe a que socket.broadcast.emit envía el mensaje a todos los demás clientes conectados, excluyendo al cliente que originó el mensaje..
## Mensajes console.log en el servidor
Los mensajes console.log proporcionan información valiosa sobre el estado de las conexiones y los eventos: Nuevo cliente conectado, Mensaje recibido y Cliente desconectado

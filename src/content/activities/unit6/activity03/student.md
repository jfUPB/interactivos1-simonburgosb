# ACTIVIDAD 3: 
## Pausa activa: ¿Por qué crees que es útil usar módulos o librerías en lugar de escribir todo desde cero? ¿Qué ventajas aporta?
Usar módulos o librerías como express, http, socket.io y path es útil porque nos ahorra tiempo, evita tener que escribir todo desde cero y nos permite trabajar con herramientas probadas, confiables y bien documentadas. Facilitan el desarrollo, hacen el código más limpio y mantenible, y garantizan compatibilidad entre sistemas operativos. Además, al ser ampliamente utilizadas, cuentan con una gran comunidad que ofrece soporte y recursos.
## Experimenta: ¿Qué ocurre cuando se cambia la carpeta de archivos estáticos a una que no existe?
Al cambiar la línea a app.use(express.static(path.join(__dirname, 'archivos_cliente'))); y luego iniciar el servidor, al intentar abrir http://localhost:3000/page1.html en el navegador, este muestra un error 404 (Not Found). Esto sucede porque la carpeta archivos_cliente no existe, por lo tanto, Express no encuentra los archivos que el navegador solicita. En la consola del navegador, también aparece un error indicando que no se pudo cargar el recurso solicitado. Al volver a cambiar la línea a 'views', todo funciona correctamente otra vez, ya que esa carpeta sí contiene los archivos estáticos. 
## Experimenta: ¿Qué pasa al cambiar la ruta del servidor?
Acceder a http://localhost:3000/page1 no funciona. El navegador muestra un error 404 (Not Found) porque esa ruta ya no está definida en el servidor.
Acceder a http://localhost:3000/pagina_uno sí funciona. El servidor responde correctamente con el archivo page1.html.
## Experimento: Observando la Conexión y Desconexión de Clientes con Socket.IO
### Abre http://localhost:3000/page1 en una pestaña:
* En la terminal del servidor, veo un mensaje similar a:
A user connected - ID: BT5F2CyEbUYD6ypRAAAB
### Abre http://localhost:3000/page2 en otra pestaña:
* En la terminal del servidor, veo otro mensaje similar, pero con un ID diferente:

A user connected - ID: xPU5OwouV64xD0RHAAAD

### Cierra la pestaña de page1:
* En la terminal del servidor, veo un mensaje que indica que el cliente se ha desconectado:

User disconnected - ID: BT5F2CyEbUYD6ypRAAAB 
### Cierra la pestaña de page2:
* Nuevamente, la terminal muestra un mensaje indicando que el cliente de esa pestaña también se ha desconectado:

User disconnected - ID: xPU5OwouV64xD0RHAAAD 


## Experimento: Observando de datos enviados

### Page 1: 
Data: { x: 100, y: 150, width: 200, height: 300 }
### Page 2: 
Received win2update from ID: 2n3gh92w10 Data: { x: 50, y: 75, width: 150, height: 250 }
### Prueba clave 
Cuando cambié el código de socket.broadcast.emit('getdata', page1); a socket.emit('getdata', page1); y reinicié el servidor, observé que, al mover la ventana de page1, no se actualizó la visualización en page2..

## Experimento: servidor
Detuve el servidor y cambié la variable port de 3000 a 3001, luego lo volví a iniciar. En la consola, vi el mensaje: Server is listening on http://localhost:3001, lo que me indicó que el servidor estaba escuchando correctamente en el nuevo puerto. Al intentar abrir http://localhost:3000/page1, no funcionó porque el servidor ya no está escuchando en el puerto 3000. Sin embargo, al abrir http://localhost:3001/page1, la página cargó sin problemas, ya que el servidor ahora está en ese puerto.
Lo que aprendí es que la función listen hace que el servidor se quede "escuchando" en el puerto que se le indique a través de la variable port. Cambiar el valor de esta variable cambia el puerto en el que el servidor espera las conexiones, por lo que es importante asegurarse de que estamos accediendo a la URL correcta correspondiente al puerto que el servidor está utilizando. Volví a restaurar el puerto a 3000 para seguir con el flujo original.

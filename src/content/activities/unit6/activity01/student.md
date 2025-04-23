# ACTIVIDAD 1:
## ¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?
Cuando ejecuté npm install, la terminal comenzó a descargar e instalar una serie de paquetes y dependencias necesarias para el funcionamiento del proyecto. 
El comando npm install sirve para instalar todas las dependencias definidas en el archivo package.json, que son necesarias para que el proyecto funcione correctamente. 
## ¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?
Después de ejecutar npm start, apareció el siguiente mensaje en la terminal:
Server listening on http://localhost:3000
User connected
Este mensaje indica que el servidor se ha iniciado correctamente y que ahora está esperando conexiones en el puerto 3000. 
## Describe lo que ves inicialmente en page1 y page2 en tu navegador
Al abrir http://localhost:3000/page1, vi una página con un fondo claro y un elemento visual (un círculo) que podía mover al mover la ventana. Tenía un diseño sencillo. 
En http://localhost:3000/page2, vi otra interfaz relacionada, parecía estar sincronizada con la primera. También mostraba elementos visuales que reflejaban el estado de la página 1, como la posición de la línea que conecta ambos circulos.
## ¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?
En la terminal del servidor se mostraron mensajes como:
Client connected
## Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador y en la terminal del servidor?
Cuando moví el elemento en la página page1, ese movimiento también cambia la dirección de la linea automáticamente en la página page2, y viceversa. Esto demuestra que ambas páginas están sincronizadas en tiempo real.
Consola del navegador (F12 → Consola):
Object
height: 671
width: 395
x: -16
y: 55
[[Prototype]]: Object

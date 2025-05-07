# ACTIVIDAD 2: 
## Pausa activa 1: Mi rampa de acceso a Internet
En mi casa me conecto a Internet usando Wi-Fi, que proviene de un módem conectado a través de un cable al proveedor de servicio. En la universidad, también uso Wi-Fi, aunque a veces me conecto con cable Ethernet cuando necesito una conexión más estable. 
Si se corta el Wi-Fi o se desconecta el cable, perdería el acceso a Internet. Eso significa que mi navegador no podría comunicarse con ningún servidor, así que no podría cargar páginas web, usar aplicaciones en línea, ni enviar ni recibir datos. Es como si mi vehículo quedara atrapado en el garaje sin salida a la carretera.
## Pausa activa 2: Relación Cliente-Servidor en la vida diaria
Un ejemplo claro fuera del mundo digital es un restaurante:
* Cliente: Yo, cuando voy al restaurante.
* Servidor: El camarero.
* Petición: “Quiero una hamburguesa con papas.”
* Respuesta: El camarero trae el plato con la comida solicitada.
## Pausa activa 3: Analizando una URL
Mi sitio favorito: https://www.youtube.com/watch?v=dQw4w9WgXcQ
* Protocolo: https://
* Nombre de dominio: www.youtube.com
* Ruta: /watch
* Parámetro: ?v=dQw4w9WgXcQ (especifica qué video ver)
## ¿Qué pasa si solo escribo el dominio?
Si solo pongo www.youtube.com, el servidor me envía una página por defecto, usualmente la página principal de YouTube.
## Pausa activa 4: Comparación HTTP vs protocolos seriales
*  Similitudes:
Ambos definen cómo debe estructurarse un mensaje para que el emisor y el receptor se entiendan. Ambos implican una secuencia: alguien envía, alguien recibe y responde.
* Diferencias:
HTTP es mucho más complejo, con tipo de contenido, métodos (GET), códigos de estado. Los protocolos seriales son más simples y cercanos al hardware. 
## ¿Por qué HTTP es más complejo?
Porque debe manejar muchísimos tipos de contenido, desde imágenes hasta formularios, pasando por autenticación, seguridad, etc. Y lo hace entre dispositivos que no se conocen, a través de Internet.
## Pausa activa 5: Analizando una página de login
### HTML:
* Los campos de usuario y contraseña.
* El botón de "Iniciar sesión".
* Los títulos y textos.
### CSS:
* El color de fondo.
* El tamaño y tipo de letra.
* El estilo del botón y sus bordes.
### JavaScript:
* Validación en tiempo real (“debes llenar este campo”).
* Mostrar errores sin recargar la página.
* Redirigir si el login es correcto.
## Pausa activa 7: Comparación entre bucle draw() y eventos
### Ventajas del modelo basado en eventos:
Mucho más eficiente, porque el código solo corre cuando es necesario (cuando hay interacción). Mejora el rendimiento y la batería en dispositivos móviles. Facilita el diseño modular y reutilizable.
### ¿Sería eficiente tener draw()?
No. Si nada ha cambiado, redibujar todo 60 veces por segundo sería un desperdicio de recursos. El modelo basado en eventos es mucho más apropiado para interfaces gráficas donde los cambios son esporádicos.
## Pausa activa 8: Usar JavaScript en cliente y servidor
Un solo lenguaje: Los desarrolladores no necesitan cambiar de mentalidad o de herramientas.
Reutilización de código: Algunas funciones pueden usarse en ambos lados.
Productividad: Equipos más pequeños pueden trabajar en toda la aplicación.
Velocidad de desarrollo: Menos configuración y más coherencia.
## Pausa activa final: HTTP vs WebSockets/Socket.IO
### HTTP:
Comunicación de ida y vuelta por cada petición. Ideal para páginas estáticas o interacciones simples.
### WebSockets / Socket.IO:
Conexión permanente bidireccional. Perfecto para aplicaciones en tiempo real: chats, videojuegos multijugador, colaboración en línea (como Google Docs).
### Aplicaciones con WebSockets:
Videojuegos online. Chats en tiempo real (WhatsApp Web, Messenger). Herramientas colaborativas (Miro, Figma, Google Docs). Seguimiento de entregas en vivo (Uber Eats, Rappi).

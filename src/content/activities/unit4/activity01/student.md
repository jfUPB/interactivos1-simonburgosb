# Actividad 1

## 1. https://p5js.org/examples/imported-media-image-transparency/  
Me gusto el uso de la imagen y el tema de transparencia. 

### Que funciones y técnica usa
* let img;
Declara una variable global para almacenar la imagen.
* preload()
Usa loadImage('/assets/moonwalk.jpg'); para cargar la imagen antes de que se ejecute el sketch.
* setup()
Define el tamaño del lienzo con createCanvas(720, 400);.
Usa describe() para proporcionar un mensaje. 
* draw()
Dibuja la imagen de fondo con image(img, 0, 0);.
* Usa tint(255, 127); para aplicar transparencia del 50% a la imagen superior.
Calcula un movimiento suavizado basado en la posición del mouse y dibuja la segunda imagen con image(img, offset, 0);.
 ### https://editor.p5js.org/simonburgosb/sketches/nqfpgwvB2 
* Cambios: Background(0), Creo un background negro para mejor superposición
* easing = 0.5, Le redusco la velocidad de movimiento de la imagen


## 2. https://editor.p5js.org/generative-design/sketches/P_1_0_01 
### Que funciones y técnica usa
* createCanvas(720, 720);
Crea un lienzo de 720x720 píxeles.
* noCursor();
Oculta el cursor del mouse para mejorar la estética interactiva.
* colorMode(HSB, 360, 100, 100);
Establece el modo de color en HSB (Hue, Saturation, Brightness) en lugar de RGB.
Permite una representación más intuitiva de los colores, ya que el tono (H) varía de 0 a 360.
* rectMode(CENTER);
Cambia el punto de referencia de los rectángulos al centro, en lugar de la esquina superior izquierda.
* noStroke();
Elimina los bordes de las formas.
* background(mouseY / 2, 100, 100);
Ajusta el color del fondo basándose en la posición del mouse en Y, haciendo que el tono (H) varíe de 0 a 360.
* fill(360 - mouseY / 2, 100, 100);
Ajusta el color del rectángulo para que sea complementario al fondo.
Si el fondo tiene H = 100, el rectángulo tendrá H = 260 (360 - 100).
* rect(360, 360, mouseX + 1, mouseX + 1);
Dibuja un rectángulo en el centro del lienzo.
Su tamaño es proporcional a mouseX, por lo que aumenta o disminuye según la posición del cursor.
* keyPressed()
Permite guardar la imagen si el usuario presiona "S".

### https://editor.p5js.org/simonburgosb/sketches/npfcWORvu 
* Agregué una variable global size
Esto permite que el tamaño del rectángulo cambie gradualmente en lugar de ajustarse instantáneamente con mouseX.
* Usé lerp() para suavizar la transición del tamaño
lerp(valorActual, valorObjetivo, factorSuavizado) interpola suavemente entre dos valores.
Esto hace que el rectángulo crezca y se reduzca de manera más fluida en lugar de cambiar bruscamente.

## 3. https://openprocessing.org/sketch/create 
### Que funciones y técnica usa
* createCanvas(windowWidth, windowHeight);
Crea un lienzo con el tamaño de la ventana del navegador, permitiendo una experiencia responsiva.
* background(100);
Establece un fondo gris (100 en escala de grises).
Se ejecuta solo en setup(), por lo que el fondo no se actualiza en draw(), dejando rastros de los círculos en la pantalla.
* circle(mouseX, mouseY, 20);
Dibuja un círculo de radio 20 píxeles en la posición del mouse (mouseX, mouseY).
Se ejecuta en cada cuadro (draw()), creando un efecto de "pintura" con círculos.

### https://editor.p5js.org/simonburgosb/sketches/BULxfvi9u 
* Agregué un fondo semitransparente (background(100, 10))
En lugar de un fondo sólido, ahora se dibuja con baja opacidad (10).
Esto crea un efecto de rastro: los círculos desaparecen gradualmente en lugar de quedarse fijos.
* Hice que cada círculo tenga un color aleatorio (fill(random(255), random(255), random(255)))
random(255) genera un valor aleatorio para rojo, verde y azul (RGB), haciendo que cada círculo tenga un color distinto.

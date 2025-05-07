# Actividad 3

## ¿Qué información se está enviando?
1.	xValue → Aceleración en el eje X (de -1024 a 1024 aprox.).
2.	yValue → Aceleración en el eje Y (de -1024 a 1024 aprox.).
3.	aState → Estado del botón A (True si está presionado, False si no).
4.	bState → Estado del botón B (True si está presionado, False si no).

## ¿Cómo se está enviando?
Se envía como texto a través de UART, en un formato de valores separados por comas con un salto de línea al final (\n).

## ¿Qué significa la parte del código?
*	{} son "espacios" que se llenan con los valores.
*	.format(xValue, yValue, aState, bState) coloca cada variable en su {} correspondiente.
*	\n al final es un salto de línea para separar cada conjunto de datos.

## ¿Por qué se separan los datos con comas y se termina con un salto de línea?
* Las comas (,) separan los valores para que sea fácil procesarlos luego con programas que lean puertos seriales.
* El salto de línea (\n) indica el fin de un conjunto de datos, facilitando su lectura.

## ¿Qué pasaría si no se separan los datos con comas y no terminan con un salto de línea?
* Sin comas, los números se juntarían, dificultando su separación.
* Sin \n, todos los datos se pegarían en una sola línea larga en Serial Terminal, sin saber dónde termina un grupo de valores.

## ¿Para qué se usa la función sleep(100)?
El sleep(100) pausa el código por 100 ms, limitando la frecuencia de envío a 10 Hz (10 veces por segundo).
* Si no se usara, el micro:bit enviaría datos lo más rápido posible, saturando el puerto serial con miles de líneas por segundo, haciéndolo ilegible.

## ¿Cómo cambian xValue y yValue cuando inclinamos el micro:bit?
* A la irquierda xValue es negativo y yValue es positivo
* A la derecha xValue es positivo y yValue es negativo
* Atras xValue es positivo y yValue es nagtivo
* Adelante xValue es negativo y yValue es positivo

## ¿Qué pasa si usamos was_pressed() en lugar de is_pressed()?
* is_pressed() devuelve True solo mientras el botón está presionado.
* was_pressed() devuelve True si el botón fue presionado en algún momento, aunque ya se haya soltado.

## Ejemplo si:
* xValue = 969
* yValue = 652
* aState = True
* bState = False

* El resultado será:
969,652,True,False

### En hex: 
39 36 39 2C 36 35 32 2C 54 72 75 65 2C 46 61 6C 73 65 0A

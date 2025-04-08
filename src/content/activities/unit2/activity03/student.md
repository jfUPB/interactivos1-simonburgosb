# Micro:bit y MicroPython

La micro:bit es una placa de desarrollo versátil que cuenta con diversas entradas y salidas que permiten la interacción con el entorno. A continuación, se detallan algunas de ellas:

## Entradas:
* Botones A y B: Dos botones físicos en la parte frontal de la placa que pueden ser presionados por el usuario para interactuar con programas.

* Pines de Entrada (P0, P1, P2): Pines que pueden leer señales analógicas o digitales, utilizados para conectar sensores externos o dispositivos de entrada.

* Acelerómetro: Sensor incorporado que detecta movimientos y la orientación de la placa en tres ejes.

* Micrófono: Disponible en la versión V2 de la micro:bit, permite captar sonidos del entorno.

## Salidas:
* Matriz de LEDs 5x5: Una pantalla de 25 LEDs que puede mostrar imágenes, texto y patrones.

* Pines de Salida (P0, P1, P2): Además de funcionar como entradas, estos pines pueden enviar señales para controlar actuadores como LEDs externos o motores.

* Zumbador: En la versión V2, la micro:bit incluye un zumbador integrado que puede generar sonidos.

* Comunicación por Radio y Bluetooth: Permite enviar y recibir datos de forma inalámbrica a otros dispositivos o micro:bits.


## Funciones para Entradas:

* Lectura de botones:
button_a.is_pressed() y button_b.is_pressed() devuelven True si el botón correspondiente está siendo presionado.

* Lectura de pines analógicos:
pin0.read_analog() lee el valor analógico del pin P0, retornando un valor entre 0 y 1023.
 
* Detección de gestos con el acelerómetro:
accelerometer.current_gesture() devuelve el gesto actual detectado, como "shake" (sacudida) o "face up" (cara arriba).

## Funciones para Salidas:

* Control de la matriz de LEDs:
display.show() muestra imágenes o texto en la matriz de LEDs.

* Escritura de valores analógicos en pines:
pin0.write_analog() escribe un valor analógico en el pin P0, permitiendo controlar la intensidad de un LED.

* Generación de sonidos con el zumbador:
music.play() reproduce una melodía utilizando el zumbador integrado o un altavoz conectado.

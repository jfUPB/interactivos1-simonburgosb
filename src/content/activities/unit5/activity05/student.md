# Actividad 5

![Texto alternativo](../../../../assets/act5_5.png)

## ¿Por qué fue necesario introducir framing en el protocolo binario?
El framing es necesario en el protocolo binario porque, a diferencia del formato de texto (donde los datos están separados por comas y terminan con un salto de línea), en un flujo binario no hay una separación clara entre paquetes de datos. Sin un sistema de delimitación, el receptor no podría identificar dónde empieza y termina cada mensaje.
Por esto, en la Unidad 2 se usa un byte especial de header (0xAA), que indica el inicio de un paquete de datos.

## 2. ¿Cómo funciona el framing?

El framing organiza los datos en paquetes con una estructura fija para que el receptor pueda leerlos correctamente. En nuestro protocolo binario, el framing funciona de la siguiente manera:
1.	Byte de inicio (header): 0xAA → Indica el comienzo de un paquete.
2.	Datos: Incluyen valores del acelerómetro (x, y), estados de los botones (A, B).
3.	Checksum: Un byte final que permite verificar si los datos llegaron correctamente.

## ¿Qué es un carácter de sincronización?
Un carácter de sincronización es un byte especial en la transmisión de datos que ayuda a identificar el inicio de un mensaje o paquete. En nuestro protocolo binario, el byte 0xAA cumple esta función.

## ¿Qué es el checksum y para qué sirve?
El checksum es un mecanismo de detección de errores que ayuda a verificar la integridad de los datos recibidos. En nuestro protocolo, se calcula sumando todos los bytes del paquete (excepto el header) y tomando el módulo 256.

# Explicacion maquina de estados 

El programa controla el parpadeo de dos píxeles en la matriz LED de un micro:bit utilizando una máquina de estados. Cada píxel tiene un intervalo de tiempo determinado para cambiar su estado (encendido o apagado).
## Identificación de Estados
Los estados representan momentos en los que el programa espera una condición antes de avanzar:
* "Init": Estado inicial, donde se configura el tiempo de inicio y se muestra el píxel.
* "WaitTimeout": Estado en el que el programa espera hasta que pase el tiempo especificado en interval.

## Identificación de Eventos
Los eventos son las condiciones que el programa evalúa en cada estado:
* Si state == "Init": Se inicializa el tiempo y se cambia a "WaitTimeout".
* Si state == "WaitTimeout" y el tiempo transcurrido (utime.ticks_diff(...)) supera interval: Se cambia el estado del píxel y se actualiza la pantalla.

## Identificación de Acciones
Las acciones son las ejecuciones que ocurren como respuesta a los eventos:
1.	Acción al iniciar ("Init")
* Se registra el tiempo de inicio.
* Se cambia el estado a "WaitTimeout".
* Se muestra el píxel en la pantalla LED.
2.	Acción al cumplirse el tiempo de espera ("WaitTimeout")
* Se reinicia el contador de tiempo.
* Se alterna el estado del píxel entre encendido y apagado.
* Se actualiza la pantalla LED.

# Explicacion de la maquina de estados para los botones

## Explicación de concurrencia en el programa

Este programa logra realizar varias acciones de manera concurrente gracias al uso de una máquina de estados y la función utime.ticks_ms(), que permite medir el tiempo transcurrido. La estructura de máquina de estados permite simular concurrencia al alternar entre distintos estados de forma secuencial, pero con temporización distinta para cada uno.

Cada ciclo de while True: evalúa el estado actual y decide si debe cambiar al siguiente con base en el tiempo transcurrido o si se ha detectado una pulsación del botón A. Esto permite manejar cambios de estado independientes de manera eficiente, simulando un comportamiento concurrente.

## Vectores de prueba
1. Vector de prueba 1: Cambio de estado por temporización
* Condiciones iniciales: El sistema está en STATE_HAPPY y muestra la imagen Image.HAPPY.
* Evento: Esperar 1500 ms sin presionar botones.
* Resultado esperado: El sistema cambia a STATE_SMILE y muestra Image.SMILE.
* Resultado obtenido: La imagen cambia correctamente.
2. Vector de prueba 2: Cambio de estado por botón en STATE_HAPPY
* Condiciones iniciales: El sistema está en STATE_HAPPY.
* Evento: Se presiona el botón A antes de que transcurran los 1500 ms.
* Resultado esperado: El sistema cambia inmediatamente a STATE_SAD y muestra Image.SAD.
* Resultado obtenido: El cambio ocurre sin esperar el temporizador.
3. Vector de prueba 3: Secuencia completa de estados
* Condiciones iniciales: El sistema inicia en STATE_INIT.
* Evento: No se presiona ningún botón y se permite que el sistema cambie de estados según los temporizadores.
* Resultado esperado: El sistema sigue la secuencia STATE_HAPPY -> STATE_SMILE -> STATE_SAD -> STATE_HAPPY de manera continua.
* Resultado obtenido: La secuencia se cumple correctamente sin interrupciones.

Si alguno de estos vectores de prueba no da el resultado esperado, puede indicar un error en la lógica de la máquina de estados o en la gestión del tiempo en utime.ticks_diff().


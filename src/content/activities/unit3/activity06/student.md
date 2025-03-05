# Vectores de prueba

## Estado: CONFIGURACIÓN (STATE_CONFIG)
1.	Incrementar tiempo al presionar A [X]
2.	Disminuir tiempo al presionar B [X]
3.	Pasar a estado ARMADO al agitar el micro:bit [X]
4.	No cambiar estado al presionar el logo táctil [X]
5.	Incrementar tiempo al recibir 'A' por UART [X]
6.	Disminuir tiempo al recibir 'B' por UART [X]

## Estado: ARMADO (STATE_ARMED)
7.	Pasar a EXPLOSIÓN cuando el tiempo llegue a 0 [X]
8.	Añadir 'A' a la secuencia de desactivación al presionar A [X]
9.	Añadir 'B' a la secuencia de desactivación al presionar B [X]
10.	Desactivar la bomba al ingresar la secuencia correcta A-B-A-B [X]
11.	Mantener el estado ARMADO si la secuencia de desactivación es incorrecta [X]
12.	Añadir caracteres a la secuencia al recibir 'A' o 'B' por UART [X]

## Estado: EXPLOSIÓN (STATE_EXPLOSION)
13.	Reiniciar el juego al presionar el logo táctil [X]
14.	No responder a A o B en estado EXPLOSIÓN [X]
15.	No responder a agitación en estado EXPLOSIÓN [X]

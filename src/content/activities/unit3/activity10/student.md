# Consolidacion

## ¿Por qué la técnica de máquina de estados es poderosa para la escalabilidad en términos de concurrencia y manejo de eventos?
* Manejo estructurado de eventos:
La máquina de estados permite gestionar eventos de manera clara y ordenada, asegurando que cada evento solo afecte el estado correspondiente. Esto evita condiciones de carrera y comportamientos inesperados.
* Facilita la concurrencia:
Al separar la lógica en estados bien definidos, diferentes partes del programa pueden ejecutarse en paralelo sin interferencias. Por ejemplo, en nuestra aplicación, el micro:bit y p5.js manejan eventos simultáneamente sin problemas.
* Escalabilidad sencilla:
Si queremos agregar nuevos estados o eventos, solo debemos extender la lógica sin modificar los estados existentes. Por ejemplo, podríamos agregar un estado de cuenta regresiva pausada sin afectar la lógica de armado o explosión.
* Claridad en la ejecución del programa:
Cada estado tiene reglas bien definidas sobre qué eventos pueden cambiarlo. Esto hace que el código sea fácil de entender, mantener y depurar.

## Ventajas y desventajas del tipo de pruebas realizadas en esta unidad
### Ventajas:
* Detección temprana de errores: Probar cada estado y cada evento permite encontrar fallos antes de integrar la aplicación.
* Cobertura completa: Consideramos eventos tanto desde p5.js como desde micro:bit, garantizando que toda la comunicación funciona correctamente.
* Pruebas sistemáticas: Definir los vectores de prueba nos permite verificar que el sistema se comporte correctamente en cada estado.

### Desventajas:
* No prueba errores inesperados: Si un evento no está en los casos de prueba, puede provocar fallos no detectados.
* Tiempo de ejecución: Al hacer pruebas de regresión después de cada cambio, la verificación puede ser lenta si hay muchos casos.

## ¿Por qué son importantes las pruebas de regresión?
* Cuando modificamos la aplicación, una pequeña alteración podría romper funcionalidades que antes funcionaban.
* Las pruebas de regresión nos permiten asegurarnos de que todo sigue funcionando correctamente después de un cambio.

## ¿Qué pasa si modificas tu aplicación y no haces pruebas de regresión?
* Pueden aparecer errores ocultos: Una modificación en un estado podría afectar otros sin darnos cuenta.
* Dificultad para depurar: Sin pruebas de regresión, encontrar la causa de un error se vuelve más difícil y costoso en tiempo.
* Menor confiabilidad: Si no validamos los cambios con pruebas, no podemos garantizar que la aplicación funcione correctamente en todas las condiciones.

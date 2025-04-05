# Correccion Codigo Bomba

## Vectores de Prueba
### Prueba 1: Ajuste del Tiempo con Botones
* Condición de prueba: Presionar el botón A para incrementar el tiempo y el botón B para disminuirlo.
* Entrada:
  * Presionar A varias veces.
  * Presionar B varias veces.
### Prueba 2: Activación por Movimiento
* Condición de prueba: Agitar la micro:bit para cambiar al estado ARMADO.
* Entrada: Agitar la micro:bit.
### Prueba 3: Cuenta Regresiva
* Condición de prueba: Observar la cuenta regresiva.
* Entrada: Permitir que el temporizador corra sin interrupciones.
### Prueba 4: Simulación de Explosión
* Condición de prueba: Verificar que al llegar a cero se muestre una imagen de calavera y suene la alarma.
* Entrada: Permitir que el tiempo llegue a 0.
### Prueba 5: Reinicio del Sistema
* Condición de prueba: Tocar el logo para reiniciar la bomba.
* Entrada: Tocar el logo de la micro:bit.
  
## Errores Encontrados y Correcciones Implementadas
1. Error: El sistema no permitía reajustar el tiempo en el estado de configuración después de la explosión.
* Causa: El display.clear() en el reinicio eliminaba la visualización del tiempo.
* Corrección: Se añadió una llamada a mostrar_tiempo(tiempo) después del reinicio.
2. Error: En algunos casos, el sonido de la explosión no se reproducía correctamente.
* Causa: music.play(music.WAWAWAWAA) se interrumpía si la ejecución se reiniciaba rápidamente.
* Corrección: Se añadió un utime.sleep(1) después de la explosión para asegurar la reproducción completa.

``` py
import utime
from microbit import *
import music


# Definición de estados
STATE_CONFIG = 0
STATE_ARMED = 1
STATE_EXPLOSION = 2

# Intervalos y configuración inicial
tiempo = 20  # Tiempo inicial en segundos
estado = STATE_CONFIG
start_time = 0
interval = 1000  # Intervalo de 1 segundo para la cuenta regresiva

# Configuración de botones
btn_up = button_a
btn_down = button_b
shake_sensor = accelerometer

def mostrar_tiempo(t):
    display.show(str(t) if t > 0 else "X")

def explotar():
    display.show(Image.SKULL)
    music.play(music.WAWAWAWAA)
    for _ in range(5):
        display.set_pixel(2, 2, 9)
        utime.sleep(0.2)
        display.clear()
        utime.sleep(0.2)
    utime.sleep(1)

def loop():
    global estado, tiempo, start_time, interval
    while True:
        if estado == STATE_CONFIG:
            mostrar_tiempo(tiempo)
            if btn_up.was_pressed():
                tiempo = min(60, tiempo + 1)
                utime.sleep(0.2)
            if btn_down.was_pressed():
                tiempo = max(10, tiempo - 1)
                utime.sleep(0.2)
            if shake_sensor.is_gesture("shake"):
                estado = STATE_ARMED
                start_time = utime.ticks_ms()
        elif estado == STATE_ARMED:
            if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
                start_time = utime.ticks_ms()
                tiempo -= 1
                mostrar_tiempo(tiempo)
            if tiempo <= 0:
                estado = STATE_EXPLOSION
                explotar()
        elif estado == STATE_EXPLOSION:
            if pin_logo.is_touched():
                estado = STATE_CONFIG
                tiempo = 20
                display.clear()
                mostrar_tiempo(tiempo)
                print("Reiniciando...")

loop()
```

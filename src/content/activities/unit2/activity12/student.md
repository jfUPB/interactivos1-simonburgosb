# Bomba Implementada

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
                print("Reiniciando...")

loop()
```

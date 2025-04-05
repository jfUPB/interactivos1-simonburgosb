# Bomba 3.0 

``` py
import utime
from microbit import *
import music

# Definición de estados
STATE_CONFIG = 0
STATE_ARMED = 1
STATE_EXPLOSION = 2

# Variables globales
tiempo = 20
estado = STATE_CONFIG
start_time = 0
interval = 1000

desactivacion_seq = ["A", "B", "A", "B"]
input_seq = []

# Variables de eventos
evento_ocurrido = False
evento_actual = ""


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

def tareaBomba():
    global estado, tiempo, start_time, input_seq, evento_ocurrido, evento_actual
    if estado == STATE_CONFIG:
        if evento_ocurrido:
            evento_ocurrido = False  # Consumir el evento
            if evento_actual == "A":
                tiempo = min(60, tiempo + 1)
                mostrar_tiempo(tiempo)
            elif evento_actual == "B":
                tiempo = max(10, tiempo - 1)
                mostrar_tiempo(tiempo)
            elif evento_actual == "S":
                estado = STATE_ARMED
                start_time = utime.ticks_ms()
                input_seq = []
            
    elif estado == STATE_ARMED:
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            start_time = utime.ticks_ms()
            tiempo -= 1
            mostrar_tiempo(tiempo)
            if tiempo <= 0:
                estado = STATE_EXPLOSION
                explotar()
        if evento_ocurrido: 
            evento_ocurrido = False
            if evento_actual=="A":
                input_seq.append("A")
            if evento_actual=="B":
                input_seq.append("B")
            if input_seq == desactivacion_seq:
                music.play(music.POWER_UP)
                input_seq = []
                tiempo = 20
                mostrar_tiempo(tiempo)
                estado = STATE_CONFIG 
        
        
                
        
    
    elif estado == STATE_EXPLOSION:
        if evento_ocurrido:
            evento_ocurrido = False  # Consumir el evento
            if evento_actual == "T": 
                estado = STATE_CONFIG
                tiempo = 20
                display.clear()
                print("Reiniciando...")
            

def tareaEventos():
    global evento_ocurrido, evento_actual
    if button_a.was_pressed():
        evento_ocurrido = True
        evento_actual = "A"
    elif button_b.was_pressed():
        evento_ocurrido = True
        evento_actual = "B"
    elif accelerometer.was_gesture("shake"):
        evento_ocurrido = True
        evento_actual = "S"
    elif pin_logo.is_touched():
        evento_ocurrido = True
        evento_actual = "T"
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('A'):
               evento_ocurrido = True
               evento_actual = "A" 
            elif data[0] == ord('B'):
               evento_ocurrido = True
               evento_actual = "B" 
            elif data[0] == ord('S'):
                evento_ocurrido = True
                evento_actual = "S" 
            elif data[0] == ord('T'):
                evento_ocurrido = True
                evento_actual = "T" 
mostrar_tiempo(tiempo)
while True:
    tareaBomba()
    tareaEventos()
```

En mi solucion lo que hze fue en la fucnion de tareaBomba incluir todos los eventos para los cmabios de estado ademas modifique el codigo para que en tare eventos
verifice si se propimieron los botones o se reciben datos desdes el serial para que asi con un bool se active el vento y se guarde el evento actual de la ccion correspondiente

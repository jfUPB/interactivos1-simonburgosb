# Semaforo 

``` py
from microbit import *
import utime

class Semaforo:
    def __init__(self, x, y, intervalos):
        self.estado = "Rojo"
        self.tiempo_inicio = utime.ticks_ms()
        self.intervalos = intervalos  # Diccionario con duración de cada estado
        self.x = x
        self.y = y
        self.actualizar_display()
    
    def actualizar_display(self):
        display.clear()
        if self.estado == "Rojo":
            display.set_pixel(self.x, self.y, 9)
        elif self.estado == "Amarillo":
            display.set_pixel(self.x, self.y + 1, 5)
        elif self.estado == "Verde":
            display.set_pixel(self.x, self.y + 2, 9)
    
    def actualizar(self):
        tiempo_actual = utime.ticks_ms()
        if utime.ticks_diff(tiempo_actual, self.tiempo_inicio) > self.intervalos[self.estado]:
            self.tiempo_inicio = tiempo_actual
            self.transicionar_estado()
            self.actualizar_display()
    
    def transicionar_estado(self):
        if self.estado == "Rojo":
            self.estado = "Verde"
        elif self.estado == "Verde":
            self.estado = "Amarillo"
        elif self.estado == "Amarillo":
            self.estado = "Rojo"

# Configuración del semáforo con tiempos de duración en cada estado
intervalos = {"Rojo": 3000, "Amarillo": 1000, "Verde": 3000}
semaforo = Semaforo(2, 0, intervalos)

while True:
    semaforo.actualizar()
    utime.sleep_ms(100)
```

## Explicacion

1. Estados:
* Rojo → Indica alto.
* Verde → Permite avanzar.
* Amarillo → Indica que cambiará a rojo.
2. Eventos evaluados en cada estado:
* Si ha pasado el tiempo definido para el estado actual, se cambia al siguiente estado.
3. Acciones ejecutadas en cada evento:
* Cambio de estado: Se actualiza el tiempo de inicio.
* Actualización del display: Se enciende un píxel en la posición correspondiente para representar el color del semáforo.

# ACTIVIDAD 3: 
## Brainstorming: 3 ideas exploradas
### Criatura emocional interactiva
#### Inputs:
* Micro:bit → inclinación = postura/emoción.
* Móvil → toques = estímulos externos.
#### Narrativa: 
Una criatura digital reacciona emocionalmente a su entorno físico y social.
#### Output: 
Su forma, color y comportamiento cambian en p5.js.
### Paisaje del ánimo
#### Inputs:
* Micro:bit → temperatura = estado ambiental.
* Móvil → acelerómetro = energía del usuario.
#### Narrativa: 
Un paisaje visual refleja el “ánimo” del entorno y del usuario.
#### Output: 
Transformaciones climáticas y visuales suaves o caóticas.
### Guardian del equilibrio
#### Inputs:
* Micro:bit → movimiento = desequilibrio.
* Móvil → botones = acciones correctivas.
#### Narrativa:
Mantener el equilibrio de un orbe flotante que reacciona al mundo físico y las decisiones del usuario.
#### Output: 
Movimiento, color, e inclinación del orbe en p5.js.

### Concepto I-P-O Final
#### Título provisional:
Criatura emocional digital

#### Narrativa/Concepto central:
Una criatura digital refleja su estado emocional en función del entorno (Micro:bit) y las interacciones del usuario (móvil). El objetivo no es controlarla, sino comprenderla a través de sus reacciones visuales.

#### Inputs específicos:
* Micro:bit	Inclinación	Representa el "estado corporal" de la criatura.
* Móvil	Toques / clics	Estímulos externos que afectan su estado.
* PC (p5.js)	Mouse/Teclado	Interacción opcional: observar o provocar reacciones visuales.

### Process (Lógica en p5.js):
#### Recepción de datos:
* Se conecta al Micro:bit por Serial para leer su inclinación.
* Se conecta al móvil por Socket.IO para recibir eventos de toque.
#### Lógica combinada:
Se define una variable de estado emocional (emotionalState) basada en:
* Inclinación → calma vs agitación.
* Frecuencia de toques → ansiedad o distracción.

Se aplican reglas para alterar:
* Color (estado de ánimo).
* Tamaño/movimiento (nivel de energía).
* Forma (estabilidad o distorsión).
#### Variables internas:
* emotionalState, touchIntensity, tiltX, tiltY, creatureEnergy.
* Estados se suavizan con interpolaciones para transiciones visuales fluidas.

### Output deseado (p5.js):
#### Una criatura animada en pantalla:
* Cambia de forma y color en tiempo real.
* Reacciona de manera fluida a la inclinación del Micro:bit y a los toques del móvil.
* Puede emitir sonidos suaves que reflejan su estado.

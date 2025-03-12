# Diagrama

## Estados de la bomba
La bomba tiene tres estados principales:
* CONFIG (Config): Se establece el tiempo inicial y se espera a que la bomba sea activada.
* ARMADO (Armado): La cuenta regresiva comienza y se pueden ingresar los códigos de desactivación.
* EXPLOSION (Explosión): La bomba "explota" si el tiempo llega a 0.

## Transiciones entre estados
Cada estado tiene condiciones específicas para cambiar a otro estado:

### De STATE_CONFIG a STATE_ARMED
* Se activa la bomba mediante un evento recibido (puede ser un "shake" o un comando serial).
* Se reinicia la secuencia de desactivación y comienza la cuenta regresiva.
  
### De STATE_ARMED a STATE_EXPLOSION
* Si el tiempo llega a 0, la bomba cambia al estado de explosión.
* Se muestra la imagen de una calavera y se reproduce un sonido de alerta.

### De STATE_ARMED a STATE_CONFIG (Desactivación exitosa)
* Si se ingresa correctamente la secuencia de desactivación (A, B, A, B), la bomba se desactiva y vuelve al estado de configuración.

### De STATE_EXPLOSION a STATE_CONFIG (Reinicio)
o	Si se detecta el toque en el logo del micro:bit o se ingesa 'T' por el puerto serial, la bomba se reinicia y vuelve al estado de configuración.

## Eventos y Acciones
Los eventos que controlan la bomba pueden venir de los botones del micro:bit, del sensor de movimiento (shake) o de la terminal serial:

### Eventos de entrada en STATE_CONFIG
* Botón A o comando serial 'A' aumenta el tiempo (máximo 60s).
* Botón B o comando serial 'B' disminuye el tiempo (mínimo 10s).
* Evento "shake" o comando serial de activación cambia el estado a STATE_ARMED.

### Eventos de entrada en STATE_ARMED
* Botón A/B o comando serial correspondiente agrega la entrada a la secuencia de desactivación.
* Si la secuencia coincide con ["A", "B", "A", "B"], la bomba se desactiva y regresa a STATE_CONFIG.
* Cada segundo, el tiempo disminuye hasta llegar a 0.

### Eventos de entrada en STATE_EXPLOSION
* Se reproduce sonido y parpadea la luz.
* Si se toca el logo del micro:bit, la bomba se reinicia.

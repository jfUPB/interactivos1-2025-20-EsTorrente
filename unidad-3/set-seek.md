# Unidad 3

## 🔎 Fase: Set + Seek
### 📝 ACTIVIDAD 01
```program.py
from microbit import *
import utime

STATE_INIT = 0
STATE_ROJO = 1
STATE_VERDE = 2
STATE_AMARILLO = 3

class Semaforo:
    def __init__(self,pixelX,rojo_interval,verde_interval,amarillo_interval):

        self.pixelX = pixelX
        self.state = STATE_ROJO
        self.last_change = utime.ticks_ms()
        self.rojo_interval = rojo_interval  
        self.verde_interval = verde_interval
        self.amarillo_interval = amarillo_interval

    def update(self):
        current_time = utime.ticks_ms()
        tiempoPasado = utime.ticks_diff(current_time, self.last_change)

        if self.state == STATE_ROJO and tiempoPasado > self.rojo_interval:
            self.state = STATE_VERDE
            self.last_change = current_time
            display.set_pixel(self.pixelX, 0, 0)
            self.set_verde()
            
        elif self.state == STATE_VERDE and tiempoPasado > self.verde_interval:
            self.state = STATE_AMARILLO
            self.last_change = current_time
            display.set_pixel(self.pixelX, 4, 0)
            self.set_amarillo()
            
        elif self.state == STATE_AMARILLO and tiempoPasado > self.amarillo_interval:
            self.state = STATE_ROJO
            self.last_change = current_time
            display.set_pixel(self.pixelX, 2, 0)
            self.set_rojo()

    def set_rojo(self):
        display.set_pixel(self.pixelX, 0, 9)

    def set_amarillo(self):
        display.set_pixel(self.pixelX, 2, 9)

    def set_verde(self):
        display.set_pixel(self.pixelX, 4, 9)

Semaforo1 = Semaforo(0,5000,3000,2000)
Semaforo1.set_rojo()
Semaforo2 = Semaforo(2,3000,2000,1000)
Semaforo2.set_rojo()
Semaforo3 = Semaforo(4,4000,2000,3000)
Semaforo3.set_rojo()

while True:
    Semaforo1.update()
    Semaforo2.update()
    Semaforo3.update()

```


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

```program.py
from microbit import *
import utime
import music

STATE_INIT = 0
STATE_CONFIG = 1
STATE_ARMED = 2
STATE_EXPLODE = 3

class Bomba:
    def __init__(self):

        self.PASSWORD = ['A','B','A']
        self.key = ['']*len(self.PASSWORD)
        self.keyindex = 0

        self.counter = 20000 #el rango de tiempo que la persona settea antes de que explote 
        self.start_time = 0 #el momento en el que se arma la bomba
        self.time_left = 0 #lo que queda antes de que explote

        self.current_state = STATE_INIT

    def update(self):
        if self.current_state == STATE_INIT:
            display.show(Image.SMILE)
            sleep(400)
            self.current_state = STATE_CONFIG

        if self.current_state == STATE_CONFIG:
            display.scroll(int(self.counter/1000), delay=100)
            display.scroll('s')

            #sumarle al counter
            if button_a.was_pressed():
                if self.counter < 60000:
                    music.pitch(400, 100)
                    display.show(Image.MEH)
                    sleep(400)
                    self.counter+=1000
                else:
                    display.show(Image.CONFUSED)
                    sleep(400)
                    display.scroll('max reached', delay=100)

            #restarle al counter    
            elif button_b.was_pressed():
                if self.counter > 10000:
                    music.pitch(200, 100)
                    display.show(Image.SURPRISED)
                    sleep(400)
                    self.counter-=1000
                else:
                    display.show(Image.CONFUSED)
                    sleep(400)
                    display.scroll('min reached', delay=100)

            #armar la bomba
            elif accelerometer.was_gesture('shake'):
                display.show(Image.ANGRY)
                music.pitch(200, 200)
                display.scroll('BOMB ARMED', delay=70)
                self.start_time = utime.ticks_ms()
                self.current_state = STATE_ARMED

        # BOMBA ARMADA
        if self.current_state == STATE_ARMED:
            time_left = utime.ticks_diff(self.counter,utime.ticks_diff(utime.ticks_ms(), self.start_time))
            display.scroll(int(time_left/1000), delay=60)

            if time_left < 7000:
                music.pitch(880, 50)
            else:
                music.pitch(400, 50)

            #check explotar
            if utime.ticks_diff(utime.ticks_ms(), self.start_time) > self.counter:
                display.show(Image.SKULL)
                music.play(music.FUNERAL)
                sleep(1500)
                self.current_state = STATE_EXPLODE

            #check contraseña
            if button_a.was_pressed():
                self.key[self.keyindex] = 'A'
                self.keyindex = self.keyindex + 1

            if button_b.was_pressed():
                self.key[self.keyindex] = 'B'
                self.keyindex = self.keyindex + 1

            if self.keyindex == len(self.key):

                passIsOK = True
                for i in range(len(self.key)):
                    if self.key[i] != self.PASSWORD[i]:
                        passIsOK = False
                        break;
                if passIsOK == True:
                    self.counter = 20000
                    display.show(self.counter,wait=False)
                    self.keyindex = 0
                    self.current_state = STATE_CONFIG
                else:
                    self.keyindex = 0

        # BOMBA EXPLOTA
        if self.current_state == STATE_EXPLODE:
            display.scroll('PRESS A TO RESTART', delay=100)

            if button_a.was_pressed():
                display.show(Image.HAPPY)
                sleep(1500)
                self.counter = 20000
                self.current_state = STATE_CONFIG
        
bomba = Bomba()

while True:
    bomba.update()

 ```


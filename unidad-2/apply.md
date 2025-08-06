# Unidad 2

## 🛠 Fase: Apply

### 📝 Actividad 05

```bomba.py
from microbit import *
import utime
import music

STATE_INIT = 0
STATE_CONFIG = 1
STATE_ARMED = 2
STATE_EXPLODE = 3

counter = 20000 #el rango de tiempo que la persona settea antes de que explote 
start_time = 0 #el momento en el que se arma la bomba
time_left = 0 #lo que queda antes de que explote

current_state = STATE_INIT

while True:
    if current_state == STATE_INIT:
        display.show(Image.SMILE)
        sleep(400)
        current_state = STATE_CONFIG

    if current_state == STATE_CONFIG:
        display.scroll(int(counter/1000), delay=100)
        display.scroll('s')

        #sumarle al counter
        if button_a.was_pressed():
            if counter < 60000:
                display.show(Image.MEH)
                sleep(400)
                counter+=1000
            else:
                display.show(Image.CONFUSED)
                sleep(400)
                display.scroll('max reached', delay=100)

        #restarle al counter    
        elif button_b.was_pressed():
            if counter > 10000:
                display.show(Image.SURPRISED)
                sleep(400)
                counter-=1000
            else:
                display.show(Image.CONFUSED)
                sleep(400)
                display.scroll('min reached', delay=100)

        #armar la bomba
        elif accelerometer.was_gesture('shake'):
            display.show(Image.ANGRY)
            display.scroll('BOMB ARMED', delay=100)
            start_time = utime.ticks_ms()
            current_state = STATE_ARMED

    # BOMBA ARMADA
    if current_state == STATE_ARMED:
        time_left = utime.ticks_diff(counter,utime.ticks_diff(utime.ticks_ms(), start_time))
        display.scroll(int(time_left/1000), delay=100)

        if time_left < 5:
            music.play(music.BA_DING)


        #check explotar
        if utime.ticks_diff(utime.ticks_ms(), start_time) > counter:
            current_state = STATE_EXPLODE

    # BOMBA EXPLOTA
    if current_state == STATE_EXPLODE:
        music.play(music.FUNERAL)
        display.show(Image.SKULL)
        sleep(1500)
        display.scroll('PRESS A TO RESTART', delay=100)

        if button_a.was_pressed():
            counter = 20000
            current_state = STATE_CONFIG

```

# Unidad 2

## 🛠 Fase: Apply

### 📝 Actividad 04
  
<img width="1090" height="897" alt="image" src="https://github.com/user-attachments/assets/182ca611-d06f-4541-84e7-a9992708b100" />

___  

︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶   

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
                music.pitch(400, 100)
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
                music.pitch(200, 100)
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
            music.pitch(200, 200)
            display.scroll('BOMB ARMED', delay=70)
            start_time = utime.ticks_ms()
            current_state = STATE_ARMED

    # BOMBA ARMADA
    if current_state == STATE_ARMED:
        time_left = utime.ticks_diff(counter,utime.ticks_diff(utime.ticks_ms(), start_time))
        display.scroll(int(time_left/1000), delay=60)

        if time_left < 7000:
            music.pitch(880, 50)
        else:
            music.pitch(400, 50)

        #check explotar
        if utime.ticks_diff(utime.ticks_ms(), start_time) > counter:
            display.show(Image.SKULL)
            music.play(music.FUNERAL)
            sleep(1500)
            current_state = STATE_EXPLODE

    # BOMBA EXPLOTA
    if current_state == STATE_EXPLODE:
        display.scroll('PRESS A TO RESTART', delay=100)

        if button_a.was_pressed():
            display.show(Image.HAPPY)
            sleep(1500)
            counter = 20000
            current_state = STATE_CONFIG

```
**VECTORES DE PRUEBA:**  
︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶  

    
| :) | Estado inicial | Evento / acción del usuario | Predict de la salida | Estado final | funciona o no |
|----|----------------|------------------------------|-------------------------------------|--------------|----|
| 🌱  | `STATE_CONFIG`, contador = 20000 | presionar **A** | beep agudo (400 Hz), dibujito `MEH`, contador aumenta a 21000 | `STATE_CONFIG` | ✅ |
| 🌿  | `STATE_CONFIG`, contador = 60000 | presionar **A** | dibujito de `CONFUSED`, mensajito “max reached” | `STATE_CONFIG` | ✅ |
| ☘️  | `STATE_CONFIG`, contador = 20000 | presionar **B** | beep grave (200 Hz), dibujito `SURPRISED`, contador disminuye a 19000 | `STATE_CONFIG` | ✅ |
| 🌼  | `STATE_CONFIG`, contador = 10000 | presionar **B** | dibujito `CONFUSED`, mensaje “min reached” | `STATE_CONFIG` | ✅ |
| 🌻  | `STATE_CONFIG` | Agitar (shake), contador entre 10000 y 60000 | dibujito `ANGRY`, beep grave, mensaje “BOMB ARMED” | `STATE_ARMED` | ✅ |
| 🍃  | `STATE_ARMED`, tiempo restante = 20000 | tiempo_restante >= 7000 | display muestra segundos, beep medio (400 Hz) cada ciclo | `STATE_ARMED` | ✅ |
| 🍂  | `STATE_ARMED`, tiempo restante = 8000 | tiempo_restante < 7000 | display muestra segundos, beep agudo (880 Hz) cada ciclo | `STATE_ARMED` | ✅ |
| 🍁  | `STATE_ARMED`, tiempo restante = 1s | tiempo restante = 0 | suena marcha fúnebre, dibujito `SKULL`, mensajito “PRESS A TO RESTART” | `STATE_EXPLODE` | ✅ |
| 🌱  | `STATE_EXPLODE` | presionar **A** | contador reiniciado a 20000, vuelve a configuración y el display muestra el tiempo | `STATE_CONFIG` | ✅ |



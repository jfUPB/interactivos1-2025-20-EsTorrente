
# Evidencias de la unidad 8


from microbit import *
import math

uart.init(baudrate=115200)

def get_tilt_data():
    """Get pitch and roll, map to -90 to 90 range"""
    pitch = accelerometer.get_y() 
    roll = accelerometer.get_x() 
    
    pitch_deg = max(-90, min(90, pitch / 11))
    roll_deg = max(-90, min(90, roll / 11))
    
    return int(pitch_deg), int(roll_deg)

while True:
    pitch, roll = get_tilt_data()
    uart.write('P' + str(pitch) + '\n')
    uart.write('R' + str(roll) + '\n')
    
    if accelerometer.was_gesture('shake'):
        uart.write('SHAKE\n')
        display.show(Image.SKULL)
        sleep(200)
        display.clear()
    
    sleep(50)  

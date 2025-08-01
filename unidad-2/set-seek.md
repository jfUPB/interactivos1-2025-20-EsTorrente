# Unidad 2

## 🔎 Fase: Set + Seek
︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶
### 📝Actividad 01  
```program.py
from microbit import *
import utime

class Pixel:
    def __init__(self,pixelX,pixelY,initState,interval):
        self.state = "Init"
        self.startTime = 0
        self.interval = interval
        self.pixelX = pixelX
        self.pixelY = pixelY
        self.pixelState = initState

    def update(self):

        if self.state == "Init":
            self.startTime = utime.ticks_ms()
            self.state = "WaitTimeout"
            display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

        elif self.state == "WaitTimeout":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                if self.pixelState == 9:
                    self.pixelState = 0
                else:
                    self.pixelState = 9
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

pixel1 = Pixel(0,0,0,1000)
pixel2 = Pixel(4,4,0,500)

while True:
    pixel1.update()
    pixel2.update()
```
  
🌱 **Describe detalladamente cómo funciona este ejemplo.**  
> 1. Importa la biblioteca que contiene todas las funciones del micro:bit + lo que se necesita para las funciones que trabajan con el tiempo.  
> 2. Define una clase llamada Pixel, que representa un solo LED en el cosito del micro:bit.  
> 3. El método `__init__` sería el constructor de esa clase, con los parámentros self (el equivalente del this en C#), pixelX (coordenada en X del pixel), pixelY (coordenada en Y del pixel), initState (el estado inicial de ese pixel, es decir, si está prendido o apagado), e interval (el intervalo de tiempo en milisegundos entre el cambio de estado).  
> 4. Inicializa cada uno de los atributos con el valor que le corresponde. Aquí aparecen 3 parámetros que no se pedían dentro del constructor: self.state (el estado inicial de la máquina de estados), this.startTime (guarda el tiempo con el que se compara el intervalo), y self.pixelState (que tiene un rango de 0 a 9 y controla el brillo (/opacidad?) del LED correspondiente.  
> 5. El método Update(self) actualiza el estado del pixel en cada iteración del loop.  
> 6. Si el estado del Pixel es igual a Init (que lo es al inicio), entonces:  
>    - `self.startTime` guarda el tiempo actual en milisegundos con `utime.ticks_ms()`  
>    - `self.starte = "WaitTimeout"` cambia al estado de esperar / embarazo.  
>    - `display.set_pixel(parámetros)` enciende/ apaga el LED dependiendo del initState.  
> 7. Como ya está en el estado WaitTimeout, se ejecuta el bloque que sigue: si la diferencia entre el tiempo actual y el startTime > el intervalo de tiempo que asignamos, entonces:   
>    - reinicia el startTime.  
>    - Si el LED estaba encendido (9 = full opacidad), lo apaga (pixelState = 0). Si no, lo prende y vuelve a actualizar el pixel.  
> 8. Ya por fuera de la clase, empieza a instanciar los Pixeles. Crea uno con la posición X y Y en 0 (esquina arriba izquierda), inicialmente apagado y con un intervalo de 1000 ms.  
> 9. Luego instancia otro con posición X y Y en 4 (esquina abajo derecha), inicialmente apagado y con un intervalo de 500 ms.  
> 10. Finalmente, crea un loop While(true) que hace que los pixeles se actualicen constantemente.  
  
🌿 **¿Cuáles son los estados en el programa?**  
> Init y WaitTimeout.  
  
🌼 **¿Cuáles son los eventos/inputs en el programa?**  
> 🍃 **EVENTOS:** esperar a que el tiempo actual pase por 1 ms al startTime (el tiempo que le asignamos) para prender o apagar el LED.  
> 🍂 **INPUTS:** no estoy segura... no sé si el tiempo o los parámetros contarían de alguna manera?
  
🌻 **¿Cuáles son las acciones en el programa?**  
> 🍃 Prender/apagar los LEDS con el display.set_pixel.  
> 🍂 Cambiar entre los estados.
> 🍁 Reiniciar el startTime 

___
### 📝Actividad 02  
🌱 Implementemos juntos un semáforo simple (rojo, amarillo, verde) utilizando una máquina de estados en Micropython. Representaremos cada color del semáforo con un LED del display del micro:bit. Escribe el código que soluciona este problema en tu bitácora.
```semaforo.py
from microbit import *
import utime

class Semaforo:
    def __init__(self):
        self.state = "Rojo"
        self.last_change = utime.ticks_ms()
        self.rojo_interval = 2000  
        self.verde_interval = 2000  
        self.amarillo_interval = 800  

    def update(self):
        current_time = utime.ticks_ms()
        tiempoPasado = utime.ticks_diff(current_time, self.last_change)

        if self.state == "Rojo" and tiempoPasado > self.rojo_interval:
            self.state = "Verde"
            self.last_change = current_time
            self.clear_lights()
            self.set_verde()
            
        elif self.state == "Verde" and tiempoPasado > self.verde_interval:
            self.state = "Amarillo"
            self.last_change = current_time
            self.clear_lights()
            self.set_amarillo()
            
        elif self.state == "Amarillo" and tiempoPasado > self.amarillo_interval:
            self.state = "Rojo"
            self.last_change = current_time
            self.clear_lights()
            self.set_rojo()

    def set_rojo(self):
        display.set_pixel(1, 0, 9)
        display.set_pixel(2, 0, 9)
        display.set_pixel(3, 0, 9)

    def set_amarillo(self):
        display.set_pixel(1, 2, 9)
        display.set_pixel(2, 2, 9)
        display.set_pixel(3, 2, 9)

    def set_verde(self):
        display.set_pixel(1, 4, 9)
        display.set_pixel(2, 4, 9)
        display.set_pixel(3, 4, 9)

    def clear_lights(self):
        display.clear()

semaforo = Semaforo()
semaforo.set_rojo()

while True:
    semaforo.update()
```
  
🌱 **EXPLICACIÓN:**  
> 1. Crea la clase semáforo  
> 2. Crea el constructor con __init__(self): (sin parámetros, no hay necesidad)  
> 3. self.starte = "Rojo" empieza el estado en rojo  
> 4. self.last_change = utime.ticks_ms() guarda el tiempo del último cambio de estado realizado  
> 5. Define cuánto va a esperar cada intervalo de color antes de cambiar.  

Ahora, en update(self) del semáforo:  
> 1. Almacena el tiempo actual.  
> 2. En tiempoPasado calcula la diferencia entre el tiempo actual y el último cambio.   
> 3. Si estaba en estado rojo y el tiempoPasado > al intervalo que puse para el cambio de rojo a verde, entonces:  
>   - Cambia el estado a Verde  
>   - Reinicia el tiempo del último cambio  
>   - Borra las luces que le corresponden al rojo  
>   - Va al método de set_verde  
> 4. Hace lo mismo dependiendo del color en el que estaba antes.  
> 5. En los métodos de set_(color), enciende los 3 LEDs que decidí asignarle a cada uno. En clear_lights los apaga todos.  

> Ya por fuera de Semaforo, instancia un semaforo nuevo y lo empieza en rojo. En en while true lo va actualizando cada frame.  
  
🌿 **OBSERVACIONES:** Aunque en el constructor se setea el estado en Rojo, luego tengo que volver a usar semaforo.set_rojo... esto es porque si no lo hago, simplemente espera los 2000 ms con los leds totalmente apagados y después prende los correspondientes al verde, saltándose el primer momento.   
  
`︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶`
  
🍃 **ESTADOS:** Rojo, Verde, Amarillo  
  
🍂 **EVENTOS:** que el tiempo actual - el tiempo transcurrido desde el último cambio sobrepase al intervalo de espera de cada color.  
  
🍁 **ACCIONES:**  
1. Cambiar los estados  
2. Prender y apagar los LEDS  
3. Actualizar el tiempo desde el último cambio  

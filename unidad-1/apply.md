# Unidad 1

## 🛠 Fase: Apply
### 📝Actividad 05
**Explica cómo funciona el sistema físico interactivo que acabamos de crear.**  
  
🌱 Parte de python (micro:bit editor):
> 1. Importa la biblioteca con todas las funciones necesarias del micro:bit.
> 2. Para saber qué versión del programa está cargado en el micro:bit, le indicamos que muestre un dibujo en la pantalla LED.
> 3. Se inicia la comunicación serial para recibir mensajes en p5.js con una velocidad de transmisión de datos de 115200.
> 4. While TRUE (ciclo infinito), detecta que el botón A esté siendo presionado (con `is`, no `was`). Si lo está, entonces envía como mensaje una "A". De lo contrario, envía una "N".
>    > **PARÉNTESIS:**  
>    >🍂Si uso is, el círculo es rojo mientras mantenga el botón presionado y verde apenas lo deje de presionar.  
>    >🍃Con was, el círculo es rojo por un frame mientras presiono el botón, e inmediatamente después se vuelve verde. No vuelve a ser rojo hasta que lo presione otra vez, incluso si nunca levanté el dedo del botón.
> 5. Espera 100 milisegundos antes de volver a revisar.
  
🌿 Parte de p5.js:
> 1. Se añade la biblioteca que permite conectar el micro:bit con el programa p5.js
> 2. Se crean 3 variables globales (que se pueden utilizar en cualquier parte del código): una que permite referenciar el objeto que manipula el puerto serial, una que permite referenciar el objeto que representa al botón que se utiliza para conectar el micro:bit, y una para evitar que port.clear() se ejecute varias veces después de abrir el serial.
> 3. Setup() se ejecuta solamente al inicio. Crea el canvas, pone el fondo blanco, inicializa el puerto y crea un botón que permita conectarse/desconectarse del micro:bit con un clic.
> 4. Draw() se ejecuta cada frame. Si el port está abierto (ya se dió clic al botón) y `connectionInitialized = false`, entonces limpia toda la información que el micro:bit había estado mandando constantemente y cambia connectionInitialized a true para que no se siga ejecutando en el loop de Draw().
> 5. Revisa si hay algún dato que se ha mandado, y si lo hay, revisa si el dato es una "A" o una "N". Si es "A", cambia el color del fill del cuadrado a rojo. Si es "N" cambia el color a verde.
> 6. Luego dibuja el cuadrado con las coordenadas de la mitad del canvas, y el ancho y largo de 50px.
> 7. Si el puerto no se ha abierto, el texto del botón dice `"Connect to micro:bit"`. Si se ha abierto, cambia a `"Disconnect"`
> 8. Se ejecuta el loop de draw constantemente, por lo que el cuadrado está siendo redibujado cada frame y actualizado en tiempo real de acuerdo a los mensajes que recibe el programa. Lo mismo para el botón.
> 9. La función `connectBtnClick()` solo se llama al realizar clic en el botón. Si el puerto no ha sido abierto, lo abre. Después indica que `connectionInitialized = false`. Con esto, se cumplen los dos requisitos para que se puedan limpiar los datos anteriores.
> 10. Si el puerto sí ha sido abierto y se vuelve a hacer clic en el botón, lo cierra de nuevo.
___
### 📝Actividad 06  
[link](https://editor.p5js.org/EsTorrente/sketches/HgND26Wwj)
```python.py
from microbit import *

uart.init(baudrate=115200)
display.show(Image.RABBIT)

while True:

    if button_a.is_pressed():
        uart.write('A')
    elif button_b.is_pressed():
            uart.write('B')
    else:
        uart.write('N')

    sleep(100)
```
```p5.js
  let port;
  let connectBtn;
  let connectionInitialized = false;
  let positionX = 160;

  function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton("Connect to micro:bit");
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
  }

  function draw() {
    background(220);

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    if (port.availableBytes() > 0) {
      let dataRx = port.read(1);
      if (dataRx == "A") {
        positionX = positionX - 10;
        fill("red");
      } else if (dataRx == "B") {
        positionX = positionX + 10;
        fill("green");
      }
      else if (dataRx == "N") {
        fill("blue");
      }
    }

    rectMode(CENTER);
    circle(positionX, height / 2, 50);

    if (!port.opened()) {
      connectBtn.html("Connect to micro:bit");
    } else {
      connectBtn.html("Disconnect");
    }
  }

  function connectBtnClick() {
    if (!port.opened()) {
      port.open("MicroPython", 115200);
      connectionInitialized = false;
    } else {
      port.close();
    }
  }
```

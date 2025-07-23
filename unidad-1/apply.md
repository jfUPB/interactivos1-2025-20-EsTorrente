# Unidad 1

## 🛠 Fase: Apply
### Actividad 06  
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

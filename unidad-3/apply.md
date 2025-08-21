# Unidad 3


## 🛠 Fase: Apply

### 📝 Actividad 06

```
let state;
let counter;
let startTime;
let eventValue;
let PASSWORD;
let passwordKey;
let keyIndex;

function setup() 
{
  createCanvas(windowWidth, windowHeight);
  background(200);
  textSize(30);
  textAlign(CENTER, CENTER);
  
  state = 'CONFIG';
  counter = 20;
  startTime = 0;
  eventValue = '0';
  PASSWORD = ['A','B','A'];
  passwordKey = []; 
  keyIndex = 0;
}

function draw() {
  //================ config ===============
  if (state === 'CONFIG') 
  {
    fill('black');
    background(200);
    
    textSize(30);
    text('Presione "A" para aumentar 1 segundo, "B" para restar.', width/2, 100);
    text('"S" para activar', width/2, 140);
    
    textSize(200);
    text(counter, width/2, height/2);
    
    if (eventValue === 'A' && counter < 60) 
    {
      eventValue = '0';
      counter += 1;
    }
    
    if (eventValue === 'B' && counter > 10) 
    {
      eventValue = '0';
      counter -= 1;
    }
    
    if (eventValue === 'S') 
    {
      eventValue = '0';
      startTime = millis();
      state = 'ARMED';
      passwordKey = [];
      keyIndex = 0;
    }
  }
  
  //================ armada ===============
  else if (state === 'ARMED') {
    textSize(200);
    fill('red')
    let timePassed = (millis() - startTime)/1000;
    let timeLeft = int(counter - timePassed);
    
    if (timeLeft > 0) {
      background(200);
      text(timeLeft, width/2, height/2);

      // Mostrar clave ingresada
      textSize(30);
      fill('black');
      text("Clave: " + passwordKey.join(''), width/2, height/2 + 100);
    } 
    else if (timeLeft <= 0) 
    {
      background(200);
      state = 'EXPLODED';
    }
    
    // contraseña -----------------
    
    if (eventValue === 'A') 
    {
      eventValue = '0';
      if (keyIndex < PASSWORD.length) 
      {
        passwordKey[keyIndex] = 'A';
        keyIndex++;
      }
    }
    
    if (eventValue === 'B') 
    {
      eventValue = '0';
      if (keyIndex < PASSWORD.length) 
      {
        passwordKey[keyIndex] = 'B';
        keyIndex++;
      }
    }
    
    // revisar si ya está completa --------
    
    if (keyIndex === PASSWORD.length) {
      let passIsOkay = true;
      
      for (let i = 0; i < PASSWORD.length; i++) 
      {
        if (passwordKey[i] !== PASSWORD[i]) 
        {
          passIsOkay = false;
          break;
        }
      }
      
      if (passIsOkay) {
        // Contraseña correcta, desarma la bomba
        counter = 20;
        state = 'CONFIG';
        passwordKey = [];
        keyIndex = 0;
      } 
      else 
      {
        // Contraseña incorrecta
        passwordKey = [];
        keyIndex = 0;
      }
    }
  }
  
  //================ explota ===============
  else if (state === 'EXPLODED') {
    textSize(30);
    fill('blue')
    background(200);
    
    text('Perdiste. Presiona "T" para reiniciar :(', width/2, 40);
    
    if (eventValue === 'T') {
      eventValue = '0';
      counter = 20;
      passwordKey = [];
      keyIndex = 0;
      state = 'CONFIG';
    }
  }
}

function keyPressed() {
  if (key === 'a' || key === 'A') 
  {
    eventValue = 'A';
  }
  
  if (key === 'b' || key === 'B') 
  {
    eventValue = 'B';
  }
  
  if (key === 's' || key === 'S') 
  {
    eventValue = 'S';
  }
  
  if (key === 't' || key === 'T') 
  {
    eventValue = 'T';
  }
}
```

___

### 📝 Actividad 07

[Link](https://editor.p5js.org/EsTorrente/sketches/TYiutwYir)  
No alcancé a hacerlo en la clase y en la casa no hay micro:bit, entonces está hecho a ciegas y en base a los anteriores programas que ya habíamos diseñado para conectarse entre los dos. No sé si funciona. :c  

🌱 **Código del micro:bit**  
``` program.py
from microbit import *

uart.init(baudrate=115200)

while True:
    if button_a.was_pressed():
        uart.write('A')
        display.show('A')
        sleep(300)
        display.clear()
        
    if button_b.was_pressed():
        uart.write('B')
        display.show('B')
        sleep(300)
        display.clear()
        
    if accelerometer.was_gesture('shake'):
        uart.write('S')
        display.show(Image.ANGRY)
        sleep(300)
        display.clear()
        
    if pin_logo.is_touched():
        uart.write('T')
        display.show(Image.HAPPY)
        sleep(300)
        display.clear()
```

🌿 **Código del p5.js**  
En el index: `<script src="https://unpkg.com/@gohai/p5.webserial@^1/libraries/p5.webserial.js"></script>`    
```
let state;
let counter;
let startTime;
let eventValue;
let PASSWORD;
let passwordKey;
let keyIndex;
let port;
let connectBtn;

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(200);
  textSize(30);
  textAlign(CENTER, CENTER);
  
  state = 'CONFIG';
  counter = 20;
  startTime = 0;
  eventValue = '0';
  PASSWORD = ['A','B','A'];
  passwordKey = []; 
  keyIndex = 0;
  
  // confi de comunicación serial
  port = createSerial();
  connectBtn = createButton('Conectar al micro:bit');
  connectBtn.position(20, 20);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  
  if(port.availableBytes() > 0){
    let dataRx = port.read(1);
    if(dataRx === 'A'){
      eventValue = 'A';
    }
    else if(dataRx === 'B'){
      eventValue = 'B';
    }
    else if(dataRx === 'S'){
      eventValue = 'S';
    }
    else if(dataRx === 'T'){
      eventValue = 'T';
    }
  }
  
  //================ config ===============
  if (state === 'CONFIG') {
    fill('black');
    background(200);
    
    textSize(30);
    text('Presione "A" para aumentar 1 segundo, "B" para restar.', width/2, 100);
    text('"S" para activar', width/2, 140);
    
    textSize(200);
    text(counter, width/2, height/2);
    
    if (eventValue === 'A' && counter < 60) {
      eventValue = '0';
      counter += 1;
    }
    
    if (eventValue === 'B' && counter > 10) {
      eventValue = '0';
      counter -= 1;
    }
    
    if (eventValue === 'S') {
      eventValue = '0';
      startTime = millis();
      state = 'ARMED';
      passwordKey = [];
      keyIndex = 0;
    }
  }
  
  //================ armada ===============
  else if (state === 'ARMED') {
    textSize(200);
    fill('red');
    let timePassed = (millis() - startTime)/1000;
    let timeLeft = int(counter - timePassed);
    
    if (timeLeft > 0) {
      background(200);
      text(timeLeft, width/2, height/2);
      
      // Mostrar clave ingresada
      textSize(30);
      fill('black');
      text("Clave: " + passwordKey.join(''), width/2, height/2 + 100);
    } 
    else if (timeLeft <= 0) {
      background(200);
      state = 'EXPLODED';
    }
    
    // contraseña -----------------
    if (eventValue === 'A') {
      eventValue = '0';
      if (keyIndex < PASSWORD.length) {
        passwordKey[keyIndex] = 'A';
        keyIndex++;
      }
    }
    
    if (eventValue === 'B') {
      eventValue = '0';
      if (keyIndex < PASSWORD.length) {
        passwordKey[keyIndex] = 'B';
        keyIndex++;
      }
    }
    
    // revisar si ya está completa --------
    if (keyIndex === PASSWORD.length) {
      let passIsOkay = true;
      
      for (let i = 0; i < PASSWORD.length; i++) {
        if (passwordKey[i] !== PASSWORD[i]) {
          passIsOkay = false;
          break;
        }
      }
      
      if (passIsOkay) {
        // Contraseña correcta, desarma la bomba
        counter = 20;
        state = 'CONFIG';
        passwordKey = [];
        keyIndex = 0;
      } else {
        // Contraseña incorrecta
        passwordKey = [];
        keyIndex = 0;
      }
    }
  }
  
  //================ explota ===============
  else if (state === 'EXPLODED') {
    textSize(30);
    fill('blue');
    background(200);
    
    text('Perdiste. Presiona "T" para reiniciar :(', width/2, 100);
    
    if (eventValue === 'T') {
      eventValue = '0';
      counter = 20;
      passwordKey = [];
      keyIndex = 0;
      state = 'CONFIG';
    }
  }
  
  // cambiar botoncito dependiendo de si está conectado o no
  if (!port.opened()) {
    connectBtn.html('Conectar al micro:bit');
  } else {
    connectBtn.html('Desconectar');
  }
}

// lo mantengo igual para testearlo en la casita
function keyPressed() {
  if (key === 'a' || key === 'A') {
    eventValue = 'A';
  }
  
  if (key === 'b' || key === 'B') {
    eventValue = 'B';
  }
  
  if (key === 's' || key === 'S') {
    eventValue = 'S';
  }
  
  if (key === 't' || key === 'T') {
    eventValue = 'T';
  }
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open('MicroPython', 115200);
  } else {
    port.close();
  }
}
```



# Evidencias de la unidad 8

### ⭐ DECISIONES CREATIVAS:  

🌱 **Inspo:** videos donde el focus son los lyrics, con movimientos rápidos de cámara, flashes, texturas en el fondo y cosas así. Lo principal es la letra, apoyado por gráficos y estética que van con la temática de la canción. Busqué específicamente referentes de metal, porque quería ver cómo lograban darle a los visuals la misma fuerza que tiene la música. [Esta fue mi inspo principal](https://youtu.be/HjuEq1p5XYY?si=KQnHm6yLhaRtrJJz).

**Le dí al usuario la opción de mandar las cosas que Dios le envió a Egipto con las partículas (no todas):**  
- los bichitos se mueven erráticamente como una infestación real  
- el fuego que cae del cielo como en la canción  
- la oscuridad se expande y pulsa, y aparte se ve slay  
- el granizo cae con peso y fuerza
  
**Los fondos cambian dependiendo de la persona que dice la letra:**  
- Rojos intensos para Dios: poder, ira, lo divino  
- Azules profundos para Moisés: tristeza, conflicto, noche  
- Azul más clarito todavía para Moisés: nostalgia, esperanza, anhelo  
- Rojos vibrantes para Ramsés: obstinación, pasión, peligro   
  
**Para tipografías:**  
- Dios en tipografía grande, impactante, que casi grita (+ la mega pared de texto de atrás que es intimidante)  
- Moisés en fuentes más serif, elegantes, humanas  
- Ramsés en negritas de maluco rebelde
  
**Figuritas de fondo:**  
- Para Moisés, el caleidoscopio adopta formas redondeadas, circulares y suaves, representando compasión, tristeza y comprensión espiritual.  
- Para Ramsés, las formas se vuelven puntiagudas y angulares, porque es señor firme maluco orgulloso, y por la dureza y el filo de su destino (que él eligió pero después Dios dijo: ok sí total)  
  
Cuando el coro de Dios se repite por toda la pantalla, es para transmitir la idea de que sus palabras llenan todo, que no hay escapatoria, que el mensaje divino satura el espacio. Es abrumador a propósito B)  
  
También, como es la versión metal, quería enfatizar como esos golpes chéveres de la música... entonces hice que todo tuviera como pulsaciones y flashes de luz en base al gesto "shake" del micro:bit y el ritmo de la música.  

🌼 **CONTROL DEL CELULAR:** elegí este para spawnear las partículas porque me permitía poner muuucha cantidad de botones, a diferencia del micro:bit que no sería tan directo. Me deja tener una interfaz que le muestre al usuario la figurita que va a spawnear, el nombre (para que lo relacione con el lyric en pantalla rápidamente) y no tenga que aprender distintos gestos de memoria (como en el micro:bit, que tocaría memorizar cuál spawnea el shake, el A, el B, todas esas cosas).  

🌻 **CONTROL DEL MICRO:BIT:** por otro lado, el micro:bit era súper perfecto para controlar el movimiento de la cámara al mismo tiempo que se usa el celular para spawnear las partículas, porque es bastante fácil tiltearlo y sacudirlo con la mano no dominante y mientras estás concentrado en múltiples acciones a la vez. Dependiendo de cómo tilteas el micro:bit, se genera un paralax entre los lyrics principales y los gráficos del fondo (la pared de texto, los caleidoscopios y las partículas), generando mucho más interés visual. Además, el gesto de "shake" está configurado para triggerear el flash de luz, lo que permite enfatizar momentos específicos como palabras dichas con más fuerza o cambio entre personajes. No necesito ningún UI para esas acciones, por lo que fue una muy buena opción.  
  
🌱 **SKETCHES DEL UI:**  
`Celular:`  
<img width="1020" height="1920" alt="image" src="https://github.com/user-attachments/assets/fe3b8643-13af-4120-8d90-fe0d32058699" />
  
`PC:`  
Dios:  
<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/8ce9c8e9-07ed-4344-bffd-e9d24458de90" />  
  
Moises:
<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/7de60d74-d1fb-4a3a-a84e-7bdfeb75175e" />   
  
Ramses:  
<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/20ac6f2d-8bfd-4bc1-8e6c-bd327bb3d82d" />  
    
🌱 **DIAGRAMA:**   
<img width="892" height="927" alt="image" src="https://github.com/user-attachments/assets/c77608b7-f452-491a-9641-a12f9366c347" />
  

🌱 **PROCESO DE ELABORACIÓN:**
1. Elegí la canción y me imaginé qué tipo de visuales podrían contar la historia por medio de colores y formas, dándole a la audicencia una idea de quiénes son los personajes y sus personalidades sin necesidad de conocerlos realmente.  
2. Empecé a buscar referentes de lyric video interesantes del género de metal para identificar cómo enfatizaban la fuerza de la música.  
3. Busqué sketches de p5.js con visualizadores de audio que crearan caleidoscopios en base a la música.
4. Identifiqué cómo usar partículas en p5.js.  
5. Comencé a hacer un "esqueleto" del código, donde indicaba los eventos, la información que debía ser enviada, los tipos de partículas, los casos donde el fondo debía de cambiar de color y cuándo.  
6. Encontré el archivo .lrc de la canción y la sincronicé correctamente con el audio.
7. Usando una mezcla de ChatGPT y Claude, les pasé el código base que había creado y describí detalladamente lo que quería que completara. Le dí también el código en p5.js de los referentes de visualizadores y partículas en p5.js para que trabajara sobre ellos. A medida que me devolvía el código, lo analizaba para encontrar errores (había múltiples, como algunos casos donde duplicaba métodos y generaba ocultamiento. Esto sucedía porque el código era muy largo, y eso generaba un break entre prompts donde tenía que continuar escribíendolo en otro mensaje). Al testearlo, identificaba todos los bugs y le devolvía una lista de los errores, captura de la consola de la página, y mi teoría de por qué estaba sucediendo... todo esto en ciclo, hasta obtener un resultado que me agradó.  
___
## ⭐ CÓDIGO ⭐

### 🌿 **micro:bit**

```py
from microbit import *
import math

uart.init(baudrate=115200)

def get_tilt_data():
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
```
### 🌿 **server.js**

```js
// server.js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const path = require('path');

const app = express();
const server = http.createServer(app);
const io = socketIO(server, {
  cors: { origin: "*", methods: ["GET", "POST"] }
});

const PORT = 3000;

// Sirve la carpeta public
app.use(express.static(path.join(__dirname, 'public')));

// Rutas explícitas
app.get('/', (req, res) => {
  res.redirect('/mobile');
});
app.get('/desktop', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'desktop', 'index.html'));
});
app.get('/mobile', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'mobile', 'index.html'));
});

io.on('connection', (socket) => {
  console.log('New client connected:', socket.id);

  socket.on('client-type', (type) => {
    console.log(`Client identified as: ${type} (${socket.id})`);
    socket.clientType = type;
    // aviso a otros 
    socket.broadcast.emit('device-connected', { id: socket.id, type });
  });

  socket.on('plague-trigger', (plagueData) => {
    console.log('Plague triggered:', plagueData);
    // enviar a todos los desktop conectados
    io.sockets.sockets.forEach((s) => {
      if (s.clientType === 'desktop') s.emit('plague-incoming', plagueData);
    });
  });

  socket.on('disconnect', () => {
    console.log('Client disconnected:', socket.id);
  });
});

server.listen(PORT, () => {
  console.log(`🎭 The Plagues - Server listening on http://localhost:${PORT}`);
  console.log(`Mobile -> http://localhost:${PORT}/mobile`);
  console.log(`Desktop -> http://localhost:${PORT}/desktop`);
});
```

### 🌿 **style.css**
```css
/* --- Lyrics overlay (center) --- */
#lyric-overlay {
  position: absolute;
  z-index: 10050; /* MUY ARRIBA para estar por encima de la vignette */
  left: 50%; top: 50%;
  transform: translate(-50%, -50%);
  width: 72vw; max-width: 1400px;
  pointer-events: none;
  text-align: center;
  line-height: 1.05;
  white-space: pre-wrap;
  text-wrap: balance;
  transition: color 0.25s ease, text-shadow 0.25s ease, font-family 0.25s ease, transform 0.12s ease;
}

/* tamaños base */
#lyric-overlay.small { font-size: 28px; }
#lyric-overlay.medium { font-size: 44px; }
#lyric-overlay.large { font-size: 64px; }
#lyric-overlay.xlarge { font-size: 92px; }

/*El span que contiene el texto (aquí aplicamos el glow real)*/
#lyric-overlay .line {
  display: inline-block;
  -webkit-font-smoothing: antialiased;
  text-rendering: optimizeLegibility;
  transition: filter 120ms linear, text-shadow 120ms linear;
  will-change: text-shadow, filter, transform;
  /* opción extra: un leve stroke para separar mejor del fondo */
  -webkit-text-stroke: 0.6px rgba(0,0,0,0.25);
}

/* MOSES - glow azul */
#lyric-overlay.moses .line {
  color: #b4d5ff;
  text-shadow:
    0 0 6px rgba(150,200,255,0.9),
    0 0 18px rgba(100,180,255,0.6),
    0 0 36px rgba(80,160,255,0.35);
  filter: drop-shadow(0 6px 18px rgba(0,30,60,0.45));
}

/* RAMSES - glow rojo */
#lyric-overlay.ramses .line {
  color: #ff3333;
  text-shadow:
    0 0 8px rgba(255,70,70,0.95),
    0 0 22px rgba(255,30,30,0.7),
    0 0 48px rgba(255,40,40,0.36);
  filter: drop-shadow(0 6px 20px rgba(60,0,0,0.5));
}

/* GOD - glow dorado */
#lyric-overlay.god .line {
  color: #ffd88c;
  text-shadow:
    0 0 8px rgba(255,230,180,0.95),
    0 0 28px rgba(255,200,100,0.7),
    0 0 60px rgba(255,160,60,0.36);
  filter: drop-shadow(0 8px 26px rgba(60,40,0,0.55));
}

/* DEFAULT - glow suave */
#lyric-overlay.default .line {
  color: #fff0d6;
  text-shadow:
    0 0 6px rgba(255,255,255,0.6),
    0 0 14px rgba(255,255,255,0.28);
  filter: drop-shadow(0 6px 14px rgba(0,0,0,0.32));
}
```
## 🌱 MOBILE
### 🌿 **sketch.js**
```js
let socket;
let buttons = [];
let connectionStatus = "Conectando...";
const plagueTypes = [
  { name: 'Pestilence', type: 'insects', emoji: '🪳', color: [255,100,30] },
  { name: 'Locusts', type: 'locusts', emoji: '🦗', color: [170,220,80] },
  { name: 'Fire', type: 'fire', emoji: '🔥', color: [255,140,40] },
  { name: 'Hail', type: 'hail', emoji: '🧊', color: [120,180,255] },
  { name: 'Darkness', type: 'darkness', emoji: '🌑', color: [90,90,110] },
  { name: 'Thunder', type: 'thunder', emoji: '⚡', color: [230,220,100] }
];

function setup(){
  const c = createCanvas(windowWidth, windowHeight);
  c.parent('sketch-container');
  textFont('Arial');

  socket = io();

  socket.on('connect', () => {
    connectionStatus = "✅ Conectado";
    socket.emit('client-type', 'mobile');
  });
  socket.on('connect_error', () => connectionStatus = "❌ Error");
  socket.on('disconnect', () => connectionStatus = "⚠️ Desconectado");

  // botones
  const padding = 18;
  const bw = width - padding*2;
  const bh = Math.min(78, (height - 160) / plagueTypes.length);
  let y = 110;
  for (let p of plagueTypes) {
    buttons.push({
      x: padding, y: y, width: bw, height: bh,
      ...p, pressed:false, pressTime:0
    });
    y += bh + 14;
  }
}

function draw(){
  clear();
  background(10,10,20);
  // título
  push();
    fill(230,150,150);
    textSize(min(46, width/8));
    textAlign(CENTER, TOP);
    textStyle(BOLD);
    text('THE PLAGUES', width/2, 10);
  pop();

  // estado
  push();
    textSize(12);
    textAlign(CENTER, TOP);
    fill(200);
    text(connectionStatus, width/2, 60);
  pop();

  // draw botones
  for (let b of buttons){
    drawButton(b);

    if (b.pressed){
      b.pressTime++;
      if (b.pressTime === 6) { // delay para evitar multi-send
        sendPlague(b, 1);
      } else if (b.pressTime > 40 && b.pressTime % 35 === 0) {
        sendPlague(b, 1 + b.pressTime/80);
      }
    }
  }
}

function drawButton(b){
  push();
    rectMode(CORNER);
    // sombra
    fill(0,0,0,90);
    rect(b.x+4, b.y+6, b.width, b.height, 14);
    // fondo
    fill(b.color[0]*0.12, b.color[1]*0.12, b.color[2]*0.12, 220);
    stroke(b.color[0], b.color[1], b.color[2], 180);
    strokeWeight(2);
    rect(b.x, b.y, b.width, b.height, 14);

    // emoji y texto
    noStroke();
    fill(255);
    textAlign(LEFT, CENTER);
    textSize(min(36, b.height*0.55));
    text(b.emoji, b.x + 18, b.y + b.height/2);

    textSize(min(20, b.height*0.35));
    textStyle(BOLD);
    text(b.name, b.x + 72, b.y + b.height/2 - 8);
    textStyle(NORMAL);
    textSize(min(12, b.height*0.24));
    fill(220,220,220,200);
    text("Tap to send", b.x + 72, b.y + b.height/2 + 14);

    // if pressed overlay
    if (b.pressed){
      fill(255,255,255,24);
      rect(b.x, b.y, b.width, b.height, 14);
    }
  pop();
}

function sendPlague(b, intensity){
  if (socket && socket.connected) {
    socket.emit('plague-trigger', { type: b.type, intensity: intensity || 1 });
  }
}

function mousePressed(){ handlePress(mouseX, mouseY); return false; }
function touchStarted(){ if (touches && touches.length>0) { handlePress(touches[0].x, touches[0].y); } return false; }
function handlePress(px, py){
  for (let b of buttons){
    if (px > b.x && px < b.x + b.width && py > b.y && py < b.y + b.height){
      b.pressed = true;
      b.pressTime = 0;
      return;
    }
  }
}
function mouseReleased(){ releaseAll(); }
function touchEnded(){ releaseAll(); }
function releaseAll(){
  for (let b of buttons){
    if (b.pressed && b.pressTime <= 10) sendPlague(b, 1);
    b.pressed = false;
    b.pressTime = 0;
  }
}
function windowResized(){ resizeCanvas(windowWidth, windowHeight); }
```
### 🌿 **index.hmtl**
```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover,user-scalable=no" />
  <title>The Plagues</title>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
  <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>
  <style>
    html,body {height:100%; margin:0; background:#080814; color:#fff; font-family: Arial, sans-serif;}
    #sketch-container{width:100%;height:100%}
    .hint {position:absolute; top:10px; width:100%; text-align:center; font-size:13px; color:#e9e7ff; opacity:0.9}
  </style>
</head>
<body>
  <div id="sketch-container"></div>
  <script src="sketch.js"></script>
</body>
</html>
```
## 🌱 DESKTOP
### 🌿 **sketch.js**
```js
let socket;
let canvas;
let sound, fft;
let isPlaying = false;
let bgColor = [70, 0, 0], targetBgColor = [70, 0, 0];
let plagueQueue = [];
let pendingPlagues = [];
let debugMessages = [];

// MICRO:BIT SERIAL
let port;
let connectBtn;
let serialBuffer = '';
let microbitConnected = false;

// CAMERA CONTROL
let cameraOffsetX = 0, cameraOffsetY = 0;
let targetCameraX = 0, targetCameraY = 0;
const CAMERA_EASE = 0.08;
const CAMERA_MAX_OFFSET = 180;

// VIGNETTE
let vigImg;
let vigOverlayEl;
const VIG_PATH = 'vig.png';

// KALEIDOSCOPIO
let kaleidoSymmetry = 8;
let kaleidoAngle;

// BEAT & SHAKE
let previousBass = 0;
let shakeFrames = 0;
let shakeMag = 0;
let pulseFrames = 0;
let pulseIntensity = 0;

// AUTO-SPAWN
let lastAutoSpawn = 0;
const AUTO_SPAWN_INTERVAL = 3500;
const MAX_ACTIVE_PLAGUES = 6;

// Lyrics
const lyrics = [
  { time: -9.43, text: "THUS SAITH THE LORD", type: "chorus", character: "god" },
  { time: -7.94, text: "THUS SAITH THE LORD", type: "chorus", character: "god" },
  { time: -5.51, text: "THUS SAITH THE LORD", type: "chorus", character: "god" },
  { time: -3.58, text: "THUS SAITH THE LORD", type: "chorus", character: "god" },
  { time: -1.22, text: "THUS SAITH THE LORD", type: "chorus", character: "god" },
  { time: 1.18, text: "THUS SAITH THE LORD", type: "chorus", character: "god" },
  { time: 3.16, text: "THUS SAITH THE LORD", type: "chorus", character: "god" },
  { time: 5.23, text: "THUS SAITH THE LORD", type: "chorus", character: "god" },
  { time: 7.44, text: "I SEND A PESTILENCE AND PLAGUE", type: "plague", character: "god" },
  { time: 9.75, text: "INTO YOUR HOUSE, INTO YOUR BED", type: "plague", character: "god" },
  { time: 11.77, text: "INTO YOUR STREAMS, INTO YOUR STREETS", type: "plague", character: "god" },
  { time: 14.26, text: "INTO YOUR DRINK, INTO YOUR BREAD", type: "plague", character: "god" },
  { time: 16.30, text: "UPON YOUR CATTLE, ON YOUR SHEEP", type: "plague", character: "god" },
  { time: 18.38, text: "UPON YOUR OXEN IN YOUR FIELD", type: "plague", character: "god" },
  { time: 20.43, text: "INTO YOUR DREAMS, INTO YOUR SLEEP", type: "plague", character: "god" },
  { time: 22.57, text: "UNTIL YOU BREAK, UNTIL YOU YIELD", type: "plague", character: "god" },
  { time: 24.51, text: "I SEND THE SWARM, I SEND THE HORDE", type: "plague-impact", character: "god" },
  { time: 28.87, text: "THUS SAITH THE LORD", type: "chorus", character: "god" },
  { time: 34.58, text: "Once I called you brother", type: "narrative", character: "moses" },
  { time: 36.50, text: "Once I thought the chance to make you laugh", type: "narrative", character: "moses" },
  { time: 40.00, text: "Was all I ever wanted", type: "narrative", character: "moses" },
  { time: 41.40, text: "I SEND THE THUNDER FROM THE SKY", type: "chorus-background", character: "god" },
  { time: 43.16, text: "I SEND THE FIRE RAINING DOWN", type: "chorus-background", character: "god" },
  { time: 45.00, text: "And even now I wish that God had chose another", type: "narrative", character: "moses" },
  { time: 49.50, text: "Serving as your foe on His behalf", type: "narrative", character: "moses" },
  { time: 52.75, text: "Is the last thing that I wanted", type: "narrative", character: "moses" },
  { time: 54.35, text: "I SEND A HAIL OF BURNING ICE", type: "chorus-background", character: "god" },
  { time: 56.10, text: "ON EVERY FIELD, ON EVERY TOWN", type: "chorus-background", character: "god" },
  { time: 59.50, text: "This was my home", type: "narrative", character: "moses" },
  { time: 62.67, text: "All this pain and devastation", type: "narrative", character: "moses" },
  { time: 64.39, text: "How it tortures me inside", type: "narrative", character: "moses" },
  { time: 67.04, text: "All the innocent who suffer", type: "narrative", character: "moses" },
  { time: 69.94, text: "From your stubbornness and pride", type: "narrative", character: "moses" },
  { time: 71.19, text: "I SEND THE LOCUSTS ON THE WIND", type: "plague", character: "god" },
  { time: 72.96, text: "SUCH AS THE WORLD HAS NEVER SEEN", type: "plague", character: "god" },
  { time: 75.33, text: "ON EVERY LEAF, ON EVERY STALK", type: "plague", character: "god" },
  { time: 77.07, text: "UNTIL THERE'S NOTHING LEFT OF GREEN", type: "plague", character: "god" },
  { time: 79.23, text: "I SEND MY SCOURGE, I SEND MY SWORD", type: "plague-impact", character: "god" },
  { time: 83.27, text: "THUS SAITH THE LORD", type: "chorus", character: "god" },
  { time: 85.10, text: "You who I called brother", type: "narrative", character: "moses" },
  { time: 87.50, text: "Why must you call down another blow?", type: "narrative", character: "moses" },
  { time: 89.34, text: "I SEND MY SCOURGE", type: "chorus-background", character: "god" },
  { time: 93.26, text: "I SEND MY SWORD", type: "chorus-background", character: "god" },
  { time: 94.80, text: "LET MY PEOPLE GO", type: "narrative", character: "moses" },
  { time: 98.79, text: "THUS SAITH THE LORD", type: "chorus", character: "god" },
  { time: 108.24, text: "You who I called brother", type: "narrative-ramses", character: "ramses" },
  { time: 109.54, text: "How could you have come to hate me so?", type: "narrative-ramses", character: "ramses" },
  { time: 113.68, text: "Is this what you wanted?", type: "narrative-ramses", character: "ramses" },
  { time: 115.43, text: "I SEND THE SWARM", type: "chorus-background", character: "god" },
  { time: 117.30, text: "I SEND THE HORDE", type: "chorus-background", character: "god" },
  { time: 119.50, text: "Then let my heart be hardened", type: "narrative-ramses", character: "ramses" },
  { time: 121.40, text: "And never mind how high the cost may grow", type: "narrative-ramses", character: "ramses" },
  { time: 124.40, text: "This will still be so", type: "narrative-ramses", character: "ramses" },
  { time: 126.00, text: "I will never", type: "narrative-ramses", character: "ramses" },
  { time: 127.40, text: "LET", type: "narrative-ramses", character: "ramses" },
  { time: 128.40, text: "YOUR", type: "narrative-ramses", character: "ramses" },
  { time: 129.30, text: "PEOPLE", type: "narrative-ramses", character: "ramses" },
  { time: 131.60, text: "GO", type: "narrative-ramses", character: "ramses" },
  { time: 132.30, text: "THUS SAITH THE LORD", type: "chorus", character: "god" },
  { time: 134.00, text: "THUS SAITH THE LORD", type: "chorus", character: "moses" },
  { time: 137.00, text: "I WILL NOT", type: "narrative-ramses-final", character: "ramses" },
  { time: 138.70, text: "LET", type: "narrative-ramses-final", character: "ramses" },
  { time: 140, text: "YOUR", type: "narrative-ramses-final", character: "ramses" },
  { time: 140.70, text: "MY", type: "narrative-ramses-final", character: "moses" },
  { time: 141.36, text: "PEOPLE", type: "narrative-ramses-final", character: "ramses" },
  { time: 144.26, text: "GO.", type: "narrative-ramses-final", character: "ramses" },
  { time: 152.26, text: "", type: "narrative-ramses-final", character: "ramses" },
];

class PlagueParticleSystem {
  constructor(type = 'insects', intensity = 1) {
    this.type = type;
    this.intensity = constrain(intensity, 0.6, 2.5);
    this.age = 0;
    this.maxAge = 180;
    this.particles = [];
    this.spawnParticles();
  }
  
  spawnParticles() {
    let count = floor(50 * this.intensity); 
    for (let i = 0; i < count; i++) {
      this.particles.push(this.createParticle());
    }
  }
  
  createParticle() {
    let p = {
      x: random(-width/2, width/2),
      y: random(-height/2, height/2),
      vx: random(-2, 2),
      vy: random(-2, 2),
      size: random(8, 25) * this.intensity, 
      life: 255,
      decay: random(0.8, 2) 
    };
    
    switch(this.type) {
      case 'insects':
        p.vx *= 1.5; p.vy *= 1.5;
        p.wobble = random(TWO_PI);
        p.wobbleSpeed = random(0.1, 0.3);
        break;
      case 'locusts':
        p.vy = random(-8, -3); 
        p.vx = random(-1, 1);
        break;
      case 'fire':
        p.vy = random(-6, -2); 
        p.vx = random(-0.5, 0.5);
        p.glow = random(10, 30);
        break;
      case 'hail':
        p.vy = random(3, 8);
        p.vx = random(-2, 2);
        p.rotation = random(TWO_PI);
        p.rotSpeed = random(-0.2, 0.2);
        p.size *= 2.5;
        break;
      case 'darkness':
        p.vx *= 0.3; p.vy *= 0.3;
        p.pulse = random(TWO_PI);
        break;
      case 'thunder':
        p.vx = random(-5, 5);
        p.vy = random(-5, 5);
        p.trail = [];
        break;
    }
    return p;
  }
  
  update() {
    this.age++;
    
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      
      let distToCenter = dist(p.x, p.y, 0, 0);
      if (distToCenter < 400) {
        let angle = atan2(p.y, p.x);
        let repelForce = map(400 - distToCenter, 0, 400, 0, 3);
        p.vx += cos(angle) * repelForce;
        p.vy += sin(angle) * repelForce;
      }

      p.x += p.vx;
      p.y += p.vy;
      p.life -= p.decay;
      
      switch(this.type) {
        case 'insects':
          p.wobble += p.wobbleSpeed;
          p.x += sin(p.wobble) * 2;
          break;
        case 'fire':
          p.vx += random(-0.3, 0.3);
          p.vy -= 0.1;
          break;
        case 'hail':
          p.rotation += p.rotSpeed;
          p.vy += 0.2; 
          break;
        case 'darkness':
          p.pulse += 0.1;
          p.size = p.size + sin(p.pulse) * 2;
          break;
        case 'thunder':
          if (p.trail) p.trail.push({x: p.x, y: p.y});
          if (p.trail && p.trail.length > 8) p.trail.shift();
          break;
      }
      
      if (p.life <= 0 || abs(p.x) > width || abs(p.y) > height) {
        this.particles.splice(i, 1);
      }
    }
  }
  
  display() {
    push();
    translate(width/2, height/2);
    
    for (let p of this.particles) {
      push();
      translate(p.x, p.y);
      
      let alpha = p.life;
      
      switch(this.type) {
        case 'insects':
          fill(100, 80, 50, alpha);
          noStroke();
          ellipse(0, 0, p.size);
          stroke(100, 80, 50, alpha * 0.5);
          line(-p.size/2, 0, p.size/2, 0);
          break;
        case 'locusts':
          fill(150, 200, 80, alpha);
          noStroke();
          ellipse(0, 0, p.size, p.size * 1.5);
          stroke(150, 200, 80, alpha * 0.7);
          line(-p.size, -p.size/2, p.size, -p.size/2);
          break;
        case 'fire':
          noStroke();
          fill(255, 150, 0, alpha);
          ellipse(0, 0, p.size);
          fill(255, 50, 0, alpha * 0.6);
          ellipse(0, 0, p.size * 0.6);
          if (p.glow) {
            fill(255, 200, 100, alpha * 0.2);
            ellipse(0, 0, p.size * 2);
          }
          break;
        case 'hail':
          rotate(p.rotation);
          stroke(150, 200, 255, alpha);
          strokeWeight(2);
          noFill();
          beginShape();
          for (let i = 0; i < 6; i++) {
            let a = TWO_PI / 6 * i;
            vertex(cos(a) * p.size, sin(a) * p.size);
          }
          endShape(CLOSE);
          break;
        case 'darkness':
          noStroke();
          fill(30, 20, 50, alpha);
          ellipse(0, 0, p.size);
          fill(0, 0, 0, alpha * 0.5);
          ellipse(0, 0, p.size * 1.5);
          break;
        case 'thunder':
          stroke(255, 255, 100, alpha);
          strokeWeight(3);
          if (p.trail && p.trail.length > 1) {
            for (let i = 1; i < p.trail.length; i++) {
              let prev = p.trail[i-1];
              let curr = p.trail[i];
              line(prev.x - p.x, prev.y - p.y, curr.x - p.x, curr.y - p.y);
            }
          }
          noStroke();
          fill(255, 255, 200, alpha);
          ellipse(0, 0, p.size);
          break;
      }
      pop();
    }
    pop();
  }
  
  isDone() { 
    return this.age > this.maxAge || this.particles.length === 0; 
  }
}

/* ========== SETUP ========== */
function preload() {
  sound = loadSound('plagues.mp3', () => {}, (e) => { console.warn('Error audio', e); });
  vigImg = loadImage(VIG_PATH, () => {}, (e) => { console.warn('vig image not found:', e); });
}

function setup() {
  canvas = createCanvas(windowWidth, windowHeight);
  fft = new p5.FFT(0.8, 1024);
  kaleidoAngle = 360 / kaleidoSymmetry;
  
  setupSerial();
  setupSocket();
  setupUI();
  
  textAlign(CENTER, CENTER);
  angleMode(DEGREES);
  frameRate(60);

  lastAutoSpawn = millis();
  createVignette();
}

function setupSerial() {
  port = createSerial();
  connectBtn = createButton('🎮 Conectar micro:bit');
  connectBtn.position(20, 70);
  connectBtn.style('padding', '10px 16px');
  connectBtn.style('background', '#4CAF50');
  connectBtn.style('color', 'white');
  connectBtn.style('border', 'none');
  connectBtn.style('border-radius', '8px');
  connectBtn.style('cursor', 'pointer');
  connectBtn.style('font-weight', 'bold');
  connectBtn.style('z-index', '1003');
  connectBtn.mousePressed(connectBtnClick);
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open('MicroPython', 115200);
    addDebug('Intentando conectar...');
  } else {
    port.close();
    microbitConnected = false;
    addDebug('Desconectado del micro:bit');
  }
}

function setupSocket() {
  socket = io();
  socket.on('connect', () => {
    socket.emit('client-type', 'desktop');
  });
  socket.on('plague-incoming', (data) => {
    addDebug('Plague incoming: ' + data.type);
    enqueuePlague(data.type || 'insects', data.intensity || 1);
  });
  socket.on('disconnect', () => addDebug('Desconectado'));
}

function setupUI() {
  let playBtn = document.getElementById('playBtn');
  if (playBtn) playBtn.addEventListener('click', togglePlay);
}

function createVignette() {
  try {
    if (!document.getElementById('vignette-overlay-img')) {
      const img = document.createElement('img');
      img.id = 'vignette-overlay-img';
      img.src = VIG_PATH;

      img.style.position = 'fixed';
      img.style.left = '0';
      img.style.top = '0';
      img.style.width = '100%';
      img.style.height = '100%';
      img.style.pointerEvents = 'none';
      img.style.zIndex = '9999';
      img.style.objectFit = 'cover';
      img.style.mixBlendMode = 'normal'; 
      img.draggable = false;
      document.body.appendChild(img);
      vigOverlayEl = img;
    }
  } catch (e) {
    console.warn('No pude crear overlay vig:', e);
  }
}

/* ========== MICRO:BIT SERIAL READING ========== */
function readMicrobitData() {
  if (!port.opened()) return;
  
  let str = port.readUntil("\n");
  
  if (str.length > 0) {
    if (!microbitConnected) {
      microbitConnected = true;
      addDebug('✅ Micro:bit conectado!');
      connectBtn.html('✅ Conectado');
    }
    
    let line = str.trim();
    if (line.length === 0) return;
    
    // Parse tilt data
    if (line.startsWith('P')) {
      let pitch = parseInt(line.substring(1));
      if (!isNaN(pitch)) {
        // Apply dead zone
        if (abs(pitch) < 5) pitch = 0;
        // Map pitch to camera Y offset (inverted for natural feeling)
        targetCameraY = map(pitch, -90, 90, -CAMERA_MAX_OFFSET, CAMERA_MAX_OFFSET);
      }
    } else if (line.startsWith('R')) {
      let roll = parseInt(line.substring(1));
      if (!isNaN(roll)) {
        // Apply dead zone
        if (abs(roll) < 5) roll = 0;
        // Map roll to camera X offset
        targetCameraX = map(roll, -90, 90, -CAMERA_MAX_OFFSET, CAMERA_MAX_OFFSET);
      }
    } else if (line === 'SHAKE') {
      // Trigger flash effect!
      triggerFlash();
      addDebug('💥 SHAKE detected!');
    }
  }
}

function triggerFlash() {
  pulseFrames = 25;
  pulseIntensity = 0.15;
  shakeFrames = 8;
  shakeMag = 18;
}

/* ========== GESTIÓN DE PLAGAS ========== */
function enqueuePlague(type, intensity) {
  if (plagueQueue.length < MAX_ACTIVE_PLAGUES) {
    plagueQueue.push(new PlagueParticleSystem(type, intensity));
  } else {
    pendingPlagues.push({ type, intensity });
    addDebug('Queued: ' + type);
  }
}

function trySpawnFromPending() {
  if (pendingPlagues.length > 0 && plagueQueue.length < MAX_ACTIVE_PLAGUES) {
    const next = pendingPlagues.shift();
    plagueQueue.push(new PlagueParticleSystem(next.type, next.intensity));
  }
}

/* ========== DETECCIÓN DE BEATS ========== */
function detectBeatAndSetShake(bass) {
  let threshold = 180;
  if (bass > threshold && previousBass <= threshold) {
    shakeFrames = 10; 
    shakeMag = map(bass, threshold, 255, 6, 28);
    pulseFrames = 18;
    pulseIntensity = map(bass, threshold, 255, 0.02, 0.12);
    addDebug('BEAT! bass=' + floor(bass));
  }
  previousBass = bass;
}

/* ========== MAIN DRAW ========== */
/* ========== MAIN DRAW ========== */
function draw() {
  // Read micro:bit data
  readMicrobitData();
  
  // Update camera position with easing
  cameraOffsetX = lerp(cameraOffsetX, targetCameraX, CAMERA_EASE);
  cameraOffsetY = lerp(cameraOffsetY, targetCameraY, CAMERA_EASE);
  
  // Análisis de audio
  const audioData = getAudioData();
  
  // Detectar beats
  detectBeatAndSetShake(audioData.bass);

  // Actualizar efectos
  updatePulseEffect();
  updateBackground(audioData.bass, audioData.mid, audioData.treble);
  
  // CLEAR BACKGROUND PROPERLY
  push();
  resetMatrix();
  drawBackground();
  pop();
  
  // Aplicar transformaciones visuales
  applyVisualTransformations();
  
  // Dibujar elementos (these are affected by camera movement)
  handleAutoSpawn();
  drawKaleidoscope(audioData.bass, audioData.mid, audioData.treble);
  drawPlagues();
  displayLyrics((sound && sound.isPlaying()) ? sound.currentTime() : 0, audioData.bass, audioData.mid, audioData.treble); // MOVED HERE!
  
  pop(); // Cerrar el push() de applyVisualTransformations
  
  // Draw effects that should be fullscreen (not affected by camera)
  push();
  resetMatrix();
  drawMotionBlur();
  drawFlashEffect();
  drawDebugInfo();
  pop();
}

function getAudioData() {
  let bass = 0, mid = 0, treble = 0;
  if (sound && sound.isLoaded()) {
    fft.analyze();
    bass = fft.getEnergy("bass");
    mid = fft.getEnergy("mid");
    treble = fft.getEnergy("treble");
  }
  return { bass, mid, treble };
}

function updatePulseEffect() {
  if (pulseFrames > 0) {
    pulseFrames--;
  } else {
    pulseIntensity = 0;
  }
}

function updateBackground(bass, mid, treble) {
  let currentTime = (sound && sound.isPlaying()) ? sound.currentTime() : 0;
  updateBackgroundColorByTime(currentTime);

  let dynamicR = map(bass, 0, 255, 5, 200) * 0.18;
  let dynamicG = map(mid, 0, 255, 5, 140) * 0.12;
  let dynamicB = map(treble, 0, 255, 20, 240) * 0.12;
  
  targetBgColor[0] = constrain(targetBgColor[0] + dynamicR, 0, 255);
  targetBgColor[1] = constrain(targetBgColor[1] + dynamicG, 0, 255);
  targetBgColor[2] = constrain(targetBgColor[2] + dynamicB, 0, 255);

  const lerpF = 0.06;
  bgColor[0] = lerp(bgColor[0], targetBgColor[0], lerpF);
  bgColor[1] = lerp(bgColor[1], targetBgColor[1], lerpF);
  bgColor[2] = lerp(bgColor[2], targetBgColor[2], lerpF);
}

function applyVisualTransformations() {
  push();

  // Calcular shake offset
  let sx = 0, sy = 0;
  if (shakeFrames > 0) {
    shakeFrames--;
    sx = random(-shakeMag, shakeMag);
    sy = random(-shakeMag, shakeMag);
    shakeMag *= 0.92;
  }

  // Calcular pulse scale
  let basePulse = 1 + pulseIntensity * (pulseFrames / 18);
  translate(width / 2, height / 2);
  scale(basePulse);
  translate(-width / 2, -height / 2);

  // Aplicar shake + camera offset
  translate(sx + cameraOffsetX, sy + cameraOffsetY);
}

function drawBackground() {
  let currentTime = (sound && sound.isPlaying()) ? sound.currentTime() : 0;
  let curr = getCurrentLyric(currentTime);
  
  for (let y = 0; y < height; y++) {
    let t = y / height;
    let r, g, b;
    
    if (curr && curr.character === 'ramses') {
      r = lerp(5, 220, t);
      g = lerp(0, 0, t);
      b = lerp(0, 0, t);
    } else {
      r = lerp(bgColor[0], bgColor[0] * 0.5, t);
      g = lerp(bgColor[1], bgColor[1] * 0.3, t);
      b = lerp(bgColor[2], bgColor[2] * 0.6, t);
    }
    stroke(r, g, b);
    line(0, y, width, y);
  }
  noStroke();
}

function handleAutoSpawn() {
  let currentTime = (sound && sound.isPlaying()) ? sound.currentTime() : 0;
  let curr = getCurrentLyric(currentTime);
  
  if (isPlaying && curr && (curr.character === 'god' || curr.character === 'ramses')) {
    if (millis() - lastAutoSpawn >= AUTO_SPAWN_INTERVAL) {
      lastAutoSpawn = millis();
      if (curr.character === 'god') {
        enqueuePlague('fire', 1.0); 
        addDebug('Auto-spawn: fire (god)');
      } else if (curr.character === 'ramses') {
        enqueuePlague('darkness', 1.0);
        enqueuePlague('fire', 1.0);
        addDebug('Auto-spawn: darkness+fire (ramses)');
      }
    }
  }
}

function drawKaleidoscope(bass, mid, treble) {
  let currentTime = (sound && sound.isPlaying()) ? sound.currentTime() : 0;
  let curr = getCurrentLyric(currentTime);
  
  if (curr && curr.character !== 'god') {
    push();
    translate(width/2, height/2);
   
    let speed, shapeType, strokeW, colorBase;
    if (curr.character === 'moses') {
      kaleidoSymmetry = 6;
      shapeType = 'curves';
      strokeW = map(mid, 0, 255, 1, 3);
      colorBase = [180, 200, 255];
    } else {
      kaleidoSymmetry = 8;
      shapeType = 'sharp';
      strokeW = map(bass, 0, 255, 2, 5);
      colorBase = [200, 0, 0];
    }
    
    kaleidoAngle = 360 / kaleidoSymmetry;
    for (let i = 0; i < kaleidoSymmetry; i++) {
      rotate(kaleidoAngle);
      if (shapeType === 'curves') {
        drawSmoothShape(bass, mid, treble, colorBase, strokeW);
      } else {
        drawSharpShape(bass, mid, treble, colorBase, strokeW);
      }
      push();
      scale(1, -1);
      if (shapeType === 'curves') {
        drawSmoothShape(bass, mid, treble, colorBase, strokeW);
      } else {
        drawSharpShape(bass, mid, treble, colorBase, strokeW);
      }
      pop();
    }
    pop();
  }
}

function drawSmoothShape(bass, mid, treble, colorBase, strokeW) {
  let radius = map(bass, 0, 255, 400, 800);
  let offset = map(mid, 0, 255, 0, 150);
  stroke(colorBase[0], colorBase[1], colorBase[2], 150);
  strokeWeight(strokeW);
  noFill();
  beginShape();
  for (let a = 0; a < 360; a += 10) {
    let r = radius + sin(a * 3 + frameCount * 0.5) * offset;
    let x = cos(a) * r;
    let y = sin(a) * r;
    curveVertex(x, y);
  }
  endShape(CLOSE);
  
  let innerRadius = map(treble, 0, 255, 100, 400);
  stroke(colorBase[0] + 30, colorBase[1] + 30, colorBase[2] + 30, 100);
  strokeWeight(strokeW * 0.5);
  line(0, 0, cos(frameCount * 2) * innerRadius, sin(frameCount * 2) * innerRadius);
}

function drawSharpShape(bass, mid, treble, colorBase, strokeW) {
  let radius = map(bass, 0, 255, 950, 1250);
  let spikes = max(3, floor(map(treble, 0, 255, 3, 8)));
  stroke(colorBase[0], colorBase[1], colorBase[2], 220);
  strokeWeight(strokeW * 1.5);
  noFill();
  beginShape();
  for (let i = 0; i < spikes; i++) {
    let angle = 360 / spikes * i + frameCount * 0.8;
    let r = i % 2 === 0 ? radius : radius * 0.4;
    let x = cos(angle) * r;
    let y = sin(angle) * r;
    vertex(x, y);
  }
  endShape(CLOSE);
}

function drawPlagues() {
  for (let i = plagueQueue.length - 1; i >= 0; i--) {
    plagueQueue[i].update();
    plagueQueue[i].display();
    if (plagueQueue[i].isDone()) {
      plagueQueue.splice(i, 1);
      trySpawnFromPending();
    }
  }
}

function drawFlashEffect() {
  if (pulseIntensity > 0.015) { 
    push();
    resetMatrix(); // Make sure flash covers whole screen
    
    let flashAlpha = map(pulseIntensity, 0.015, 0.18, 40, 160);
    flashAlpha = constrain(flashAlpha, 0, 220);
    
    // Check current character for color
    let currentTime = (sound && sound.isPlaying()) ? sound.currentTime() : 0;
    let curr = getCurrentLyric(currentTime);
    
    noStroke();
    
    // Blue flash for Moses, yellow for everyone else
    if (curr && curr.character === 'moses') {
      fill(80, 150, 255, flashAlpha); // Blue flash
    } else if (curr && curr.character === 'ramses') {
      fill(255, 20, 20, flashAlpha); // Red flash
    } else {
      fill(255, 200, 80, flashAlpha); // Yellow flash
    }
    
    rect(0, 0, width, height);
    pop();
  }
}

function drawMotionBlur() {
  // Create intentional motion blur based on camera movement
  let motionSpeed = abs(cameraOffsetX - targetCameraX) + abs(cameraOffsetY - targetCameraY);
  
  if (motionSpeed > 2) { // Only show blur when moving
    push();
    let blurAlpha = map(motionSpeed, 2, 50, 0, 35);
    blurAlpha = constrain(blurAlpha, 0, 35);
    
    // Direction of movement
    let dirX = targetCameraX - cameraOffsetX;
    let dirY = targetCameraY - cameraOffsetY;
    let dirMag = sqrt(dirX * dirX + dirY * dirY);
    
    if (dirMag > 0.1) {
      dirX /= dirMag;
      dirY /= dirMag;
      
      // Draw motion lines
      noFill();
      for (let i = 0; i < 8; i++) {
        let offset = i * 8;
        stroke(255, 255, 255, blurAlpha / (i + 1));
        strokeWeight(1);
        
        // Draw subtle lines in direction of motion
        for (let j = 0; j < 50; j++) {
          let x = random(width);
          let y = random(height);
          let len = map(motionSpeed, 2, 50, 5, 25);
          line(x - dirX * offset, y - dirY * offset, 
               x - dirX * (offset + len), y - dirY * (offset + len));
        }
      }
    }
    pop();
  }
}

function drawDebugInfo() {
  push();
  fill(255, 255, 255, 200);
  noStroke();
  textAlign(LEFT, TOP);
  textSize(12);
  textFont('monospace');
  
  let debugY = 120;
  text(`Camera: X=${floor(cameraOffsetX)} Y=${floor(cameraOffsetY)}`, 20, debugY);
  debugY += 18;
  text(`Target: X=${floor(targetCameraX)} Y=${floor(targetCameraY)}`, 20, debugY);
  debugY += 18;
  
  if (microbitConnected) {
    fill(100, 255, 100, 200);
    text('🎮 Micro:bit activo', 20, debugY);
  } else {
    fill(255, 100, 100, 200);
    text('🎮 Micro:bit desconectado', 20, debugY);
  }
  
  pop();
}

/* ========== BACKGROUND Y LYRICS ========== */
function updateBackgroundColorByTime(time) {
  let curr = getCurrentLyric(time);
  if (curr && curr.character === 'god') {
    targetBgColor = [139, 0, 0];
  } else if (time < 34.58) {
    targetBgColor = [139, 0, 0];
  } else if (time < 60.67) {
    targetBgColor = [2, 15, 40];
  } else if (time < 82.27) {
    targetBgColor = [20, 50, 100];
  } else if (time < 106.94) {
    targetBgColor = [50, 80, 140];
  } else if (time < 132.30) {
    targetBgColor = [180, 0, 0];
  } else {
    targetBgColor = [139, 0, 0];
  }
}

function getCurrentLyric(time) {
  for (let i = lyrics.length - 1; i >= 0; i--) {
    if (time >= lyrics[i].time) return lyrics[i];
  }
  return null;
}

/* ========== LYRICS DOM ========== */
function updateVisualStyle(character) {
  const body = document.body;
  const overlay = document.getElementById('lyric-overlay');

  body.classList.remove('god', 'moses', 'ramses', 'default');
  overlay.classList.remove('god', 'moses', 'ramses', 'default');

  if (character === 'god') {
    body.classList.add('god');
    overlay.classList.add('god');
  } else if (character === 'moses') {
    body.classList.add('moses');
    overlay.classList.add('moses');
  } else if (character === 'ramses') {
    body.classList.add('ramses');
    overlay.classList.add('ramses');
  } else {
    body.classList.add('default');
    overlay.classList.add('default');
  }
}

function updateLyricsDOM(time, bass, mid, treble) {
  const overlay = document.getElementById('lyric-overlay');
  if (!overlay) return;

  const curr = getCurrentLyric(time);
  if (!curr) {
    overlay.style.opacity = '0';
    updateVisualStyle('default');
    return;
  }

  let baseSizePx = Math.round(Math.min(window.innerWidth * 0.06, 72));
  if (curr.character === 'moses') baseSizePx = Math.round(Math.min(window.innerWidth * 0.048, 56));
  if (curr.character === 'ramses') baseSizePx = Math.round(Math.min(window.innerWidth * 0.052, 64));
  if (curr.character === 'god') baseSizePx = Math.round(Math.min(window.innerWidth * 0.06, 72));

  overlay.classList.remove('small','medium','large','xlarge');
  if (baseSizePx < 36) overlay.classList.add('small');
  else if (baseSizePx < 52) overlay.classList.add('medium');
  else if (baseSizePx < 78) overlay.classList.add('large');
  else overlay.classList.add('xlarge');

  let pulse = 1 + (pulseIntensity || 0) * 6;
  let vibrX = Math.round(map(treble, 0, 255, -6, 6));
  let vibrY = Math.round(map(treble, 0, 255, -4, 4));

  // PARALLAX: Move lyrics opposite to camera (but less)
  let parallaxX = -cameraOffsetX * 0.15;
  let parallaxY = -cameraOffsetY * 0.15;

  // FLOATING TILT: Subtle sine wave rotation
  let floatTilt = Math.sin(frameCount * 0.02) * 1.5; // 1.5 degrees max tilt

  overlay.style.transform = `translate(-50%,-50%) scale(${pulse}) translate(${vibrX + parallaxX}px, ${vibrY + parallaxY}px) rotate(${floatTilt}deg)`;

  let idx = lyrics.indexOf(curr);
  let dur = 1.8;
  if (idx + 1 < lyrics.length) dur = Math.max(1.1, lyrics[idx + 1].time - curr.time);
  let since = time - curr.time;
  let alpha = 1;
  if (since > dur - 0.3) alpha = map(since, dur - 0.3, dur, 1, 0);
  overlay.style.opacity = alpha;

  overlay.querySelector('.line').textContent = curr.text;
  updateVisualStyle(curr.character);
}

function drawRepeatedText(textString) {
  push();
  fill(0, 0, 0, 80); 
  textSize(42);
  textFont('Anton, Arial');
  rotate(-0.15);
  for (let y = -height*1.5; y < height*2.5; y += 85) {
    for (let x = -width*1.5; x < width*2.5; x += 520) {
      push();
      translate(x + (frameCount*0.7)%520, y + sin(frameCount*0.02 + x*0.001)*10);
      rotate(sin(frameCount*0.012 + x*0.0005) * 0.05);
      text(textString, 0, 0);
      pop();
    }
  }
  pop();
}

function displayLyrics(time, bass, mid, treble) {
  updateLyricsDOM(time, bass, mid, treble);
  
  const curr = getCurrentLyric(time);
  if (!curr) return;

  if (curr.character === 'god' || curr.type === 'narrative-ramses-final') {
    drawRepeatedText(curr.text);
  }
}

/* ========== UTILIDADES ========== */
function togglePlay() {
  if (!sound || !sound.isLoaded()) return addDebug('Audio no cargado');
  if (isPlaying) {
    sound.pause();
    isPlaying = false;
    let btn = document.getElementById('playBtn');
    if (btn) btn.textContent = 'play B)';
  } else {
    sound.play();
    isPlaying = true;
    let btn = document.getElementById('playBtn');
    if (btn) btn.textContent = 'pausar';
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}

function addDebug(msg) { 
  debugMessages.unshift(msg); 
  if (debugMessages.length > 12) debugMessages.pop(); 
}
```
### 🌿 **index.hmtl**
```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>The Plagues</title>

  <!-- p5, p5.sound, p5.web-serial y socket.io -->
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/addons/p5.sound.min.js"></script>
  <script src="https://unpkg.com/@gohai/p5.webserial@^1/libraries/p5.webserial.js"></script>
  <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>

  <!-- Fuentes -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Anton&family=Cinzel:wght@400;700&display=swap" rel="stylesheet">

  <style>
    html,body {
      height: 100%; margin: 0;
      background: #000;
      overflow: hidden;
      font-family: 'Anton', Arial, sans-serif;
      transition: background 0.8s ease;
    }

    canvas { display:block; }

    .overlay {
      position: absolute; left:12px; top:12px; z-index:1002;
      color: #fff; background: rgba(0,0,0,0.45);
      padding:8px 12px; border-radius:8px; font-size:14px;
    }

    #controls {
      position:absolute; right:12px; bottom:18px; z-index:1002;
    }

    #playBtn {
      background:#ff5b5b; border:none; color:white;
      padding:10px 16px; border-radius:8px;
      cursor:pointer; font-weight:bold;
      transition: filter 0.2s ease;
      font-family: 'Anton', Arial, sans-serif;
    }

    #playBtn:hover { filter:brightness(1.05); }

    /* --- Lyrics overlay (center) --- */
    #lyric-overlay {
      position: absolute;
      z-index: 10050;
      left: 50%; top: 50%;
      transform: translate(-50%, -50%);
      width: 72vw; max-width: 1400px;
      pointer-events: none;
      text-align: center;
      line-height: 1.05;
      white-space: pre-wrap;
      text-wrap: balance;
      transition: color 0.25s ease, text-shadow 0.25s ease, font-family 0.25s ease, transform 0.12s ease;
    }

    #lyric-overlay.small { font-size: 28px; }
    #lyric-overlay.medium { font-size: 44px; }
    #lyric-overlay.large { font-size: 64px; }
    #lyric-overlay.xlarge { font-size: 92px; }

    #lyric-overlay .line {
      display: inline-block;
      -webkit-font-smoothing: antialiased;
      text-rendering: optimizeLegibility;
      transition: filter 120ms linear, text-shadow 120ms linear;
      will-change: text-shadow, filter, transform;
      -webkit-text-stroke: 0.6px rgba(0,0,0,0.25);
    }

    #lyric-overlay.moses {
      font-family: "Cinzel", serif;
    }
    
    #lyric-overlay.moses .line {
      color: #b4d5ff;
      text-shadow:
        0 0 6px rgba(150,200,255,0.9),
        0 0 18px rgba(100,180,255,0.6),
        0 0 36px rgba(80,160,255,0.35);
      filter: drop-shadow(0 6px 18px rgba(0,30,60,0.45));
    }

    #lyric-overlay.ramses {
      font-family: "Anton", sans-serif;
    }

    #lyric-overlay.ramses .line {
      color: #ff3333;
      text-shadow:
        0 0 8px rgba(255,70,70,0.95),
        0 0 22px rgba(255,30,30,0.7),
        0 0 48px rgba(255,40,40,0.36);
      filter: drop-shadow(0 6px 20px rgba(60,0,0,0.5));
    }

    #lyric-overlay.god {
      font-family: "Anton", sans-serif;
    }

    #lyric-overlay.god .line {
      color: #ffd88c;
      text-shadow:
        0 0 8px rgba(255,230,180,0.95),
        0 0 28px rgba(255,200,100,0.7),
        0 0 60px rgba(255,160,60,0.36);
      filter: drop-shadow(0 8px 26px rgba(60,40,0,0.55));
    }

    #lyric-overlay.default {
      font-family: "Cinzel", serif;
    }

    #lyric-overlay.default .line {
      color: #fff0d6;
      text-shadow:
        0 0 6px rgba(255,255,255,0.6),
        0 0 14px rgba(255,255,255,0.28);
      filter: drop-shadow(0 6px 14px rgba(0,0,0,0.32));
    }

    body.moses { background: radial-gradient(circle at center, #001d3d, #000); }
    body.ramses { background: radial-gradient(circle at center, #300, #000); }
    body.god { background: radial-gradient(circle at center, #3a2800, #000); }
    body.default { background: radial-gradient(circle at center, #000, #000); }
  </style>
</head>

<body class="default">
  <div id="lyric-overlay" class="default medium"><span class="line"></span></div>
  <div id="controls"><button id="playBtn">Play</button></div>

  <script src="sketch.js"></script>
</body>
</html>
```
___
# ⭐ **MI AUTOEVALUACIÓN:** 5.0

🌱 **Actividad 1:** completada 100%.  
- Documenté mis referentes.  
- Expliqué mis decisiones creativas.   
- Justifiqué y expliqué por qué elegí las funciones para el celular y el micro:bit.  
- Hice bocetos de las interfaces.  
- Realicé un diagrama que explicara la comunicación entre los componentes.  

🌱 **Apply:** completada 100% y totalmente funcional.  

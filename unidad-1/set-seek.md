# Unidad 1

## 🔎 Fase: Set + Seek

### 📝 Actividad 01

**¿Qué es un sistema físico interactivo?**  
> 🌱Una combinación de hardware y software que captan un input (video, tableta digitalizadora, sonido, sliders, knobs, trackers...), lo procesan en tiempo real y generan un output visual, auditivo, etc. Permite una interacción directa entre los humanos y la tecnología. Al ser en tiempo real, logran adaptarse y generar una experiencia única en cada interacción particular.

___
︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶  

**¿Cómo podrías aplicar lo que has visto en tu perfil profesional?**
> 🌿Mi proyecto soñado siempre ha sido conseguir una manera de permitirle al usuario interactuar directamente con un corto animado. Quiero aprender sobre realidad aumentada, trackers, sensores, todas las herramientas que podrían incluirse en un trabajo así. Considero que la tecnología, los videojuegos y la música son medios extremandamente potentes para el desarrollo de ideas novedosas, que permitan amplificar las emociones experimentadas por un usuario. Si simplemente escuchar una canción, ver el video musical y leer la letra es capaz de provocar escalofríos en una persona, me emociona imaginarme lo que podría generar el sentirse no solo inmerso en los visuales y la historia, sino también tener la capacidad de interactuar con el entorno.
> 
> Entré a esta carrera porque los videojuegos, animaciones y todas las formas de arte han tenido un impacto gigantesco en mi vida, mis emociones, mis valores y personalidad. Yo misma he experimentado de primera mano lo que es sentirse movido hasta el punto del llanto por una melodía, una historia, un paisaje, una pintura...
> 
> Quiero crear productos que no se parezcan a lo común, sino explorar los límites de lo posible por medio de la mezcla entre algo tan humano como lo es el arte y algo tan poderoso como lo es la tecnología. Quiero inspirar a otras personas con mis creaciones, tal como otros lo hicieron conmigo cuando vi sus proyectos de pequeña (˶˃ ᵕ ˂˶)

```
  ∧,,,∧
 (• ⩊ •)
|￣U U￣￣￣￣￣￣￣￣￣￣￣￣￣￣￣￣￣￣|
|   Quiero aprender touch designer     |   
￣￣￣￣￣￣￣￣￣￣￣￣￣￣￣￣￣￣￣￣￣
```

___
︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶  
  
### 📝 Actividad 02

**¿Qué es el diseño/arte generativo?**
> 🌻Una colaboración entre humanos y la tecnología donde la persona establece unos parámetros, reglas y limitaciones para el sistema, dándole una dirección a sus acciones. Luego, con cierto nivel de autonomía, la máquina genera un resultado visual, auditivo, etc. En los ejemplos mostrados en clase, se observan los distintos grados de participación del humano en el producto final; la chica principalmente participaba al inicio al crear un repositorio de materiales, patrones y herramientas para que el programa trabajara solo, mientras que el chico interactuaba activamente e "intercambiaba" ideas con la máquina de cierta forma al dejarse guiar por los sonidos que producía.
  
**¿Cómo podrías aplicar lo que has visto en tu perfil profesional?**
> 🌼 Me atrae demasiado la posibilidad de implementar variaciones dentro de los gráficos para videojuegos por medio de arte generativo. Me parece que sería una manera brutal de agregar rejugabilidad, sobretodo en juegos que sean bastante pesados en cuanto a historia. Me parece que la industria en este momento se concentra demasiado en llevar los gráficos a ser lo más realistas posibles, y eso termina provocando que todos los productos en el mercado se vean igual 💔. Para mí, la parte visual y auditiva de un juego es la más importante para generar un impacto verdadero. Si el estilo está bien jalado, la manera en la que potencia la historia no tiene comparación. Estuve hablando hace unos días sobre la moda que está surgiendo de llevar a cabo conciertos virtuales con artistas dentro de videojuegos. Uno que me llamó bastante la atención fue el de Aurora (la chica de la canción de The Seed) en el juego [Sky: Children of The Light](https://www.youtube.com/watch?v=lzUg5ffOyOo). Un evento así sería impresionante mezclado con arte generativo que se fuera adaptando no solo a la música, sino tambien a la interacción de los usuarios.
  
___
︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶  
  
### 📝 Actividad 03

**Sacude el micro:bit. ¿Qué pasa?**  
> 🌿 El círculo en la pantalla se pone de color verde y se escribe la letra "C" dentro de él.

**Presiona el botón Send Love. ¿Qué pasa?**  
> 🌻 El display del micro:bit muestra un corazón por un momento cortito, y después cambia a una carita feliz.

**En este sistemas físico interactivo identifica los inputs, outputs y el proceso.**  
> 🌱INPUTS: Botones A y B, acelerómetro, botones en la aplicación, serial.

> 🌿PROCESO: El primer programa recibe el input de los botones físicos y acelerómetro en el micro:bit conectado, y controla la figura que se muestra en los LEDs. Al mismo tiempo, el segundo programa contiene una biblioteca que los comunica a ambos. Al obtener el input del primer programa, altera el color y la letra en el display con el círculo. Por otro lado, el segundo programa detecta el input de los botones virtuales y le manda una "h" al programa inicial, el cuál se encarga de mostrar el corazón y carita feliz en los LEDs.

> 🌻OUTPUTS: LEDs, circulito del programa que cambia de color y muestra una letra.
___

### 📝 Actividad 04  
Mi meta con este programa era:
>1. Aprender a utilizar audio dentro del programa (no me quería quedar con las ganas 💔)
>2. Agarrar el tiro de cómo funcionan los loops en p5.js (no fue nada distinto de lo que ya sabía... lo único diferente que noté fue el push() y pop())
>3. Ver cómo funcionaban los blend modes
>4. Programar algo que me sirviera como base para empezar a entender cómo replicar [visualizers viejitos de windows media player](https://www.youtube.com/watch?v=ntyKbTLrfxE) que tenía en mi pc xp 💔

Para esto, utilicé las funciones:
>- Seno: para la rotación de los óvalos.
>- Coseno: para cambiar el valor del canal verde sin input del usuario.
>- Random(): para cambiar el tamaño de los óvalos al azar y que generara esa apariencia de anillos como de saturno.
  
Fue muy divertido. Pasé la tarde completa solamente probando distintos valores para i y combinaciones con varias canciones. Mis ubicaciones favoritas para el mouse son arriba a la derecha, o fuera de la pantalla (ahí se nota más la rotación de los óvalos).
   
🌱 [Enlace](https://editor.p5js.org/EsTorrente/sketches/AWgfmq2NU)  

🌿 **INDEX.HMTL:**
```index.html
<!DOCTYPE html>
<html lang="en">
  <head>
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.8/lib/p5.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.8/lib/addons/p5.sound.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/addons/p5.sound.min.js"></script>
    <link rel="stylesheet" type="text/css" href="style.css">
    <meta charset="utf-8" />

  </head>
  <body>
    <main>
    </main>
    <script src="sketch.js"></script>
  </body>
</html>

```

🌻 **SKETCH.JS:**
```sketch.js
let cancion;
let fft;

function preload() {
  song = loadSound('BirthdaySuit.mp3'); 
}

// ===============================================

function setup() {
  createCanvas(windowWidth, windowHeight);
  angleMode(DEGREES);
  noFill();
  
  //audio
    fft = new p5.FFT();
  
  startAudio();
}

// ===============================================

function draw() {
  
  background(0, 20); //lo que mostraste en clase para el efecto de trail
  blendMode(ADD); // //muy fan, parece que brilla

  translate(width / 2, height / 2); //para que esté centrado
  
// AUDIO ==========================================
  
  let spectrum = fft.analyze();
  let bass = fft.getEnergy("bass");

// ROTAR ==========================================
  
  for (var i = 0; i < 90; i++) {
    push();

    var offset = map(mouseX, 0, width, -100, 100);
    rotate(sin(frameCount + i) * offset); //como sin() siempre me tira un valor entre -1 y 1, hay que multiplicarlo por el valor del offset para que la rotación sí se note
    
// COLORES =======================================
    
    var r = map(mouseX, 0, width, 100, 255); //color rojo depende de posición x de mouse
    var g = map(cos(frameCount / 2 + i), -1, 1, 50, 200); //cambio automático de verde
    var b = map(mouseY, 0, height, 100, 255); //color azul depende de posición y de mouse
    
    //uso map para decir que dependiendo de la posición del mouse, me tire un número equivalente dentro del rango de 100 a 255

// ESCALA =========================================
    
    let pulse = map(bass, 0, 255, 0.8, 3.5);
    
    stroke(r, g, b, 50);

    // para el elipse chiquito
    var w = 400 - i * 3 + random(-10, 10);
    var h = w * map(mouseY, 0, height, 0.5, 1.5) * pulse; //cambiar altura con mouse arriba/abajo
    
    // para el elipse exterior
    var w2 = 800 - i * 4 + random(-10, 10);
    var h2 = w * map(mouseX, 0, width, 0.5, 1.5) * pulse; //cambiar altura con mouse derecha/izquierda
    
    //usa el w del primer elipse para que se vea más interesante que con w2

    ellipse(0, 0, w, h);
    ellipse(0, 0, w2, h2);

    pop();
    
  }

  blendMode(BLEND);
}

function startAudio() {
  if (song && !song.isPlaying()) {
    song.play();
  }
}
```



<img width="4222" height="812" alt="image" src="https://github.com/user-attachments/assets/2758cb53-7382-4736-84fd-2c77dafee596" />


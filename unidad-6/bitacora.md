
# Evidencias de la unidad 6

### 📝 Actividad 1

🌱 **¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?**
Salió el siguiente mensaje:
```
added 120 packages, and audited 121 packages in 2s

17 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
npm notice
npm notice New major version of npm available! 10.9.3 -> 11.6.1
npm notice Changelog: https://github.com/npm/cli/releases/tag/v11.6.1
npm notice To update run: npm install -g npm@11.6.1
npm notice
```
> Agregó las dependencias necesarias para poder correr el programa. También avisan si hay actualizaciones disponibles.  

🌿 **¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?**
> `Server is listening on http://localhost:3000`. Indica que el servidor se inició correctamente y está funcionando en el puerto 3000. "localhost" significa que el servidor está corriendo en mi propio computador.  

🌼 **Describe lo que ves inicialmente en page1 y page2 en tu navegador.**
> Al abrir solamente page1, sale el mensaje de "esperando conexión de la otra ventana". Al abrir page2, ambas ventanas se actualizan y muestran solamente un círculo en el centro de la ventana, con un puntico negro en medio.

🌻 **¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?**
```
A user connected - ID: V-jH6Z_SBvW-i6aqAAAB
Received win1update from ID: V-jH6Z_SBvW-i6aqAAAB Data: { x: 0, y: 0, width: 1920, height: 945 }
Debug - Connected clients: 1, Page1: 1, Page2: 0, Synced: 0
Sync status: pages=false, synced=false, clients=1
Debug - Connected clients: 1, Page1: 1, Page2: 0, Synced: 1
Sync status: pages=false, synced=true, clients=1
A user connected - ID: wv40xecnLhN4r6QqAAAD
Received win2update from ID: wv40xecnLhN4r6QqAAAD Data: { x: 0, y: 0, width: 1920, height: 945 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
Sync status: pages=true, synced=false, clients=2
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
Sync status: pages=true, synced=false, clients=2
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
```
> El servidor detecta cada conexión, recibe los datos de posición de cada ventana, y muestra el proceso de sincronización hasta que ambas ventanas están completamente conectadas y sincronizadas.  

🌱 **Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?**
> Al mover una ventana, la línea que conecta los círculos se ajusta en tiempo real, reflejando la nueva posición relativa entre ambas ventanas. Los círculos mantienen su posición en el centro de sus respectivas ventanas, pero la línea cambia de longitud y dirección.
> `Consola del navegador:` muestra el estado actual de sincronización, el id del que se conecta, y los datos reomotos recibidos.  
<img width="681" height="275" alt="image" src="https://github.com/user-attachments/assets/16e8f3de-eae9-4b2a-a5aa-99009ba89da9" />  
<img width="685" height="182" alt="image" src="https://github.com/user-attachments/assets/ca65165b-fa77-4135-ac25-3e420b144b6a" />  
  
> `Terminal del servidor:` la misma que puse en la pregunta pasada. Muy similar.  

___
### 📝 Actividad 2

🌱 **Piensa en cómo te conectas a Internet en casa o en la Universidad. ¿Usas Wi-Fi? ¿Un cable de red? Eso es simplemente tu “rampa de acceso” a la gran red de carreteras. ¿Qué pasaría si esa rampa se corta? Anota tus ideas.**  
> En mi casa utilizo el wifi. En la universidad, algunos computadores están configurados con el internet y otro con el cable de red. Si esa conexión se corta, se impide el acceso al servidor. Mi guess es que, así como en mi PC puedo correr un localhost, alguien más está manteniendo un servidor enorme para el internet (los proveedores). Como todo debe ser pagado y controlado, los cables y el wifi no solamente permiten acceder al puerto, sino que son una garantía de que tienes permitido hacer uso de ellos. Por eso es que algunas de las licencias para programas en la universidad funcionan checkeando que el pc esté conectado por ethernet, o por eso es que es posible bannear de un juego cualquier cuenta por ip para impedir que cualquier persona acceda a él desde una conexión de internet específica.  

🌿 **¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?**  
> Cuando se va al médico, el cliente es el paciente y el servidor el doctor. Se pide un remedio o exámenes, se entrega una orden de lo que necesita reclamar/realizar para curarse.  
> Cuando me voy a hacer las uñas, yo soy el cliente y la manicurista el servidor. Se pide un diseño en las uñas, se entrega ese diseño finalizado.  

🌼 **Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.google.com) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?**  
>https://www.windows93.net/#!hampster
  
`Protocolo:` https://  
`Dominio:` www.windows93.net  
`Ruta:` /#!hampster  

> Si solo escribo el dominio, me llevaría a la home page (en el caso de esta página en específico, es la pantalla del PC sin abrir ninguna ventana). 

🌻 **Compara HTTP con los protocolos seriales que usaste. ¿Qué similitudes encuentras? ¿Qué diferencias clave ves? ¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?**
> No estoy muy segura, pero por lo que veo, tanto ASCII como HTML usan texto que sí puedo leer al mandar los datos. En cuanto a diferencias, el HTPP no utiliza solamente el cable directo al serial sino que toca manejar internet, sincronización de servidores, adaptarse a cualquier dispositivo desde el que se abra, etc. Todo eso lo hace mucho más complejo.  

🌱 **Piensa en una página web simple, como un formulario de login. ¿Qué parte crees que es HTML (ej. los campos de texto, el botón)? ¿Qué parte es CSS (ej. el color del botón, el tipo de letra)? ¿Qué parte es JavaScript (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de “contraseña incorrecta” que aparece sin recargar la página)?**
> Creo que el HTML sería la parte de definir los campos de datos que se ingresan, la estructura. Si hay botones, listas, checkbox, cosas así.    
> El CSS me imagino que serían el color del botón, el tipo de letra, el tamaño de los campos, los márgenes...  
> Y el JavaScript, la parte de validación de datos, de mensajes de error...  

🌿 **Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”. ¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web? ¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado?**
> una página web usualmente está diseñada para poder ser ejecutada de forma fluida desde la mayoría de dispositivos. Si una página tiene muchas interacciones, animaciones, cosas que calcular... llamarlo cada frame puede hacer que corra demasiado lento en algunos dispositivos, como celulares más viejitos. Usualmente eso se refleja en el tiempo de carga, y la página se queda congelada solamente con darle a un botón (o directamente se demora un motón en abrirse). No sería eficiente.

🌼 **¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?**
> Para los desarrolladores puede ser util porque es complejo aprender a ser competente en múltiples lenguajes. Así se puede contratar un equipo que esté más especializado en javascript, y pueden trabajar tanto en el cliente como en el navegador sin problemas. Además, me imagino que facilita la parte de programación, porque las funciones funcionan igual en ambos lados. No hay que preocuparse por adaptar recepción de datos de un lugar a otro y esas cosas.  

🌻 **Resume con tus propias palabras la diferencia fundamental entre una comunicación HTTP tradicional y una comunicación usando WebSockets/Socket.IO. ¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real?**
> Creo que en HTTP, la "conversación" entre cliente y servidor es mucho más extensa. Se deben pedir varios datos, explicar desde dónde se piden, especificar de qué tipo es cada archivo, etc en cada interacción. WebSockets se salta esa parte que toma tiempo y genera retraso, simplificándola para poder recibir y enviar datos de forma instantánea con una conexicón directa y una sola línea de código para recibir y enviar. Me imagino que se usaba en juegos como Club Penguin y todos los .io, en cosas como MySpace, Facebook, WhatsApp, google docs...

___
### 📝 Actividad 3

🌱 **Detén el servidor si está corriendo. Cambia la primera ruta de /page1 a /pagina_uno. Inicia el servidor. Intenta acceder a http://localhost:3000/page1. ¿Funciona? Ahora intenta acceder a http://localhost:3000/pagina_uno. ¿Funciona? ¿Qué te dice esto sobre cómo el servidor asocia URLs con respuestas? Restaura el código.**
> No, /page1 ya no funciona pero /pagina_uno sí. Me dice que el servidor utiliza la URL para saber a quién mandarle el request de ejecutar el js y html correspondiente.

🌿 **Asegúrate de que el servidor esté corriendo (npm start). Abre http://localhost:3000/page1 en una pestaña. Observa la terminal del servidor. ¿Qué mensaje ves? Anota el ID. Abre http://localhost:3000/page2 en OTRA pestaña. Observa la terminal. ¿Qué mensaje ves? ¿El ID es diferente? Cierra la pestaña de page1. Observa la terminal. ¿Qué mensaje ves? ¿Coincide el ID con el que anotaste? Cierra la pestaña de page2. Observa la terminal.**
> `Page1 ID:` A user connected - ID: ScyS1SRBIPNQ8pguAAAB
> `Page2 ID:` A user connected - ID: gBR4nZ2rH5VIRCykAAAF
> `Cerrar Page1:` User disconnected - ID: ScyS1SRBIPNQ8pguAAAB
> `Cerrar Page2:` User disconnected - ID: gBR4nZ2rH5VIRCykAAAF
> Sí, ambos IDs coinciden.  

🌼 **Inicia el servidor y abre page1 y page2. Mueve la ventana de page1. Observa la terminal del servidor. ¿Qué evento se registra (win1update o win2update)? ¿Qué datos (Data:) ves? Mueve la ventana de page2. Observa la terminal. ¿Qué evento se registra ahora? ¿Qué datos ves? Experimento clave: cambia socket.broadcast.emit(‘getdata’, page1); por socket.emit(‘getdata’, page1); (quitando broadcast). Reinicia el servidor, abre ambas páginas. Mueve page1. ¿Se actualiza la visualización en page2? ¿Por qué sí o por qué no? (Pista: ¿A quién le envía el mensaje socket.emit?). Restaura el código a broadcast.emit.**
> `Mover Page1:` Received win1update from ID: KJOROJ-q_VhNf1DwAAAB Data: { x: -4, y: 109, width: 237, height: 968 }  
> `Mover Page2:` Received win2update from ID: zHdk-5FsKF6bfvFnAAAF Data: { x: 937, y: 119, width: 159, height: 968 }  
> Al cambiar la línea de código, deja de actualizarse page2. socket.emit se envía el dato a sí mismo, mientras que broadcast.emit se lo manda a todos los clientes menos al que lo envía.  


🌻 **Detén el servidor. Cambia const port = 3000; a const port = 3001;. Inicia el servidor. ¿Qué mensaje ves en la consola? ¿En qué puerto dice que está escuchando? Intenta abrir http://localhost:3000/page1. ¿Funciona? Intenta abrir http://localhost:3001/page1. ¿Funciona? ¿Qué aprendiste sobre la variable port y la función listen? Restaura el puerto a 3000.**
> `Server is listening on http://localhost:3001`  
> http://localhost:3000/page1 ya no funciona. Me sale el mensaje de error `localhost refused to connect.`
> http://localhost:3001/page1 sí funciona. Port define dónde escucha el servidor, y server.listen inicia el server en ese puerto en específico. Es como que nos cambien de salón para la clase. Si yo llevo al 314 un viernes, no voy a poder ver la clase de sistemas físicos interactivos.  

___
### 📝 Actividad 4

🌱 **Abre page2.html en tu navegador (con el servidor corriendo). Abre la consola de desarrollador (F12). Detén el servidor Node.js (Ctrl+C). Refresca la página page2.html. Observa la consola del navegador. ¿Ves algún error relacionado con la conexión? ¿Qué indica? Vuelve a iniciar el servidor y refresca la página. ¿Desaparecen los errores?**
> Error que sale al desconectar:

<img width="700" height="58" alt="image" src="https://github.com/user-attachments/assets/60e39694-06eb-44ea-a208-b7cf803767cd" />

> Mensaje al reconectar: 
<img width="751" height="136" alt="image" src="https://github.com/user-attachments/assets/ad323b42-2884-450a-8f13-d43303c7ff4b" />
  
> Hay un error en el GET del script llamado `manager.js`. Efectivamente, este desaparece al volver a iniciar el servidor y refrescar. Lo que indica es que el cliente intenta conectarse al servidor pero no lo encuentra, mostrando que la comunicación depende completamente del servidor activo. Este es el script:  
<img width="829" height="583" alt="image" src="https://github.com/user-attachments/assets/681f460e-13f5-4ce7-8565-85bfa4de570e" />
  
🌿 **Comenta la línea socket.emit(‘win2update’, currentPageData, socket.id); dentro del listener connect. Reinicia el servidor y refresca page1.html y page2.html. Mueve la ventana de page2 un poco para que envíe una actualización. ¿Qué pasó? ¿Por qué?**
``
A user connected - ID: EYJDFhGbRZFCdga1AAAB
A user connected - ID: DQQRlrLOck6_rXLFAAAD
Received win1update from ID: DQQRlrLOck6_rXLFAAAD Data: { x: 0, y: 0, width: 808, height: 882 }
Debug - Connected clients: 2, Page1: 1, Page2: 0, Synced: 0
Sync status: pages=false, synced=false, clients=2
Debug - Connected clients: 2, Page1: 1, Page2: 0, Synced: 1
Sync status: pages=false, synced=false, clients=2
Debug - Connected clients: 2, Page1: 1, Page2: 0, Synced: 2
Sync status: pages=false, synced=true, clients=2
``
> Ambos clientes se conectaron, pero sólo se envió actualización de datos de la ventana 1. El debug indica que hay 2 clientes, pero solo está recibiendo datos de la página 1. En teoría están sincronizados, pero es que directamente no puede hacer la parte de dibujar la conexión porque no tiene la información necesaria para hacerlo.

🌼 **Asegúrate de tener este console.log en page2.js. Abre ambas páginas. Mueve la ventana de page1. Observa la consola del navegador de page2. ¿Qué datos muestra? Mueve la ventana de page2. Observa la consola de page1. ¿Qué pasa? ¿Por qué?**
> `Consola Page2:` Received valid remote data: {x: 100, y: 50, width: 800, height: 600}
> `Consola Page1:` Received valid remote data: { x: 937, y: 119, width: 159, height: 968 }
> Cada vez que una ventana se mueve, la otra recibe sus nuevos datos de posición en tiempo real.

🌻 **Observa checkWindowPosition() en page2.js y modifica el código del if para comprobar si el código dentreo de este se ejecuta. Mueve cada ventana y observa las consolas. ¿Qué puedes concluir y por qué?**
Agregué la línea `console.log('if funciona correctamente :)');` dentro del if. Cada frame que la ventana se moviera, se volvía a mandar el mensaje... lo que significa que el if se estaba ejecutando constantemente porque identificaba correctamente que las coordenadas anteriores eran distintas a las actuales. Mientras no se mueva, el mensaje no se manda. Por ende, ese código se corre solamente cuando es necesario... como el draw() en p5.js que se llama literal cada frame que corre el programa. Es más eficiente.    
<img width="824" height="471" alt="image" src="https://github.com/user-attachments/assets/9283cd30-e6e2-4667-b55d-0e748556ded9" />

🌱 **Cambia el background(220) para que dependa de la distancia entre las ventanas. Puedes calcular la magnitud del resultingVector usando let distancia = resultingVector.mag(); y luego usa map() para convertir esa distancia a un valor de gris o color. background(map(distancia, 0, 1000, 255, 0)); (ajusta el rango 0-1000 según sea necesario). Inventa otra modificación creativa.**
> La modificación creativa que hice fue agregarle un shake a la bolita para simular la tensión al alejarse y estirar la cuerda. Me quedó así :D
```program.js
function draw() {

    // MODIFICACIÓN DEL FONDO GRIS =================================

    //esto lo tuve que mover para arriba porque si no el fondo se dibujaba superpuesto al círculo
    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let vector1 = createVector(currentPageData.x, currentPageData.y);
    let resultingVector = createVector(vector2.x - vector1.x, vector2.y - vector1.y);
    let distance = resultingVector.mag();

    let gris = map(distance, 0, 1000, 255, 0);
    background(gris);

    // MODIFICACIÓN CREATIVA :D ====================================
    // mapear la intensidad para un shake
    shakeIntensity = map(distance, 0, 1500, 0, 12);
    
    // hacerlo random
    let shakeX = random(-shakeIntensity, shakeIntensity);
    let shakeY = random(-shakeIntensity, shakeIntensity);
    
    //==============================================================
    
    if (!isConnected) {
        showStatus('Conectando al servidor...', color(255, 165, 0));
        return;
    }
    
    if (!hasRemoteData) {
        showStatus('Esperando conexión de la otra ventana...', color(255, 165, 0));
        return;
    }
    
    if (!isFullySynced) {
        showStatus('Sincronizando datos...', color(255, 165, 0));
        return;
    }
    // Solo dibujar cuando esté completamente sincronizado
    checkWindowPosition();
    
    // dibujar círculo main de la ventanita con el shake!!!!!!!!!!!!!!!!!!!!
    drawCircle(point2[0] + shakeX, point2[1] + shakeY);
    
    stroke(50);
    strokeWeight(20);
    drawCircle(resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
    line(point2[0] + shakeX, point2[1] + shakeY, resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
}
```
___

### 📝 Apply :D

Esto lo sufrí demasiado, porque creo que me salí mucho de la zona de comfort. Mi idea era, basado en eso de mandar la posición y las dimensiones, hacer un jueguito donde tú movieras una pestaña al arrastrarla con el mouse, y la otra la persiguiera automáticamente. Cuando fui a buscar cómo hacerlo, google decía que podía usar MoveBy(dx,dy) o MoveTo(x,y). PERO PROBLEMA!!!!!!!!!!!!!!!!!!!!!!!!!  
Los navegadores BLOQUEAN que se pueda mover una pestaña. Tenía que sacarlas como un PopUp, y luego cambiar con html las dimesiones (para que salieran de una vez más chiquitas y se pudieran perseguir)  

index.html (lo tuve que agregar para abrir las otras pestañas como popup. Está en la carpeta de public).
```p.html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <title>Launcher :B</title>
  <style>
    button { 
      padding: 15px 30px; 
      font-size: 18px; 
      margin: 10px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Holi :P</h1>
  <button onclick="abrirVentanas()">Abrir Juego</button>
  <p>si no se abren las ventanas automáticamente, permite los popups plis</p>

  <script>
    let win1 = null;
    let win2 = null;

    function abrirVentanas() {
      win1 = window.open("/page1.html", "page1", "width=420,height=420,left=100,top=100");
      win2 = window.open("/page2.html", "page2", "width=420,height=420,left=650,top=100");
    }

  </script>
</body>
</html>
```
page1.html
```p.html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <title>Page 1</title>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
  <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>
  <style> body { margin:0; }</style>
</head>
<body>
<script defer src="page1.js"></script>
  <h3>AAAAAH ARRÁSTRAME PARA HUIR</h3>
  <p>DDDDDDDDDD:</p>
</body>
</html>
```
page1.js
```p.js
let currentPageData = {
  x: window.screenX,
  y: window.screenY,
  width: window.outerWidth,
  height: window.outerHeight
};

let previousPageData = {
  x: window.screenX,
  y: window.screenY,
  width: window.outerWidth,
  height: window.outerHeight
};

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point1 = [currentPageData.width / 2, currentPageData.height / 2];
let socket;
let isConnected = false;
let hasRemoteData = false;
let isFullySynced = false;

function setup() {
  createCanvas(windowWidth, windowHeight);
  frameRate(60);
  socket = io();

  socket.on('connect', () => {
    console.log('Connected with ID:', socket.id);
    isConnected = true;
    socket.emit('win1update', currentPageData, socket.id);

    setTimeout(() => {
      socket.emit('requestSync');
    }, 400);
  });

  socket.on('getdata', (response) => {
    if (response && response.data && isValidRemoteData(response.data)) {
      remotePageData = response.data;
      hasRemoteData = true;
      console.log('page1 recibió getdata:', remotePageData);
      socket.emit('confirmSync');
    }
  });

  socket.on('fullySynced', (synced) => {
    isFullySynced = synced;
    console.log('page1 fullySynced=', synced);
  });

  socket.on('peerDisconnected', () => {
    hasRemoteData = false;
    isFullySynced = false;
    console.log('page1: peerDisconnected');
  });

  socket.on('disconnect', () => {
    isConnected = false;
    hasRemoteData = false;
    isFullySynced = false;
    console.log('page1 disconnected from server');
  });

}

function isValidRemoteData(data) {
  return data &&
         typeof data.x === 'number' &&
         typeof data.y === 'number' &&
         typeof data.width === 'number' && data.width > 0 &&
         typeof data.height === 'number' && data.height > 0;
}

function checkWindowPosition() {
  currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.outerWidth,
    height: window.outerHeight
  };

  if (currentPageData.x !== previousPageData.x ||
      currentPageData.y !== previousPageData.y ||
      currentPageData.width !== previousPageData.width ||
      currentPageData.height !== previousPageData.height) {

    point1 = [currentPageData.width / 2, currentPageData.height / 2];
    socket.emit('win1update', currentPageData, socket.id);
    previousPageData = { ...currentPageData };
  }
}

function draw() {
  background(200, 230, 255);

  if (!isConnected) {
    showStatus('Conectando al servidor...', color(255, 165, 0));
    return;
  }

  if (!hasRemoteData) {
    showStatus('Esperando datos de la otra ventana...', color(255, 165, 0));
    return;
  }

  if (!isFullySynced) {
    showStatus('Sincronizando...', color(255, 165, 0));
    return;
  }

  //dibujar circulito inocente
  drawCircle(point1[0], point1[1]);
  checkWindowPosition();

  //dibujar circulito malvado
  let vector1 = createVector(currentPageData.x, currentPageData.y);
  let vector2 = createVector(remotePageData.x, remotePageData.y);
  let resultingVector = createVector(vector2.x - vector1.x, vector2.y - vector1.y);

  stroke(50);
  strokeWeight(10);
  drawCircle(resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
  line(point1[0], point1[1], resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
}

function showStatus(message, statusColor) {
  textSize(20);
  textAlign(CENTER, CENTER);
  noStroke();
  fill(0, 0, 0, 150);
  rectMode(CENTER);
  let textW = textWidth(message) + 30;
  let textH = 36;
  rect(width / 2, height / 6, textW, textH, 8);
  fill(statusColor);
  text(message, width / 2, height / 6);
}

function drawCircle(x, y) {
  fill(255, 50, 50);
  noStroke();
  ellipse(x, y, 120, 120);
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```

page2.html
```p.html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <title>Page 2</title>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
  <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>
  <style> body { margin:0; }</style>
</head>
<body>
  <script defer src="/page2.js"></script>
  <h3>CORRE QUE TE COMOOOO</h3>
  <p>>:DDDDDDDDDDDDDDD</p>
</body>
</html>
```
page2.js
```p.js
let currentPageData = {
  x: window.screenX,
  y: window.screenY,
  width: window.outerWidth,
  height: window.outerHeight
};

let previousPageData = { ...currentPageData };
let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point2 = [currentPageData.width / 2, currentPageData.height / 2];

let socket;
let isConnected = false;
let hasRemoteData = false;
let isFullySynced = false;

const maxStep = 30; // pixels por tick (aka velocidad de movimiento)
const moveInterval = 80; // ms entre movimiento

function setup() {
  createCanvas(windowWidth, windowHeight);
  frameRate(60);
  socket = io();

  socket.on('connect', () => {
    console.log('Connected with ID:', socket.id);
    isConnected = true;
    socket.emit('win2update', currentPageData, socket.id);

    setTimeout(() => {
      socket.emit('requestSync');
    }, 400);
  });

  socket.on('getdata', (response) => {
    if (response && response.data && isValidRemoteData(response.data)) {
      remotePageData = response.data;
      hasRemoteData = true;
      console.log('page2 recibió getdata:', remotePageData);
      socket.emit('confirmSync');
    }
  });

  socket.on('fullySynced', (synced) => {
    isFullySynced = synced;
    console.log('page2 fullySynced=', synced);
  });

  socket.on('peerDisconnected', () => {
    hasRemoteData = false;
    isFullySynced = false;
    console.log('page2: peerDisconnected');
  });

  socket.on('disconnect', () => {
    isConnected = false;
    hasRemoteData = false;
    isFullySynced = false;
    console.log('page2 disconnected from server');
  });
   
  // ============== MOVIMIENTO AAAAAAAAAAAAAAAAAAAAA=======================
  // si está sincronizado y hay datos, la ventanita se intenta mover
  setInterval(() => {
    if (!hasRemoteData || !isFullySynced) return;

    const targetX = remotePageData.x;
    const targetY = remotePageData.y;

    const curX = window.screenX;
    const curY = window.screenY;

    const dx = targetX - curX;
    const dy = targetY - curY;
    const dist = Math.hypot(dx, dy);

    if (dist < 40) {
      window.close();
      return;
    }

    const step = Math.min(maxStep, dist);
    const vx = (dx / dist) * step;
    const vy = (dy / dist) * step;
    const nextX = Math.round(curX + vx);
    const nextY = Math.round(curY + vy);

    window.moveTo(nextX, nextY);

  }, moveInterval);
}

function isValidRemoteData(data) {
  return data &&
         typeof data.x === 'number' &&
         typeof data.y === 'number' &&
         typeof data.width === 'number' && data.width > 0 &&
         typeof data.height === 'number' && data.height > 0;
}

function checkWindowPosition() {
  currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.outerWidth,
    height: window.outerHeight
  };

  if (currentPageData.x !== previousPageData.x ||
      currentPageData.y !== previousPageData.y ||
      currentPageData.width !== previousPageData.width ||
      currentPageData.height !== previousPageData.height) {

    point2 = [currentPageData.width / 2, currentPageData.height / 2];
    socket.emit('win2update', currentPageData, socket.id);
    previousPageData = { ...currentPageData };
  }
}

function draw() {
  background(255, 220, 220);

  if (!isConnected) {
    showStatus('Conectando al servidor...', color(255, 165, 0));
    return;
  }

  if (!hasRemoteData) {
    showStatus('Esperando datos de la otra ventana...', color(255, 165, 0));
    return;
  }

  if (!isFullySynced) {
    showStatus('Sincronizando...', color(255, 165, 0));
    return;
  }

  drawCircle(point2[0], point2[1]);
  checkWindowPosition();

  // posición aprox circulito inocente D:
  let vector2 = createVector(remotePageData.x, remotePageData.y);
  let vector1 = createVector(currentPageData.x, currentPageData.y);
  let resultingVector = createVector(vector2.x - vector1.x, vector2.y - vector1.y);

  stroke(50);
  strokeWeight(10);
  drawCircle(resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
  line(point2[0], point2[1], resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
}

function showStatus(message, statusColor) {
  textSize(20);
  textAlign(CENTER, CENTER);
  noStroke();
  fill(0, 0, 0, 150);
  rectMode(CENTER);
  let textW = textWidth(message) + 30;
  let textH = 36;
  rect(width / 2, height / 6, textW, textH, 8);
  fill(statusColor);
  text(message, width / 2, height / 6);
}

function drawCircle(x, y) {
  fill(180, 20, 20);
  noStroke();
  ellipse(x, y, 120, 120);
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```
server.js
```p.js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const path = require('path');

const app = express();
const server = http.createServer(app);
const io = socketIO(server);
const port = 3000;

let page1 = { x: 0, y: 0, width: 100, height: 100 };
let page2 = { x: 0, y: 0, width: 100, height: 100 };
let connectedClients = new Map();
let syncedClients = new Set();

app.use(express.static(path.join(__dirname, 'views')));

app.get('/', (req, res) => res.sendFile(path.join(__dirname, 'views', 'index.html')));
app.get('/page1.html', (req, res) => res.sendFile(path.join(__dirname, 'views', 'page1.html')));
app.get('/page2.html', (req, res) => res.sendFile(path.join(__dirname, 'views', 'page2.html')));
app.get('/page1.js', (req, res) => res.sendFile(path.join(__dirname, 'views', 'page1.js')));
app.get('/page2.js', (req, res) => res.sendFile(path.join(__dirname, 'views', 'page2.js')));

io.on('connection', (socket) => {
  console.log('A user connected - ID:', socket.id);
  connectedClients.set(socket.id, { page: null, synced: false });

  socket.on('disconnect', () => {
    console.log('User disconnected - ID:', socket.id);
    connectedClients.delete(socket.id);
    syncedClients.delete(socket.id);
    socket.broadcast.emit('peerDisconnected');
    checkAndNotifySyncStatus();
  });

  socket.on('win1update', (window1, sendid) => {
    if (isValidWindowData(window1)) {
      page1 = window1;
      connectedClients.set(socket.id, { page: 'page1', synced: false });
      socket.broadcast.emit('getdata', { data: page1, from: 'page1' });
      checkAndNotifySyncStatus();
    }
  });

  socket.on('win2update', (window2, sendid) => {
    if (isValidWindowData(window2)) {
      page2 = window2;
      connectedClients.set(socket.id, { page: 'page2', synced: false });
      socket.broadcast.emit('getdata', { data: page2, from: 'page2' });
      checkAndNotifySyncStatus();
    }
  });

  socket.on('requestSync', () => {
    const clientInfo = connectedClients.get(socket.id);
    if (clientInfo?.page === 'page1') {
      socket.emit('getdata', { data: page2, from: 'page2' });
    } else if (clientInfo?.page === 'page2') {
      socket.emit('getdata', { data: page1, from: 'page1' });
    }
  });

  socket.on('confirmSync', () => {
    syncedClients.add(socket.id);
    const clientInfo = connectedClients.get(socket.id);
    if (clientInfo) {
      connectedClients.set(socket.id, { ...clientInfo, synced: true });
    }
    checkAndNotifySyncStatus();
  });

  // ========= CUANDO SE CAPTURA LA VENTANITA DE LA BOLITA BUENA =====
  socket.on('captured', () => {
    console.log('Debug - Fin juego (captured)');
    io.emit('gameOver');
  });
  // ================================================================
});

function isValidWindowData(data) {
  return data &&
         typeof data.x === 'number' &&
         typeof data.y === 'number' &&
         typeof data.width === 'number' && data.width > 0 &&
         typeof data.height === 'number' && data.height > 0;
}

function checkAndNotifySyncStatus() {
  const page1Clients = Array.from(connectedClients.entries()).filter(([id, info]) => info.page === 'page1');
  const page2Clients = Array.from(connectedClients.entries()).filter(([id, info]) => info.page === 'page2');

  const bothPagesConnected = page1Clients.length > 0 && page2Clients.length > 0;
  const allClientsSynced = Array.from(connectedClients.keys()).every(id => syncedClients.has(id));
  const hasMinimumClients = connectedClients.size >= 2;

  console.log(`Debug - Connected clients: ${connectedClients.size}, Page1: ${page1Clients.length}, Page2: ${page2Clients.length}, Synced: ${syncedClients.size}`);

  if (bothPagesConnected && allClientsSynced && hasMinimumClients) {
    io.emit('fullySynced', true);
    console.log('All clients are fully synced');
  } else {
    io.emit('fullySynced', false);
    console.log(`Sync status: pages=${bothPagesConnected}, synced=${allClientsSynced}, clients=${connectedClients.size}`);
  }
}

server.listen(port, () => {
  console.log(`Juega en http://localhost:${port}`);
});
```



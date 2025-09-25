
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

> ___
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



# Evidencias de la unidad 7

### 📝 Actividad 01

🌱 **¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?**  
> `https://9rlf84l8-3000.use2.devtunnels.ms/`. Porque el localhost se refiere a un servidor en cada maquinita de pc. Si otro dispotivo quiere acceder a la máquina, toca usar una herramienta como esa de devtunnels para conectarlos. Si yo l mando el localhost, se abriría solamente localmente en el celular. Y lo de la ip funciona solamente si estás en el mismo wifi :(    

🌿 **Describe brevemente qué hace npm install y npm start.**  
> `npm install:` instala las dependencias del proyecto (librerías y cositas para que pueda correr)  
> `npm start:` inicia el servidor (lo pone a correr y funcionar)   

🌼 **¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?**
> En ambos me salió "new client connected" cuando se unieron, pero solamente cuando se unió el cel me empezó a llegar el mensaje de "received message" con las coordenadas del touch. No eran tampoco como en la actividad anterior que decía como un código para cada uno, solamente mencionaba en general que se conectó un client sin decir cuál es cuál.  

🌻 **Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?**
> Sii, funcionó!! y sí había como un segundo cada ciertos frames donde se buggeaba y saltaba de una posición a otra.

___
### 📝 Actividad 02

🌱 **Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?**  
> Es necesario porque crear una conexión pública puede ser súper inseguro y abrirte a un montón de ataques. Ofrece una manera de controlar esas conexiones a los ports para desarrollar cositas, probarlas y hostearlas. En este caso en específico, es más porque hace súper sencilla esa conexión entre dos dispositivos sin enredarse mucho con manejar ips y toda la vuelta, y no está sujeto a restricciones de red. La forma en la que funciona es que reenvía las conexiones a node, entonces hace como el papel de "mensajero" entre ambos dispositivos.   

🌿 **Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.**  
> Detecta cuando la persona está moviendo el input del touch. Como un movimiento puede ser de un solo pixel por que el dedo tiemble o la mano se recueste distinto, se agrega un threshold que permite ignorar cualquier señal con cambios irrelevantes. Así no se sobrecarga el tunel con señales, porque ya de por sí es suficiente trabajo mandar la info de un lado a otro.  

🌼 **Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?**  
> Me imagino que usar la IP es más rápido (porque está en la misma red), pero configurar cosas así usualmente tira problemas como con firewall y eso. Terrible para hostear servidores de minecraft. Y aparte, no muy seguro en absoluto. También, obviamente, la restricción de que deben estar con tu wifi. Con DevTunnels, se puede conectar desde cualquier lugar, pero en la documentación dice que hay límite de usuarios que pueden acceder al mismo tiempo. Además, los datos se demoran más en mandarse.  

🌻 **Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal).**  
<img width="319" height="414" alt="image" src="https://github.com/user-attachments/assets/015990bc-8c1d-49a0-ab51-5e9e2692ccd2" /> <img width="738" height="1600" alt="image" src="https://github.com/user-attachments/assets/d47dce78-b5ed-4c8c-a12c-951f103ac447" />  

___
### 📝 Actividad 03

🌱 **¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?**  
> `express.static(‘public’)` agarra automáticamente los archivos de la carpeta public en el proyecto para poder mostrarlas cuando alguien se conecta al server. En el de la unidad 6, tocaba definir manualmente la ruta de cada una de las vistas D:    

🌿 **Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?**  
> 1. En el sketch.js de mobile, touchMoved() detecta el movimiento y ejecuta socket.emit('message', touchData)  
> 2. El servidor recibe el mensaje con socket.on('message', (message) => etc) y manda el broadcast de message con el message.   
> 3. Cuando el sketch de mobile lo recibe, escribe en la consola los datos. Cuando el sketch de desktop lo recibe, si el mensaje es de tipo touch, mueve el circulito.  
> 4. Usa el broadcast emit porque es el único que deja mandarle el mensaje a todos los clientes MENOS al cel que lo envió. El io se lo mandaría a TODOS (incluyendo al cel), y el emit a solamente al cel...  

🌼 **Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?**  
> Los dos computadores sí, pero el cel no. Por lo que expliqué, de que el broadcast emit se lo manda a TODOS los clientes MENOS el que lo mandó :P  

🌻 **¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?**   
> Avisa cuándo se conectó un cliente, avisa la posición que está detectando para el touch, avisa si un cliente se desconectó. Todo eso me sirve para entender dónde está fallando el código, donde se de el caso.  
  
___
### 📝 Actividad 04
<img width="664" height="931" alt="image" src="https://github.com/user-attachments/assets/979e3615-2e27-46ee-8057-9e085a8a0b68" />    
  
___
 
## 📝 Apply




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
> 

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

🌱 **Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?**
> Al minimizar ambas ventanas, cambia la posición de los círculos y se extiende esa línea que une sus centros. 


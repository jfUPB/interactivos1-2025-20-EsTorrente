
# Evidencias de la unidad 5

## Set: ¿Qué aprenderás en esta unidad? 💡

🌱 **Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?**  
> El micro:bit está mandando una línea que contiene la secuencia de datos (valor en X del acelerómetro, valor en Y del acelerómetro, si A está presionado, si B está presionado) separados por una coma, finalizando con un `\n`, y usando la linea `uart.write`. El programa de p5.js recibe la línea entera, la corta en el `\n`, la separa por elementos usando la coma como separador, y revisa que la línea sea exactamente de 4 datos. Si no lo es, lanza un error. Si cumple con el requisito, entonces asigna cada dato a una variable en el programa y actualiza su valor cada frame.   
  
🌿 **¿Cómo es la estructura del protocolo ASCII usado?**  
> `nombre = "{},{},...\n".format(var1,var2...)`: misma cantidad de llaves que de datos a enviar, separados por una coma y finalizando con un cambio de línea.  
  
🌼 **Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.**  

```
    if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
      if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length == 4) {
          microBitX = int(values[0]) + windowWidth / 2;
          microBitY = int(values[1]) + windowHeight / 2;
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";
          updateButtonStates(microBitAState, microBitBState);
        } else {
          print("No se están recibiendo 4 datos del micro:bit");
        }
      }
    }
```
> 

🌻 **¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?**  
> La función updateButtonStates se llama cada frame con datos actualizados, y utiliza 4 variables: microBitAState, microBitBState, prevmicroBitAState y prevmicroBitBState. Al combinar estos, podemos identificar distintos eventos.  
> 1. `microBitAState solo` = se está presionando A.  
> 2. `microBitBState solo` = se está presionando B.  
> 3. `microBitAState && prevmicroBitAState === false` = se presionó A (no detecta que se quedó presionado, porque el botón debía estar suelto el frame anterior para correrse).  
> 4. `microBitBState && prevmicroBitBState === false` = se presionó B (no detecta que se quedó presionado, porque el botón debía estar suelto el frame anterior para correrse).  
> 5. `microBitBState === false && prevmicroBitBState` = se soltó B (detecta que fue presionada en el frame anterior y en el frame actual ya no lo está).  
> 6. `microBitAState === false && prevmicroBitAState` = se soltó A (detecta que fue presionada en el frame anterior y en el frame actual ya no lo está).  
> 7. `microBitAState && microBitBState` = ambas están presionadas.
> Al terminar de ejecutar los bloques de código que cumplan los checks, se actualiza cuál fue el estado de ambos botones en ese frame dentro de las variables de estado previo.  
  
🌱 **Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.**  
Nido con pollito (pollito agregado en post porque fue mucho ki para mí):    
<img width="852" height="750" alt="image" src="https://github.com/user-attachments/assets/43d1ad71-ec6a-44af-a9e9-a8f3031f1f74" />  
Tigre ensangrentado después de atacar violentamente a su víctima (ojos y orejas agregados en post):  
<img width="895" height="750" alt="image" src="https://github.com/user-attachments/assets/e554a4bf-6d16-477e-a129-d4ba84e57743" />  
___

## Seek: Investigación 🔎

### 📋 Actividad 02
🌱 **Abre la aplicación, configura el puerto, deja los valores por defecto y presiona Conectar. Selecciona el puerto del micro:bit (mbed Serial port) y presiona Conectar. Luego, en la sección de Recepción de Datos, en Mostrar datos como, selecciona Texto. Captura el resultado del experimento anterior. ¿Por qué se ve este resultado?**  
<img width="1004" height="255" alt="image" src="https://github.com/user-attachments/assets/36b83035-ebc2-4d94-840d-b951d706f155" />
> 

🌿 **Ahora cambia la opción de Mostrar datos como a Todo en Hex y vuelve a capturar el resultado. Captura el resultado del experimento anterior. Lo que ves ¿Cómo está relacionado con esta línea de código?**  
<img width="995" height="253" alt="image" src="https://github.com/user-attachments/assets/f5f38774-bc48-4755-b1b8-1cdfa735653f" />
> 

🌼 **¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?**  
>

🌻 **Captura el resultado del experimento. ¿Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato '>2h2B'? ¿Qué significa cada uno de los bytes que se envían?**  
<img width="989" height="448" alt="image" src="https://github.com/user-attachments/assets/5b957bd2-7382-4496-a4c3-574f20a222bb" />
> Se están enviando 2 bytes del xValue, 2 bytes del yValue, 1 byte de aState y 1 byte de bState. En total, cada vez que el micro:bit envía el dato, se están enviando 6 bytes. Como los bytes más grandes se envían primero, entonces aparecen al inicio los de 2.  
> - `2h`: 2 enteros cortos  
> - `2B`: 2 enteros sin signo  

🌱 **Recuerda de la unidad anterior que es posible enviar números positivos y negativos para los valores de xValue y yValue. ¿Cómo se verían esos números en el formato '>2h2B'?**  
>

🌿 **Captura el resultado del experimento. ¿Qué diferencias ves entre los datos en ASCII y en binario? ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII? ¿Qué ventajas y desventajas ves en usar un formato ASCII en lugar de binario?**  
<img width="960" height="297" alt="image" src="https://github.com/user-attachments/assets/58bb3b30-ee69-469d-b5d1-612f519e463a" />
> 

### 📋 Actividad 03

🌼 **Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.**  
> Creo que es porque este formato indica directamente en el código cuántos datos de cuántos bytes se van a enviar. En el anterior, necesitábamos definir manualmente un punto de corte. Aquí, se sabe directamente cuál será el largo del dato enviado.  

🌻 **Compara el código de la unidad anterior relacionado con la recepción de los datos seriales que ves ahora. ¿Qué cambios observas? ¿Qué ves en la consola? ¿Por qué crees que se produce este error?**  
<img width="939" height="301" alt="image" src="https://github.com/user-attachments/assets/79706bee-efb5-4944-a1d4-2b19900fef64" />
>

🌱 **Analiza el código, observa los cambios. Ejecuta y luego observa la consola. ¿Qué ves?**  
>

🌿 **¿Qué cambios tienen los programas y ¿Qué puedes observar en la consola del editor de p5.js?**  
<img width="959" height="402" alt="image" src="https://github.com/user-attachments/assets/e24c9ff0-0d24-42a2-a088-75003f891bb3" />
>







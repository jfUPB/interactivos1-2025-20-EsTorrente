
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

## Seek: Investigación 🔎




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
> El código está diciendo que si hay algún byte que se esté recibiendo, debe leer lo que esté en el port hasta encontrarse con un "\n". Cuando lo encuentra, separa el texto de data por la ubicación de las comas. Revisa si la cantidad de segmentos en la que se dividió es igual a 4, y si lo es, significa que se envió correctamente todo lo que definimos. De ahí, simplemente está diciendo que la primera sección en la que lo partió le corresponde a microBitX, la segunda a microBitY (a estas les agrega las dimensiones de la pantalla / 2 para que puedan interpretarse como coordenadas estables), la tercera sección le corresponde al estaod del botón A, y el último al estado del botón B. (PARÉNTESIS: las variables de los botones se inicializan en false. Cuando las estamos seteando en esta parte del código, el `values[2].toLowerCase() === "true"` lo que hace es decir: lo que me enviaste es igual a "true"? si sí, entoncefs microBit_State = verdadero... y si no, microBit_State = false). Le manda esos datos al método de updateButtonStates y listo. Finalmente, si no pasó el check de que el length sean 4 datos, entonces tira un mensaje que nos indica que algo está mal.  

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
> No estoy muy segura de por qué no lo puede mostrar como texto D:  
> En mi cabecita igual los números del HEX... siguen siendo números??? pero asumo entonces que debe ser más como el unicode, donde no serían el número como tal sino una versión codificada de una serie de caracteres... y por eso no lo puede leer.  
 
🌿 **Ahora cambia la opción de Mostrar datos como a Todo en Hex y vuelve a capturar el resultado. Captura el resultado del experimento anterior. Lo que ves ¿Cómo está relacionado con esta línea de código?**  
<img width="995" height="253" alt="image" src="https://github.com/user-attachments/assets/f5f38774-bc48-4755-b1b8-1cdfa735653f" />  
> No entiendo mucho lo que estoy viendo, dónde empieza y dónde termina el dato que se envía cada frame... pero lo que sí entiendo es que los caracteres junticos que observo son cada uno un byte.  

🌼 **¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?**  
> Creo que la mayor diferencia es que el binario parece mucho más eficaz a la hora de mandar los datos, porque ocupa menos espacio y se envía más rápido. Cada dato se manda ya en “su forma más cruda”, sin necesidad de convertirlo a caracteres de texto.  
> La parte negativa es que yo no puedo leer nada de lo que dice a simple vista D:  
> Además, hay que ser súper cuidadoso a la hora de definir el formato, porque si me equivoco en cuántos bytes corresponde a cada dato, los números se empiezan a leer mal. En ASCII, en cambio, basta con separar por comas y ya sé dónde empieza y dónde termina cada valor.  

🌻 **Captura el resultado del experimento. ¿Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato '>2h2B'? ¿Qué significa cada uno de los bytes que se envían?**  
<img width="989" height="448" alt="image" src="https://github.com/user-attachments/assets/5b957bd2-7382-4496-a4c3-574f20a222bb" />  
> Se están enviando 2 bytes del xValue, 2 bytes del yValue, 1 byte del aState y 1 byte del bState. En total, cada vez que el micro:bit envía el dato, son 6 bytes. Como en el formato se usa el símbolo >, eso significa que los bytes “más grandes” (el byte alto de los enteros) se mandan primero.  
> - `2h`: son dos enteros cortos con signo (cada uno ocupa 2 bytes). Ahí van el xValue y el yValue.  
> - `2B`: son dos enteros sin signo de 1 byte cada uno. Ahí van los estados de los botones A y B, representados con 0 o 1 (creo, porque así es el true/false).  
> `PD: Creo que la trampita que habías mencionado es que le agregaste el check del gesto shake. Al principio sí me comí la trampa y no entendía por qué no llegaba ningún dato, pero no fue sino detenerme un segundo a mirar bien el código para notarlo.`  

🌱 **Recuerda de la unidad anterior que es posible enviar números positivos y negativos para los valores de xValue y yValue. ¿Cómo se verían esos números en el formato '>2h2B'?**  
> No estoy 100% segura de todos los detalles, pero sí sé que como esos valores pueden ser negativos, entonces se guardan usando el formato de 2 bytes con signo (int16). Tuve que buscar el dato porque no sabía... y dice que en hexadecimal, los negativos se representan con algo que se llama complemento a dos, y por eso es que a veces aparecen un montón de F al inicio de los bytes cuando el número es negativo. Por ejemplo, un -1 no se guarda como 0x-1, sino como 0xFF 0xFF. En cambio, si el número es positivo, los bytes se ven sin esas F de relleno.  

🌿 **Captura el resultado del experimento. ¿Qué diferencias ves entre los datos en ASCII y en binario? ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII? ¿Qué ventajas y desventajas ves en usar un formato ASCII en lugar de binario?**  
<img width="960" height="297" alt="image" src="https://github.com/user-attachments/assets/58bb3b30-ee69-469d-b5d1-612f519e463a" />  
> En binario, cuando los miro en la cosita web en formato HEX, se ven separados por espacios... y en ASCII los valores aparecen separados por comas y con números normales que yo puedo leer. Aunque ahí en esa versión combinada donde lo puse, se separan con brackets por algún motivo? y el \n se ve como [0a], además de que aparece al inicio y al fin del dato con ASCII. La ventaja del ASCII es que es súper fácil de leer e interpretar a simple vista. El problema es que ocupa mucho más espacio porque cada número se convierte en texto, y además el computador tiene que convertirlos otra vez a números para poder usarlos. El binario, en cambio, ocupa mucho menos espacio y llega más directo al computador, porque no le toca hacer tanta conversión. Pero es mucho más difícil de interpretar para mí.

### 📋 Actividad 03

🌼 **Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.**  
> Creo que es porque en el formato binario ya se indica directamente en el código cuántos datos y de cuántos bytes se van a enviar. Entonces el receptor sabe exactamente dónde cortar. En cambio, en ASCII cada número puede tener distinta cantidad de dígitos, así que tocaba poner separadores como la coma y el salto de línea para que el programa supiera dónde terminaba un número y dónde empezaba el siguiente.  

🌻 **Compara el código de la unidad anterior relacionado con la recepción de los datos seriales que ves ahora. ¿Qué cambios observas? ¿Qué ves en la consola? ¿Por qué crees que se produce este error?**  
<img width="939" height="301" alt="image" src="https://github.com/user-attachments/assets/79706bee-efb5-4944-a1d4-2b19900fef64" />  
> 1. Ya no se usa la línea de `readUntil` ni el `\n` porque sabemos directamente que se van a mandar 6 bytes fijos.
> 2. En vez de checkear si hay más de 0 datos, checkea que hayan 6 o más. 
> 3. Utiliza `getInt16(0)` para agarrar el primer dato, `getInt16(2)` para el segundo (porque el primero ocupaba el byte 0 y el byte 1), `getUint8(4)` para el tercero (porque los uints no tienen signo, siempre se toman positivos), y `getUint8(5)` para el último porque el anterior se componía de un solo byte.  
> 4. Ya no se están seteando los estados de los botones con `=== "true"` sino con `=== 1`  
> 5. No estoy del todo segura de cómo funciona el DataView, pero estoy viendo que es necesario para interpretar los datos. Eso no era necesario con ASCII. Me imagino que es como un cast?  
  
> El error que mencionas creo que pasa porque los 6 bytes no siempre llegan justos, sino que se mezclan con otros bytes del siguiente paquete. Entonces el programa los corta mal, junta pedacitos de mensajes distintos, y termina interpretando números que no corresponden a lo que realmente enviamos.  

🌱 **Analiza el código, observa los cambios. Ejecuta y luego observa la consola. ¿Qué ves? ¿Qué cambios tienen los programas y ¿Qué puedes observar en la consola del editor de p5.js?**   
<img width="959" height="402" alt="image" src="https://github.com/user-attachments/assets/e24c9ff0-0d24-42a2-a088-75003f891bb3" />  
> Ahora sí funciona :D  
> Los datos se cortan de manera correcta, no hay bytes sueltos ni números que nada qué ver. Todo llega bien alineado. Igual siento que el procedimiento se volvió muchísimo más largo y complejo que con ASCII. Con ASCII bastaba con un split(",") y listo, y acá hay que estar pendiente de los bytes, los offsets y el DataView. Quizás es porque no estoy familiarizada con muchas de las líneas de código que se usaron, pero por ahora siento que el ASCII es más amigable aunque el binario sea más rápido y eficiente.  

___

### ⭐ MI INVESTIGACIÓN Y PREGUNTAS ⭐
| PREGUNTA | RESPUESTA GOOGLEADA | MI INTERPRETACIÓN |
|----------|---------------------|-------------------|
| Por qué los valores del HEX no son realmente números? por qué la página que usé para mirar los datos enviados no los interpreta como texto? qué son entonces realmente? | Lo que se envía por serial son bytes crudos (un byte = 8 bits = un valor entre 0 y 255). Esos bytes no tienen “tipo de dato”: pueden representar un número, una letra, un color, o lo que tú quieras, según cómo el receptor los interprete. El valor de cada byte en base 16 (hexadecimal) es una forma práctica de ver los bytes en bruto. No son números ni texto por sí mismos, son datos binarios. El “texto ASCII” es solo un caso especial donde a cada número (ej: 65) se le asigna un carácter (ej: 'A'). | No son texto, es la forma súper primitiva de los datos. Como no lo estoy poniendo en el código que lo interpreta con su contexto, la página simplemente me permite visualizar lo que se está enviando directamente. Como el HEX no tiene asignado esos caracteres especiales como el ASCII, entonces la opción de texto no tenía qué mostrarme realmente. |
| Por qué se utiliza 0xAA como el inicio del paquete? y por qué un checksum para el final? | 0xAA (10101010 en binario) se usa porque es un valor muy fácil de reconocer y poco probable que aparezca al azar en medio de los datos. Eso lo convierte en un buen “byte de sincronización”. El checksum al final sirve para verificar que el paquete llegó completo y sin errores de transmisión. Si un byte se pierde o cambia en el camino, el checksum no coincide y el paquete se descarta. | Se usa específicamente 0xAA porque no es para nada común que un programa lo tire por naturaleza. El checksum me deja ver que la suma de los datos al enviarse sea igual al recibirse, y así sé que todo se procesó correctamente. |
| Realmente es más eficaz usar binario para enviar los datos si luego hay que hacer el triple de código en la parte de p5.js para asegurarse de que corte bien los datos, cuando en ASCII era un check simple para el \n? | Binario tiene la ventaja de que los datos ocupan mucho menos (6 bytes vs ~12–15 bytes en ASCII). Esto es importante si envías muchos datos o la velocidad de transmisión es baja. Su desventaja es que necesitas más código para sincronizar y validar. ASCII es fácil de leer e interpretar, basta con buscar un \n como delimitador. Sin embargo, ocupa más espacio y requiere convertir los números a texto (y luego de texto a número). En proyectos simples (como con micro:bit), ASCII es suficiente. Pero en sistemas industriales, juegos en red, sensores de alta frecuencia… binario es más eficiente y rápido aunque requiera más trabajo del programador. | Básicamente, sufro yo programando algo más largo para que el programa corra mejor. Es más eficaz para el usuario y la máquina, pero mas doloroso para mí D: |
| Qué es el serialBuffer? qué hace serialBuffer.concat(newData)? | serialBuffer es un arreglo (array) que guarda temporalmente los bytes recibidos. Como los datos no siempre llegan de a 8 bytes justos, se van guardando en este buffer hasta que haya suficiente para formar un paquete completo. `serialBuffer.concat(newData)` junta el array anterior con los nuevos bytes recibidos (newData). | el serial buffer va recogiendo temporalmente los datos nuevos que llegan hasta que alcanza los 8 que le pedí, y ahí ya lo manda como un paquete completo. |
| cuál es la diferencia de slice y splice en serialBuffer.slice(0, 8) y serialBuffer.splice(0, 8)? | `slice(inicio, fin)` → copia una parte del array sin modificar el original. `splice(inicio, cantidad)` → corta y elimina esa parte del array, modificando el original. | El slice corta el array y los pega en packet, los datos todos siguen en ese mismo array original. El splice corta el original otra vez y directamente los elimina cuando termina. |
| qué es el DataView? por qué se usa para extraer los datos en view.getInt16(0)? | DataView es una clase de JavaScript que permite leer y escribir datos binarios dentro de un ArrayBuffer. Es necesario porque los bytes que llegan son “planos”, se desea interpretarlos como enteros de 16 bits o enteros de 8 bits. | coge los numeritos separados de los bytes y los convierte a los números que les corresponden. |

Literalmente después de responder todas estas preguntas y seguir leyendo las actividades, me di cuenta de que la mayoría de cosas que investigué eran preguntas que tú nos planteaste también en el reflect. Flop. Pero supongo que eso significa que mi proceso de pensamiento e investigación es adecuado, y es muestra de que las preguntas que planteé sí ayudan a mi aprendizaje. 









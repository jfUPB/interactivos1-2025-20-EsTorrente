
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
<a name="02"></a>
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
<a name="03"></a>
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
<a name="tabla"></a>
| PREGUNTA | RESPUESTA GOOGLEADA | MI INTERPRETACIÓN |
|----------|---------------------|-------------------|
| Por qué los valores del HEX no son realmente números? por qué la página que usé para mirar los datos enviados no los interpreta como texto? qué son entonces realmente? | Lo que se envía por serial son bytes crudos (un byte = 8 bits = un valor entre 0 y 255). Esos bytes no tienen “tipo de dato”: pueden representar un número, una letra, un color, o lo que tú quieras, según cómo el receptor los interprete. El valor de cada byte en base 16 (hexadecimal) es una forma práctica de ver los bytes en bruto. No son números ni texto por sí mismos, son datos binarios. El “texto ASCII” es solo un caso especial donde a cada número (ej: 65) se le asigna un carácter (ej: 'A'). | No son texto, es la forma súper primitiva de los datos. Como no lo estoy poniendo en el código que lo interpreta con su contexto, la página simplemente me permite visualizar lo que se está enviando directamente. Como el HEX no tiene asignado esos caracteres especiales como el ASCII, entonces la opción de texto no tenía qué mostrarme realmente. |
| <a name="EleccionHeader"></a> Por qué se utiliza 0xAA como el inicio del paquete? y por qué un checksum para el final? | 0xAA (10101010 en binario) se usa porque es un valor muy fácil de reconocer y poco probable que aparezca al azar en medio de los datos. Eso lo convierte en un buen “byte de sincronización”. El checksum al final sirve para verificar que el paquete llegó completo y sin errores de transmisión. Si un byte se pierde o cambia en el camino, el checksum no coincide y el paquete se descarta. | Se usa específicamente 0xAA porque no es para nada común que un programa lo tire por naturaleza. El checksum me deja ver que la suma de los datos al enviarse sea igual al recibirse, y así sé que todo se procesó correctamente. |
| <a name="HeaderLargo"></a> Sobre ese header, por qué se usa un dato de un solo byte? hay algunos casos donde el header sea más largo? | no la googleé, voy a asumir | mi guess es que en nuestro caso no es un header más largo porque, en el caso de que se dé casualmente el envío de forma natural de 0xAA, la lectura errónea no sería catastrófica porque igual tenemos un checksum... e incluso si logra pasar ese checksum, simplemente se dan parámetros incorrectos por un frame y luego continúa funcionando con normalidad. Según vi, al probabilidad de que salga ese header de por sí es muy bajita... pero me imagino que en un programa súper serio e importante, no se pueden dar el lujo de admitir error ni por un solo frame. Creo que hacer el header más largo reduce incluso más la probabilidad de que la combinación de bits se dé de forma natural, y por ende, lo vuelve más seguro. |
| <a name="ProblemaChecksum"></a> Qué pasa si en el checksum, por pura casualidad, dos de los datos se corrompen de manera que la suma igual da lo mismo que pedimos? | (mi guess antes de buscarlo es que, en nuestro caso, tampoco importa mucho.. se lee el dato incorrecto por un frame y ya sigue fallando el checksum. La probabilidad de que pase 2 veces CREO que es súper baja. Ahora sí, la respuesta buscada:) Este fenómeno se llama un error de compensación y es la gran debilidad de los checksums basados en sumas. Para detectar estos errores, se usan algoritmos más complejos como CRC (Cyclic Redundancy Check). Un CRC es mucho mejor detectando errores burst (ráfagas de errores consecutivos) y errores de compensación. La elección de nuevo es un trade-off: un CRC es más robusto pero requiere más poder de cálculo tanto en el transmisor como en el receptor. La comprobación de redundancia cíclica o CRC es un método para detectar cambios o errores accidentales en el canal de comunicación. La CRC utiliza un polinomio generador que está disponible tanto en el lado del emisor como en el del receptor. Un ejemplo de polinomio generador es del tipo x3 + x + 1. Este polinomio generador representa la clave 1011. Otro ejemplo es x2 + 1, que representa la clave 101. | Básicamente, al parecer ese error es lo suficientemente importante como para tener un nombre propio y una solución alternativa. Según entendí, en lugar de simplemente realizar una suma y una división como check, se utiliza más bien un polinomio. Ese polinomio genera un key, y si al recibirlo y decodificarlo el dato contiene un 1, es porque hubo un error. |
| <a name="Sleep"></a> Tú habías dicho que el sleep no es muy recomendable... hay alguna alternativa en este caso para controlar el flujo de datos? | Algunas soluciones son: Control de Flujo por Hardware (RTS/CTS): Los puertos seriales tienen pines dedicados (RTS - Request to Send y CTS - Clear to Send) para este propósito. Control de Flujo por Software (Protocolo XON/XOFF): Similar al anterior, pero usando dos caracteres de control especiales enviados por el propio canal de datos. Confirmación de Recepción (Acknowledgment - ACK): Esta es la solución más robusta y la que usan protocolos como TCP. El protocolo se vuelve bidireccional. | la primera solución es que el programa de p5.js baje un pin para decirle al micro:bit que tiene un buffer lleno, y luego lo vuelva a subir para continuar (necesita hardware). La segunda funciona como el header, enviando un bit para indicar que pare y otro para continuar. La tercera es que el micro:bit envía un paquete, el programa de p5.js lo recibe y devuelve un mensaje, y el micro:bit no vuelve a enviar nada hasta recibirlo. Se demora más que el sleep en procesar. |
| <a name="String"></a> Qué pasa si quiero enviar un string desde el micro:bit que no siempre sea del mismo largo? cómo se tendría que adaptar el envío de manera binaria y el check en el programa de p5.js? | /// | Se empaquetan los datos fijos primero usando la misma estructura que ya vimos. Luego convertimos el string a bytes y obtenemos su longitud. Empaquetamos la longitud como 1 byte (asumiendo que el string será menor a 255 caracteres). Construimos el paquete completo, hacemos el checksum y lo escribimos. En la parte de p5.js, leemos el byte que indica la longitud del string y luego tocaría calcular el lenght total del paquete como `1 (header) + 6 (datos fijos) + 1 (longitud string) + stringLength (string) + 1 (checksum)`. El check se hace con `serialBuffer.length >= totalPacketLength`. Por último, se hace un splice desde la posición donde empiezan los datos del string (9 en este caso) hasta ese punto + stringLenght, y se convierte a a texto con javascript. |
| <a name="Eficaz"></a> Realmente es más eficaz usar binario para enviar los datos si luego hay que hacer el triple de código en la parte de p5.js para asegurarse de que corte bien los datos, cuando en ASCII era un check simple para el \n? | Binario tiene la ventaja de que los datos ocupan mucho menos (6 bytes vs ~12–15 bytes en ASCII). Esto es importante si envías muchos datos o la velocidad de transmisión es baja. Su desventaja es que necesitas más código para sincronizar y validar. ASCII es fácil de leer e interpretar, basta con buscar un \n como delimitador. Sin embargo, ocupa más espacio y requiere convertir los números a texto (y luego de texto a número). En proyectos simples (como con micro:bit), ASCII es suficiente. Pero en sistemas industriales, juegos en red, sensores de alta frecuencia… binario es más eficiente y rápido aunque requiera más trabajo del programador. | Básicamente, sufro yo programando algo más largo para que el programa corra mejor. Es más eficaz para el usuario y la máquina, pero mas doloroso para mí D: |
| Qué es el serialBuffer? qué hace serialBuffer.concat(newData)? | serialBuffer es un arreglo (array) que guarda temporalmente los bytes recibidos. Como los datos no siempre llegan de a 8 bytes justos, se van guardando en este buffer hasta que haya suficiente para formar un paquete completo. `serialBuffer.concat(newData)` junta el array anterior con los nuevos bytes recibidos (newData). | el serial buffer va recogiendo temporalmente los datos nuevos que llegan hasta que alcanza los 8 que le pedí, y ahí ya lo manda como un paquete completo. |
| cuál es la diferencia de slice y splice en serialBuffer.slice(0, 8) y serialBuffer.splice(0, 8)? | `slice(inicio, fin)` → copia una parte del array sin modificar el original. `splice(inicio, cantidad)` → corta y elimina esa parte del array, modificando el original. | El slice corta el array y los pega en packet, los datos todos siguen en ese mismo array original. El splice corta el original otra vez y directamente los elimina cuando termina. |
| qué es el DataView? por qué se usa para extraer los datos en view.getInt16(0)? | DataView es una clase de JavaScript que permite leer y escribir datos binarios dentro de un ArrayBuffer. Es necesario porque los bytes que llegan son “planos”, se desea interpretarlos como enteros de 16 bits o enteros de 8 bits. | coge los numeritos separados de los bytes y los convierte a los números que les corresponden. |

Literalmente después de responder todas estas preguntas y seguir leyendo las actividades, me di cuenta de que la mayoría de cosas que investigué eran preguntas que tú nos planteaste también en el reflect. Flop. Pero supongo que eso significa que mi proceso de pensamiento e investigación es adecuado, y es muestra de que las preguntas que planteé sí ayudan a mi aprendizaje. 

___

### 📋 Actividad 04

🌱 **Código modificado para recibir datos de nueva forma:**

```program.py
// M_1_4_01
//
// Generative Gestaltung – Creative Coding im Web
// ISBN: 978-3-87439-902-9, First Edition, Hermann Schmidt, Mainz, 2018
// Benedikt Groß, Hartmut Bohnacker, Julia Laub, Claudius Lazzeroni
// with contributions by Joey Lee and Niels Poldervaart
// Copyright 2018
//
// http://www.generative-gestaltung.de
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

/**
 * creates a terrain like mesh based on noise values.
 *
 * MOUSE
 * position x/y + left drag   : specify noise input range
 * position x/y + right drag  : camera controls
 *
 * KEYS
 * arrow up                   : noise falloff +
 * arrow down                 : noise falloff -
 * arrow left                 : noise octaves -
 * arrow right                : noise octaves +
 * space                      : new noise seed
 * +                          : zoom in
 * -                          : zoom out
 * s                          : save png
 */

//MICRO:BIT
let port;
let connectBtn;
let connectionInitialized = false;
let microBitConnected = false;
let serialBuffer = [];

// ------ mesh ------
var tileCount;
var zScale;

// ------ noise ------
var noiseXRange;
var noiseYRange;
var octaves;
var falloff;

// ------ mesh coloring ------
var midColor;
var topColor;
var bottomColor;
var strokeColor;
var threshold;

// ------ mouse interaction ------
var offsetX;
var offsetY;
var clickX;
var clickY;
var zoom;
var rotationX;
var rotationZ;
var targetRotationX;
var targetRotationZ;
var clickRotationX;
var clickRotationZ;

const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAITMICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};
let appState = STATES.WAIT_MICROBIT_CONNECTION;
let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;

function setup() {
  createCanvas(600, 600, WEBGL);
  colorMode(HSB, 360, 100, 100);
  cursor(CROSS);
  
  // MICRO BIT ===========================================
  port = createSerial();
  connectBtn = createButton('Conectar al micro:bit');
  connectBtn.position(20, 20);
  connectBtn.mousePressed(connectBtnClick);

  // ------ mesh ------
  tileCount = 50;
  zScale = 150;

  // ------ noise ------
  noiseXRange = 10;
  noiseYRange = 10;
  octaves = 4;
  falloff = 0.5;

  // ------ mesh coloring ------
  topColor = color(0, 0, 100);
  midColor = color(30, 99, 63);
  bottomColor = color(0, 0, 0);
  strokeColor = color(60, 100, 100);
  threshold = 0.30;

  // ------ mouse interaction ------
  offsetX = 0;
  offsetY = 0;
  clickX = 0;
  clickY = 0;
  zoom = -300;
  rotationX = 0;
  rotationZ = 0;
  targetRotationX = PI / 3;
  targetRotationZ = 0;
}

function updateButtonStates(newAState, newBState) {
  
  if (newAState) {
    targetRotationX += 0.4;
    falloff -= 0.5;
      print("A pressed");
  }
  if (newBState) {
    targetRotationZ += 0.4;
    octaves++;
      print("B pressed");
  }
  
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}

function readSerialData() {

  let available = port.availableBytes();
  if (available > 0) {
    let newData = port.readBytes(available);
    serialBuffer = serialBuffer.concat(newData);
  }


  while (serialBuffer.length >= 8) {
    if (serialBuffer[0] !== 0xaa) {
      serialBuffer.shift(); 
      continue;
    }

    if (serialBuffer.length < 8) break;


    let packet = serialBuffer.slice(0, 8);
    serialBuffer.splice(0, 8); 


    let dataBytes = packet.slice(1, 7);
    let receivedChecksum = packet[7];

    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;

    if (computedChecksum !== receivedChecksum) {
      console.log("Checksum error in packet");
      continue; 
    }
    
    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0);
    microBitY = view.getInt16(2);
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
    updateButtonStates(microBitAState, microBitBState);

    console.log(
      `microBitX: ${microBitX} microBitY: ${microBitY} microBitAState: ${microBitAState} microBitBState: ${microBitBState}`
    );
  }
}

function draw() {
  background(0, 0, 100);
  ambientLight(150);
  
  //******************************************
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");

  readSerialData();

  // ------ set view ------
  push();
  translate(width * 0.05, height * 0.05, zoom);

  if (mouseIsPressed && mouseButton == RIGHT) {
    offsetX = mouseX - clickX;
    offsetY = mouseY - clickY;
    targetRotationX = min(max(clickRotationX + offsetY / float(width) * TWO_PI, -HALF_PI), HALF_PI);
    targetRotationZ = clickRotationZ + offsetX / float(height) * TWO_PI;
  }
  rotationX += (targetRotationX - rotationX) * 0.25;
  rotationZ += (targetRotationZ - rotationZ) * 0.25;
  rotateX(-rotationX);
  rotateZ(-rotationZ);

  // ------ mesh noise ------
    noiseXRange = microBitX / 220; // MODIFICADO CON MICROBIT
    noiseYRange = microBitY / 220; // MODIFICADO CON MICROBIT

  noiseDetail(octaves, falloff);
  var noiseYMax = 0;

  var tileSizeY = height / tileCount;
  var noiseStepY = noiseYRange / tileCount;

  for (var meshY = 0; meshY <= tileCount; meshY++) {
    beginShape(TRIANGLE_STRIP);
    for (var meshX = 0; meshX <= tileCount; meshX++) {

      var x = map(meshX, 0, tileCount, -width / 2, width / 2);
      var y = map(meshY, 0, tileCount, -height / 2, height / 2);

      var noiseX = map(meshX, 0, tileCount, 0, noiseXRange);
      var noiseY = map(meshY, 0, tileCount, 0, noiseYRange);
      var z1 = noise(noiseX, noiseY);
      var z2 = noise(noiseX, noiseY + noiseStepY);

      noiseYMax = max(noiseYMax, z1);
      var interColor;
      colorMode(RGB);
      var amount;
      if (z1 <= threshold) {
        amount = map(z1, 0, threshold, 0.15, 1);
        interColor = lerpColor(bottomColor, midColor, amount);
      } else {
        amount = map(z1, threshold, noiseYMax, 0, 1);
        interColor = lerpColor(midColor, topColor, amount);
      }
      fill(interColor);
      stroke(strokeColor);
      strokeWeight(1);
      vertex(x, y, z1 * zScale);
      vertex(x, y + tileSizeY, z2 * zScale);
    }
    endShape();
  }
  pop();

}
}

function mousePressed() {
  clickX = mouseX;
  clickY = mouseY;
  clickRotationX = rotationX;
  clickRotationZ = rotationZ;
}

function keyReleased() {
  if (keyCode == UP_ARROW) falloff += 0.05;
  if (keyCode == DOWN_ARROW) falloff -= 0.05;
  if (falloff > 1.0) falloff = 1.0;
  if (falloff < 0.0) falloff = 0.0;

  if (keyCode == LEFT_ARROW) octaves--;
  if (keyCode == RIGHT_ARROW) octaves++;
  if (octaves < 0) octaves = 0;

  if (keyCode == 187) zoom += 20; // '+'
  if (keyCode == 189) zoom -= 20; // '-'

  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
  if (key == ' ') noiseSeed(floor(random(100000)));
}
```
  
🌿 **Vas a documentar en tu bitácora todo el proceso de construcción de la aplicación, mostrando las pruebas intermedias que hiciste, los errores que encontraste y cómo los solucionaste.**
> El proceso de construcción fue muy sencillo. Realmente había manejado bien la parte de la modificación del programa en la versión anterior, por lo que no tuve que realizar correciones al código base. Simplemente comparé el código del ejemplo del ejercicio #3 y fuí analizando los cambios entre ese y mi plantilla. Empecé por borrar lo que ya no necesitaba, que era la manera vieja de procesar los datos. Luego, creé la función que manejaba ese proceso de la nueva forma. Una vez montada la función, la llamé en el draw()... y finalmente, caí en cuenta de que había una variable extra que debía agregar al inicio.
<a name="errores"></a>
> Cuando estaba contruyendo el proyecto, estaba DEMASIADO dormida. Cometí dos errores MUY bobos y MUY simples de solucionar. Uno de ellos, por ejemplo, fue haber agregado correctamente la función de leer datos, pero olvidarme de llamar `readSerialData()` en el draw (me quedé como 5 minutos procesando por qué no llegaban los datos). Otro error fue que, en medio de mi cansancio, se me olvidó declarar `let serialBuffer = [];`. Cuando fui a correr el programa, obviamente me lanzó error porque estaba intentando asignar un dato a una variable que no creé correctamente. Todo se arregló fácilmente con solo sentarme, leer detenidamente el código en lugar de copiar/pegar de manera confiada, y teniendo la ventaja de que comprendo realmente lo que estoy haciendo.  

Muestra de cómo se veía sin el `readSerialData()`. No sale ningún error... pero yo sabía que en el código, en caso de correr correctamente, me debería estar tirando un mensaje en el log que me dijera que había un error en el checksum si había un problema, o me hiciera print de los valores que estaba recibiendo. Como simplemente no había nada en consola, fue fácil darme cuenta de que ni siquiera estaba llamando el método y arreglarlo.  
<img width="1912" height="820" alt="image" src="https://github.com/user-attachments/assets/5ad43d9b-e4e9-4c43-aaa6-25f55f081118" />  
  
🌼 **Vas a realizar múltiples experimentos analizando el comportamiento de la aplicación que construiste. Reporta el proceso de experimentación en la bitácora. Con estas evidencias debes demostrar que has comprendido los conceptos y técnicas vistas en esta unidad.**  
  
**⭐ EXPERIMENTO 1 ⭐: modificar el código para quitar el checksum y ver cómo se daña la recepción de datos en mi programa.**
<a name="ex1"></a>  
> **Mi predicción:** los valores de X y Y que controlan los parámetros del ruido en el dibujo van a ser súper erráticos, porque los números no van a estar bien construidos y se van a convertir en valores arbitrarios. Además, los inputs van a mezclarse entre sí. Siento que la parte de la inclinación va a afectar el estado de los botones.

> **Lo que pasó:** Efectivame, todo sucedió tal cuál. El dibujo se dibujó con un ruido súper caótico, inclinar el micro:bit a la izquierda lo detectaba como presionar el botón B, y presionar el botón B se detectaba como presionar A. Esto es porque, sin el uso del checksum (y el buffer que usa), el programa solamente agarra los datos que le llegan y forma grupitos de datos sin reglas.   
  
<img width="1742" height="859" alt="image" src="https://github.com/user-attachments/assets/a5429799-b8a5-4e17-8faa-51b2566623da" />  
   
**⭐ EXPERIMENTO 2 ⭐: qué pasa si disminuyo y aumento el sleep() en el programa del micro:bit?**  
<a name="ex2"></a>  
> **Mi predicción:** si aumento el sleep, va a pasar un rato en el que no está detectando ningún input. Eso afecta, por ejemplo, la funcionalidad de dejar presionado el botón B para rotar la figura. Si lo disminuyo, no sé si el PC soporte la velocidad de envío... en el PC de la sala de los viernes, se me crasheó Google cuando lo intenté D:  
     
> **Lo que pasó:** al quitar el sleep por completo, es como si el programa estuviera x2. Presionar B una sola vez hace que el dibujito gire UN MONTÓN, y cada mínima inclinación del micro:bit provocaba como un "jittering" en el ruido. Siento que es porque la misma línea de datos se logra mandar MUCHAS veces por frame, provocando que el input "se repita" y dé esa sensación de hypersensibilidad. Por otro lado, aumentar el sleep a 2000 hizo el efecto contrario. Hizo que se viera a 2 fps. Aunque el programa en p5.js sí estaba corriendo a un framerate normal, los datos se envían solamente cada 2.  
  
**⭐ EXPERIMENTO 3 ⭐: reemplazar `b'\xAA'` en el packet por algo común.**  
<a name="ex3"></a>  
> Lo que hice fue ir a la página de terminal que nos diste para ver los datos enviados por el micro:bit y elegir un dato random que vi que se repitiera. En este caso, tomé `f4`. Lo reemplacé en la línea `packet = b'\f4'`.
  
> **Mi predicción:** va a tirarme un error, porque al inicio del código tiene un check que dice: `(serialBuffer[0] !== 0xaa)`. Como checkea el primer dato y es distinto, entonces asumo que directamente me dirá que hay un problema con el paquete.
  
> **Lo que pasó:** exactamente eso :>  
   
<img width="1682" height="561" alt="image" src="https://github.com/user-attachments/assets/6df9101f-beca-45d4-ab76-7bf8a036d521" />

**⭐ EXPERIMENTO 4 ⭐: qué pasa si quito `serialBuffer.splice(0, 8)`?** 
<a name="ex4"></a>  
> **Mi predicción:** sin el splice, el código va a seguir leyendo siempre los 8 datos que mandé inicialmente. Nunca va a leer ningún input nuevo, entonces el programa no va a funcionar más allá del primer frame.  
  
> **Lo que pasó:** crasheó mi ventana D:
> Viéndolo bien, fue porque quitar ese splice creó un loop infinito. El problema no es simplemente que no lea más datos, sino que forma un array súper enorme porque los datos se leen Y LUEGO NO SE ELIMINAN!! entonces la CPU está agregando infinitamente un MONTÓN de datos que la sobrecargan y se desbordan. Por eso crasheó.  
> Es lo mismo que me había sucedido cuando intenté quitar el sleep en la sala de los viernes...  

___

## 📝 Valoración de la unidad 

### 1. Profundidad de la Indagación
| Autoevaluación | Justificación / Evidencias |
|----------------|----------------------------|
| Excelente | Considero que mi indagación fue más allá de los requisitos técnicos. No me limité a implementar el código, sino que investigué el diseño y las implicaciones detrás de cada decisión: investigué a fondo la [elección de 0xAA como header](#EleccionHeader), [en qué casos puede ser implementado un header más largo](#HeaderLargo), la necesidad del checksum, preguntándome por [sus problemas](#ProblemaChecksum) y alternativas, además de explorar escenarios como el [envío de strings de longitud variable](#String) y [alternativas al sleep()](#Sleep) para control de flujo, demostrando curiosidad por los principios de la comunicación de datos y no solo por su implementación. Finalmente, cuestioné también la diferencia en [eficacia entre los dos métodos](#Eficaz) enseñados para enviar datos. |

### 2. Calidad de la Experimentación
| Autoevaluación | Justificación / Evidencias |
|----------------|----------------------------|
| Excelente | Diseñé experimentos creativos y precisos que aislaron y demostraron la necesidad de cada componente del programa. En el [experimento 1](#ex1), quité el checksum para evidenciar visualmente la corrupción de datos y la mezcla entre valores. En el [experimento 2](#ex2), modifiqué el sleep() para analizar su impacto en la saturación, replicando un problema que ya había observado empíricamente en las actividades guiadas. En el [experimento 3](#ex3), cambié el header para probar el mecanismo de sincronización y verificación. El [experimento 4](#ex4), aunque causó un crash, fue súper crucial para entender el consumo del buffer y el peligro de los bucles infinitos. Cada experimento tuvo una hipótesis clara y un análisis de resultados. |

### 3. Análisis y Reflexión
| Autoevaluación | Justificación / Evidencias |
|----------------|----------------------------|
| Excelente | Mi bitácora demuestra una reflexión profunda que conecta la evidencia con la teoría. En la [Actividad 03](#03), analicé el error de sincronización y por qué el framing con header y checksum lo resolvía, articulando el problema a nivel de bytes. Reflexioné sobre la relación entre [eficiencia y complejidad](#Eficaz), concluyendo que sufro yo programando algo más largo para que el programa corra mejor. Analicé mis propios [errores](#errores) (olvidar readSerialData() o serialBuffer) no como fallas, sino como parte del aprendizaje, documentando cómo los solucioné mediante un análisis lógico. 

### 4. Apropiación y Articulación de Conceptos
| Autoevaluación | Justificación / Evidencias |
|----------------|----------------------------|
| Excelente | En la [Actividad 02](#02), expliqué con claridad la estructura de '>2h2B' y la representación de números negativos en complemento a dos. En mi [tabla de investigación](#tabla), articulé la diferencia entre slice y splice, y el rol del DataView, junto a muchas otras preguntas y respuestas sobre temas más complejos de lo enseñado. No me limité a copiar definiciones, sino que investigué, sinteticé y me apropié de conceptos complejos como CRC, control de flujo y protocolos de longitud variable, explicándolos en mis términos. |

# Unidad 3


## 🤔 Fase: Reflect

### 📝 Actividad 08
🌱 **Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?** 
> Una máquina de estados es una forma de programar donde separamos el código a ejecutar en secciones. Cada sección está definida por un estado, unas acciones que realiza, un evento que está esperando y una transición al siguiente estado para pasar a la siguiente sección.  
> Los 4 componentes que utilizamos fueron:  
> 1. Estados  
> 2. Eventos  
> 3. Acciones  
> 4. Transiciones  
  
🌿 **Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender varios eventos y tareas “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit o en p5.js. ¿Qué problema soluciona en comparación con usar funciones como sleep()?**  
> La máquina de estados permite checkear inputs al mismo que tiempo que realiza acciones en ciclo, permitiendo ejecutar el código de manera fluida sin sobrecargar al PC. Además, usar funciones como Sleep() es prácticamente como "pausar" el programa entero, evitando que cualquier otro código se ejecute hasta que este termine. No se recomienda (a menos que se sepa exactamente qué se está haciendo al implementarlo) porque evita la lectura o detección de otros eventos.  

🌼 **Imagina que tienes que añadir una nueva funcionalidad a la bomba: si se recibe un evento especial (por ejemplo, una combinación de botones o un comando serial) mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?**  
> En el bloquecito de ARMED, sacaría una flechita que haga un loop hacia ese mismo bloque (porque no está cambiando esatdo, solamente realizando una acción y regresando al loop). Ahí escribiría que `counter = counter/2`.   

🌻 **Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.**  
> Un vector de prueba es una secuencia de seguimiento al programa donde eliges un estado, unas acciones, predices lo que, en teoría, debería pasar si el programa se ejecuta correctamente... y así al ejecutarlo puedes confirmar si todo está funcionando. Si algo no sucede como lo predices en tu secuencia, entonces te permite identificar el punto exacto del programa en el que está saliendo mal (un cambio de estado, la detección de un evento, una operación...).  

🌱 **¿Qué parte del diseño de la bomba te resultó más desafiante: crear el diagrama de estados o traducir ese diagrama a código? ¿Por qué?**  
> Crear el diagrama de estados, porque me estresa que cada programador tiene una forma a la que está acostumbrado a diseñarlos e interpretarlos. Me da ansiedad pensar que algo no se entienda claramente y sea malinterpretado, entonces sobrepienso cada bloque, color y flecha que pongo. La parte de escribir el código me resulta muy natural.  

🌿 **Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?**  
> Cuando la bomba estallaba por primera vez, escribía un mensaje en la pantalla en color azul. En el estado de CONFIG no tenía una línea para volver a ponerla en negro, entonces el mensaje de configuración al inicio al darle a "T" para volver a intentarlo también aparecía de ese color. Pensar en términos de transiciones me permitió darme cuenta que era necesario agregar ese dato al inicio para mantener el orden en la interfaz. Lo mismo con el tamaño de la letra. También me permitió identificar que debía agregar tanto la letra minúscula como la mayúscula en la sección de detección del input, porque al inicio sólo detectaba el evento si se hacía con el bloc mayus desactivado.   
 
🌼 **El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?**  
>  Sí, comencé simplemente escribiendo los distintos estados y sus condiciones de transición. Después me concentré en conseguir que el input del teclado funcionara correctamente, y finalmente fui llenando de a poco las acciones de cada método. Dejé de último la contraseña para desactivar la bomba porque me pareció la más intimidante, pero realmente fue muy fácil.   

🌻 **Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?**  
>  Para los bosses en un videojuego, para hacer rigs interactivos, para el cambio de escenarios en un videojuego mundo abierto (como el ciclo de día/noche)...  

___

### 📝 Actividad 09

🌱 **Continuar: ¿Qué actividad, explicación o ejemplo de esta unidad te ayudó más a entender el poder de las máquinas de estados? ¿Qué elemento consideras que es indispensable y debería mantener?**
> Creo que definitivamente pasar el código del micro:bit a p5.js, porque me desafió a evaluar si realmente había comprendido el funcionamiento del código lo suficiente como para traducirlo a un lenguaje distinto. Fue muy reconfortante ver que efectivamente había sido capaz de analizarlo y realizarlo con facilidad.  

🌿 **Dejar de hacer: ¿Hubo algún paso o actividad que te pareció confuso? ¿Qué cambiarías o eliminarías?**
> No, todo me pareció súper claro.   

🌼 **Empezar a hacer: ¿Qué te habría ayudado a entender mejor?**
> Nada, todo me quedó súper claro.   

🌻 **Ritmo y dificultad: En una escala del 1 (muy fácil) al 5 (muy difícil), ¿Cómo calificarías la dificultad de pasar del análisis de un programa a diseñar y programar uno complejo? ¿Por qué?**
> 2. Sí requiere de concentración y esfuerzo, pero todos los programas que usamos tienen una documentación excesivamente clara y fácil de comprender.  

🌱 **Comentario adicional: ¿Hay algo más que te gustaría compartir sobre tu proceso de aprendizaje en esta unidad? ¿Algún momento de frustración o de “¡Aha!” que quieras destacar?**
> De frustración cuando anunciaste que ya no habrán más reflects :(  

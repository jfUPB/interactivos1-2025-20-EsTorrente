# Unidad 2


## 🤔 Fase: Reflect
### 📝 Actividad 06  

🌱 **Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?**
> Una máquina de estados es un comportamiento cíclico de funciones que realizan una acción, esperan a un evento específico y cambian su estado para realizar una acción diferente en loop. Sus componentes fundamentales son: eventos, acciones, estados y transiciones.
    
🌿 **Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender un temporizador y botones “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit.   
> porque permite ejecutar el código del temporizador al mismo tiempo que checkea cada frame si el evento del botón pulsado se ha cumplido, permitiendo una interrupción casi imperceptible e inmediata (si bien diseñada) de la acción que se estaba realizando anteriormente.  
  
🌼¿Qué problema soluciona en comparación con usar funciones como sleep()?**  
> El programa puede saltar de cualquier estado a otro si ha sido programado con un evento correspondiente. Si deseo regresar al inicio, puedo programar una transición entre el estado actual al primero. Un programa que simplemente utiliza sleep() para esperar a que finalice una acción solamente podrá ejecutarse linealmente, no volver al inicio al menos que sea reiniciado. Además, según comentaste en la clase, al sleep() hay que "huirle" porque prácticamente detiene totalmente la CPU.  
  
🌻 **Imagina que tienes que añadir una nueva funcionalidad a la bomba temporizada: si se agita (shake) el micro:bit mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?**
> Lo modificaría de forma que se cree una conexión del estado STATE_ARMED hacia una acción independiente (sin cambiar el estado) y regrese de nuevo a STATE_ARMED, siguiendo el evento de `accelerometer.was_gesture('shake')/`. En el código, jamás se estaría saliendo del bloque de código de este estado... simplemente sería un "if" anidado dentro de ella que realice la operación de restar el valor al tiempo restante.  

🌱 **Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.**
> Un vector de prueba es una secuencia específica de acciones y eventos que se realizan al ejecutar un código, permitiendo predecir el comportamiento del programa y confirmar si todo está sucediendo de la manera esperada. Es una herramienta crucial para verificar el funcionamiento porque permite encontrar el punto exacto donde una transición puede estarse rompiendo, así como encontrar pequeñas excepciones a la lógica y corregirlas con facilidad.  

🌼 **¿Qué parte del diseño de la bomba temporizada te resultó más desafiante: crear el diagrama de estados (Actividad 04) o traducir ese diagrama a código MicroPython (Actividad 05)? ¿Por qué?**
> El diagrama de estados. De hecho, yo fui creándolo a medida que iba programando. Me genera mucho estrés trabajar con diagramas porque yo tengo una idea clara del funcionamiento del programa en mi cabeza y lo que debe suceder en cada momento, pero siento que como cada persona tiene una forma distinta de plasmar e interpretar esas ideas en un diagrama, por lo que a veces puede ser muy subjetivo a la hora de calificar. Si yo no estoy ahí para explicar y justificar cada figurita, conexión y texto, siento que no se va a entender claramente.   

🌻 **Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?**
> El scroll estaba provocando que el timer mostrara el número de 2 en 2. Me di cuenta de que el tiempo largo que tomaba mostrar el número provocaba un retraso en el loop del estado de STATE_ARMED, pero si no lo hacía con scroll, el número podía confundirse entre el primer y segundo dígito. Preferí utilizar el delay dentro del scroll para reducir el tiempo que tardaba en completar la animación, permitiendo que el check del estado y la actualización del timer sucedieran con mayor velocidad.  

🌱 **El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?**
> Sí. Comencé simplemente por plantear los distintos estados y las acciones que se estarían realizando dentro de cada una. Luego me concentré en identificar las variables o inputs que debía leer para la transición entre estados, y planteé los eventos que lo detonarían. Finalmente, una vez el programa podía cambiar de manera fluida entre estados al completar cada evento, me concentré en pulir algunos detalles como el sonido.    

🌿 **Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?**
> En videojuegos se puede utilizar para cambiar el tono y la intensidad de la música, crear bosses con múltiples etapas, cambiar la apariencia del ambiente entre día/noche...  

___
### 📝 Actividad 07  

Hay un pequeño error en el diagrama. Accidentalmente se escribió que tanto presionar el botón A como el B en el estado de STATE_CONFIG sumaría 1000 al conteo. Dejando eso de lado, el resto del diagrama es claro y concreto. Hay algunas discrepancias entre el código implementado y las acciones registradas en el diagrama (principalmente el uso de .show en el diagrama y .scroll en el código).
El programa es eficaz y cumple con todos los requisitos. Los vectores de prueba están correctamente planteados. 10/10 (pero ya sabemos que es mejor no utilizar scroll a futuro).
    
<img width="850" height="125" alt="image" src="https://github.com/user-attachments/assets/b2ed0bea-e0b6-43b9-9977-73d653d89039" />

___
### 📝 Actividad 08  

**🌱¿Qué actividad, explicación o ejemplo de esta unidad te ayudó más a entender el poder de las máquinas de estados? ¿Qué elemento consideras que es indispensable y debería mantener?**
> Definitivamente la bomba. El semáforo fue útil como introducción, pero tener que lidiar con otros eventos y cálculos más complejos nos obligó a pensar más estratégicamente y utilizar todas las herramientas que hemos aprendido hasta el momento. Realizar los diagramas también lo considero indispensable, por más que me estrese personalmente.  
  
**🌿 ¿Hubo algún paso o actividad que te pareció confuso, innecesariamente complicado o que aportó poco a tu aprendizaje? ¿Qué cambiarías o eliminarías?**
> No, hasta el momento todo me ha parecido claro y necesario.   
  
**🌼 ¿Qué te habría ayudado a entender mejor?**
> Quizás profundizar un poquito más sobre cómo hacer los vectores de prueba. Al inicio hacía descripciones muy extensas y detalladas de cada acción y cambio en el vector en lugar de una tabla sencilla.
  
**🌻 En una escala del 1 (muy fácil) al 5 (muy difícil), ¿Cómo calificarías la dificultad de pasar del análisis de un programa (Actividad 03) al diseño desde cero de uno complejo (Actividad 04 y 05)? ¿Por qué?**
> 2. Sí requiere de un mayor análisis y concentración, pero no había absolutamente nada que se estuviera exigiendo en el programa que no estuviera ejemplificado de forma clara en los ejercicios anteriormente realizados. Teniéndolos como muestra, se trata simplemente de adaptar la misma estructura con un par de cambios menores.  
  
**🌱 ¿Hay algo más que te gustaría compartir sobre tu proceso de aprendizaje en esta unidad? ¿Algún momento de frustración o de “¡Aha!” que quieras destacar?**
> No, todo el proceso fue bastante suave y constante. Quizás el momento en el que me dí cuenta de que el uso del scroll estaba impidiendo la ejecución fluida del programa, y me di cuenta de la importancia de evitarlo o usarlo sólo cuando es totalmente necesario.

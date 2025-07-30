# Unidad 1

## 🤔 Fase: Reflect
### 📝 Actividad 07
***Parte 1: recuperación de conocimiento (Retrieval Practice)***
  
🌱 **Basándote en los ejemplos que vimos de sistemas físicos interactivos al iniciar el curso, describe las tres características que definen a un sistema físico interactivo.**  
> 1. Procesado en tiempo real (creo?)
> 2. Tiene cierto nivel de autonomía
> 3. Sigue reglas y direcciones preestablecidas.

🌿**Explica el modelo input-process-output de Patrick Hübner usando como ejemplo el sistema que construiste con micro:bit y p5.js en la Actividad 06. ¿Cuál fue el input, cuál fue el proceso y cuál fue el output?**  
> 🍃**INPUT:** Los botones y el serial envían la señal de interacciones con el micro:bit al programa.  
> 🍂**PROCESO:** El programa procesa el input, identifica de qué botón viene, y envía un dato específico al programa p5.js. El programa p5.js recibe el dato enviado, filtra su tipo, y realiza los cálculos para mover el círculo. Esto se ejecuta cada frame.  
> 🍁**OUTPUT:** En la pantalla del editor de p5.js, se puede observar la imagen del círculo dibujado y los respectivos cambios a su color y posición.  

🌼 **¿Cuál es la función de la línea uart.write('A') en el código del micro:bit y qué función en p5.js se encarga de “escuchar” ese mensaje?**  
> Su función es enviar un caracter al programa de p5.js que le permita identificar que el botón A está siendo presionado, y que pueda ejecutar la acción asignada La función que se encarga de escuchar a ese mensaje es:   
  > `if (dataRx == "A"){}`, que pasa el filtro identificando el caracter.  

🌻 **¿Cuál es la diferencia fundamental entre el arte/diseño tradicional y el arte/diseño generativo?**
> Que la tecnología juega un papel principal o equitativo frente al rol activo del humano involucrado. En el arte tradicional, la persona utiliza herramientas para conseguir el producto final... pero todas las decisiones son tomadas por el humano (como en qué dirección mover el pincel, qué color usar...). En comparación, en el arte generativo se le cierto nivel de libertad y autonomía a la máquina, cediendo parte del control (a pesar de que siempre sigue unas reglas básicas establecidas). 

🍃**Imagina que quieres que un círculo en p5.js cambie a un color aleatorio cada vez que sacudes el micro:bit. Describe qué tendrías que programar en el micro:bit y qué tendrías que programar en p5.js para lograrlo.** 
> 1. Importar la biblioteca de funciones necesarias en el programa de micro:bit
> 2. Iniciar la comunicación serial con el badwith establecido (no recuerdo el número)
> 3. Usar un display.show para mostrar una imagen que confirme que el programa ha sido cargado correctamente en el micro:bit
> 4. Usar un if (función que llama al acelerómetro e identifica si lo sacudieron), uart.write('A'), sleep(100).
> 5. En el programa de p5.js, importar la biblioteca que permite que se comunique con el micro:bit
> 6. Crear 3 variables que sirvan para el botón de iniciar la conexión con el port, abrir y cerrarlo, y el bool que diga si ya fue inicializado o no.
> 7. En Setup(), crear el botón que conecta/desconecta el port, y la función que llama con el clic
> 8. En Draw(), Crear el método que usa port.clear para borrar los datos previamente enviados si: el port ha sido abierto, y el bool de conexión iniciada = false. Cuando termina le hace set al bool en true para evitar que el ciclo siga.
> 9. Crear una variable para r, g, b.
> 10. Identificar si el port ha enviado un mensaje, leer ese mensaje y decir que si es = "A", entonces ejecutar un código que asigne valores aleatorios a las variables r, g, b con random().
> 11. Usar stroke() para cambiar el color del fill de acuerdo a las variables r, g, b.
> 12. Dibujar el círculo con el radio deseado.
___
  
🌱¿Qué fue más desafiante para ti en esta unidad: la parte conceptual (entender qué es un sistema físico interactivo) o la parte técnica (hacer que el micro:bit y p5.js se comunicaran)? ¿Por qué?  
> Un poquito más la conceptual, porque es muy fácil obviar algunos de los inputs presentes en sistemas físicos interactivos más complejos. Lo complicado no fue entender la teoría, sino no limitarse en el razonamiento.

🌿Describe el momento “¡Aha!” que tuviste cuando lograste que una acción en el micro:bit (presionar un botón, sacudirlo) tuviera un efecto visible en el canvas de p5.js por primera vez. ¿Qué fue lo que entendiste en ese instante?
> Que algo tan sencillo como realizar una acción y ver algo novedoso suceder como consecuencia puede provocar una reacción muy eufórica en las personas. En el momento en el que se nos dió libertad para probarlo, lo único que escuchaba era lo emocionados que se sintieron mis compañeros. También, al ver el panel derecho con todos los tipos distintos de inputs que recibe el micro:bit, me di cuenta de que hay una cantidad gigantesca de posibilidades y combinaciones posibles, sobretodo de la mano de un programa p5.js.

🌼Al inicio de la unidad te pregunté: “¿Este curso para qué me sirve?”. Después de experimentar y construir tu primer prototipo, ¿Cómo ha cambiado o se ha vuelto más concreta tu respuesta a esa pregunta?  
> Sigue siendo la misma. Yo diría que me siento aún más inspirada. Cada vez que hacemos una actividad nueva, se me ocurren mil posibilidades más para incluirla en proyectos futuros. Me emociona muchísimo pensar en el futuro del arte interactivo. También siento que debería ser más común hacer una pequeña introducción a la programación usando micro:bits en los colegios, porque podría ayudar a sembrar esa emoción y curiosidad por la tecnología en los niños.

🌻El tutorial de la Actividad 05 te llevó paso a paso. ¿Cómo te sentiste con ese método de aprendizaje? ¿Te dio seguridad o preferirías haberlo intentado por tu cuenta desde el principio?
> Me gustó mucho ir paso a paso, pero me gustó aún más que se mostrara el error. Siento que es una buena manera de aprender a no fiarse simplemente de las instrucciones dadas, copiar y pegar... sino realmente comprender qué estamos escribiendo y predecir antes de ejecutar si el programa funcionará (como nos han enseñado).
  
___
### 📝 Actividad 08
🌱 *ACTIVIDAD 1: [5]/5*  
Comentarios:  
> 🐟 Las respuestas son completas, claras y concisas.
 
🌿 *ACTIVIDAD 2: [5]/5*  
Comentarios:  
> 🐟 Las respuestas son claras. Hace falta mencionar que el sistema tiene cierto grado de autonomía en el proceso, pero todo lo demás es completamente claro.
 
🌱 *ACTIVIDAD 3: [5]/5*  
Comentarios:  
> 🐟 Los inputs, outputs y el proceso están descritos claramente y no omiten ninguno de los componentes.
 
🌿 *ACTIVIDAD 4: [5]/5*  
Comentarios:  
> 🐟 El programa es increíblemente creativo, interesante, y cumple con todos los requisitos solicitados. Demuestra un nivel superior de interés por la temática, y un gran entendimiento del simulador y código.
 
=======================
 
🌱 *ACTIVIDAD 5: [5]/5*  
Comentarios:  
> 🐟 La explicación es detallada y cumple con todos los requisitos. Se explica claramente el envío constante del estado del botón A, la lectura en cada frame de aquel dato y cómo esto afecta el color del cuadrado.
 
🌿 *ACTIVIDAD 6: [5]/5*  
Comentarios:  
> 🐟 El código es funcional y se hace entrega de todos los elementos solicitados.
___
### 📝 Actividad 09
**🌱Continuar: ¿Qué actividad, video o ejemplo de esta unidad te resultó más inspirador o te ayudó más a entender el potencial de los sistemas físicos interactivos?**
> La de el chico tocando batería. Me gustó demasiado el hecho de que el humano seguía teniendo igual cantidad de participación que el programa. Más que simplemente escribir algunas líneas de código y dejar que las obras de arte las haga la máquina mientras espero, me encanta la idea de que sea una colaboración más activa.

**🌿Dejar de hacer: ¿Hubo alguna parte que te pareció demasiado abstracta, muy rápida o confusa? ¿Hay algo que crees que podríamos cambiar para que sea más claro?**
> No, todo fue supremamente claro.

**🌼Empezar a hacer: ¿Qué te genera más curiosidad ahora? ¿Te gustaría explorar más sensores del micro:bit (luz, temperatura), crear visualizaciones más complejas en p5.js o ver más ejemplos de proyectos artísticos?**
> Rotundo sí a todo. 

**🌻Balance inspiración vs. técnica: ¿Cómo sentiste el equilibrio entre ver los videos inspiradores de la Actividad 01 y la parte técnica de conectar las herramientas en las actividades 03-06?**
> Perfecta. Considero que esa inspiración sí es totalmente necesaria para darse una idea de todo lo que podría ser posible. Ayuda a reducir un poco el miedo de trabajar con sistemas desconocidos, reemplazándolo por curiosidad.

**🌱Comentario adicional: ¿Hay algo más que quieras compartir sobre tu experiencia en esta unidad introductoria?**
> Me encantó trabajar con el micro:bit. Siento que es simple, amigable, muy novedoso y ofrece bastantes posibilidades.

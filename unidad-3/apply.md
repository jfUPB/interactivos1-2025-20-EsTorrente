# Unidad 3


## 🛠 Fase: Apply

```
function setup() {
  createCanvas(windowWidth, windowHeight);

  background(200);

  textSize(30);
  textAlign(CENTER, CENTER);
  
  state = 'CONFIG'
  counter = 20
  startTime = 0;
  event = '0'
  
  let PASSWORD = ['A','B','A'];
  let passwordKey = []; 
  keyIndex = 0;
  
}

function draw() {
  
  //================ config ===============
  if (state === 'CONFIG')
    {
      background(200);
      
      text('Presione "A" para aumentar 1 segundo, "B" para restar.', width/2, 40);
      text(counter, width/2, height/2);
      
      if (event === 'A' & counter < 60)
        {
          event = '0';
          counter += 1;
        }
      
      if (event === 'B' & counter > 10)
        {
          event = '0';
          counter -= 1;
        }
      
      if (event === 'S')
        {
          event = '0';
          startTime = millis();
          state = 'ARMED';
        }
    }
  
  //================ armada ===============
  
  if (state === 'ARMED')
    {
      timePassed = (millis() - startTime)/1000;
      timeLeft = int(counter - timePassed);
      
      if (timeLeft > 0)
        {
          background(200);
          text(timeLeft, width/2, height/2);
        }
      else if (timeLeft == 0)
        {
          background(200);
          state = 'EXPLODED';
        }
      
      //coso contraseña
      if (event === 'A')
        {
          event = '0';
          passwordKey[keyIndex] = 'A';
          keyIndex++;
        }
      
      if (event === 'B')
        {
          event = '0';
          passwordKey[keyIndex] = 'B';
          keyIndex++;
        }
      
      if (keyIndex == PASSWORD.length)
        {
          passIsOkay = True;
          
          for (let x = 0; x < PASSWORD.lenght; i ++)
            {
              
            }
        }
    }
  
  //================ explota ===============
  
  if (state === 'EXPLODED')
    {
      background(200);
      
      text('Perdiste. Presiona "T" para reiniciar :(', width/2, 40);
      
      if (event === 'T')
        {
          event = '0';
          counter = 20;
          startTime = millis();
          state = 'CONFIG'
        }
      
    }
}

function keyPressed()
{
  if (key === 'a')
    {
      event = 'A';
    }
  if (key === 'b')
    {
      event = 'B';
    }
  if (key === 's')
    {
      event = 'S';
    }
  if (key === 't')
    {
      event = 'T';
    }
}

```

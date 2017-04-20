# detonador
Jogo simples em Processing chamado detonador, que irá funcionar em uma espécie de consola arcada dos anos 80, incorporando um detonador fisico que ira provocar a explosão e pontuação do jogo 

![image](https://{scontent.fopo1-1.fna.fbcdn.net/v/t31.0-8/17039379_670172063193311_3224195269592974630_o.jpg?oh=6929e4d17d581dfb14b7$})

```processing
import controlP5.*;
 
 ControlP5 cp5;
    boolean display = false;
    int xp = 260;
    int step = 65;
    int xp2 = 260;
    int step2 = 65;
    PImage bg;
    PImage detonator;
    PImage menu;
    PFont font;
    String time = "10";
    int t;
    int interval = 10;
    int gamestate = 0;
    int gameover = 0;
    float score = 0;
    Button start;
    Button back;
    
    void setup() {
      size(600, 600);
      smooth();
      noStroke();
      bg = loadImage("fundo.jpg");
      detonator = loadImage("rs_detonator.png");
      menu = loadImage("menubg.jpg");
      font = createFont("Arial", 80);
      textFont(font);
      
      cp5 = new ControlP5(this);
      start = cp5.addButton("START").setValue(0).setPosition(225,400).setSize(180,40);
      back = cp5.addButton("BACK").setValue(0).setPosition(225,400).setSize(180,40);
    }

     void drawHumidityBar() {  
       rect(30,250,40,250);
       fill(255,200,200);
      }
      
      void drawExplosionBar() { 
        noStroke();
       rect(530,250,40,250);
       fill(255,200,200);
       
      }
      
      void drawHumidityPaddle() {
        noStroke();
          rect(30, xp, 40, 20);
          fill(255);
      }
      
      void drawExplosionPaddle() {  
          rect(530, xp2, 40, 20);
          fill(255);
      }

    void draw() {
      
     if (gamestate == 0){
       
       background(menu);
       
       back.hide();
       start.show();
        
       cp5.addCallback(new CallbackListener() {
    
         public void controlEvent(CallbackEvent theEvent) {
      switch(theEvent.getAction()) {
        case(ControlP5.ACTION_PRESS): start.hide();  gamestate = 1; break;
       
      }
    }
  }
  );
       
      
       
     } else if (gamestate == 1){
       
      background(bg);

      image(detonator,200,330);
    

    
     
    t = interval-int(millis()/1000);
    
    if (t > 0 && t <= 10){
     
      time = nf(t , 2); 
      text(time, width/2, height/5);
      textAlign(CENTER);
    }
    
    if(t == 0){
      step =0;
      step2=0;
      
      score = -xp*0.4 + xp2*0.6;
      text("GAME OVER",width/2, height/5);
      text(score,width/2, height/3);
  
      back.show();
       
     
      cp5.addCallback(new CallbackListener() {
    
         public void controlEvent(CallbackEvent theEvent) {
      switch(theEvent.getAction()) {
        case(ControlP5.ACTION_PRESS): gamestate = 0; break;
       
      }
    }
  });
      
 
  }

   
      drawHumidityBar();
      drawExplosionBar();
      drawHumidityPaddle();
      drawExplosionPaddle();
      
      // Humidity Paddle Movement
      xp+=step;
      if (xp > 450) {
        
        step = -1;
      }
      if (xp < 260) {
        
        step = 1;
      }
      
      
      xp2+=step2;
      if (xp2 > 450) {
        
        step2 = -2;
      }
      if (xp2 < 260) {
        
        step2 = 2;
      }
      
     }
     
    }

```

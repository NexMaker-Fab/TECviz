# Introduction
[Processing](https://processing.org/) is a flexible software sketchbook and a language for learning how to code. Since 2001, Processing has promoted software literacy within the visual arts and visual literacy within technology. There are tens of thousands of students, artists, designers, researchers, and hobbyists who use Processing for learning and prototyping.

# Similar Softwares
* [p5.js](https://p5js.org/): is a JavaScript library that is similar to Processing in terms of syntax and functionality. It is designed for web-based graphics and interactive media, and can be used to create dynamic visualizations and interactive user interfaces. p5.js is often used in creative coding and web development, and is well-suited for projects that involve real-time data, user input, and web APIs.

* [OpenFrameworks](https://openframeworks.cc/): is an open-source C++ toolkit that is similar to Processing in terms of its emphasis on creative coding and multimedia applications. It provides a collection of libraries and tools for working with graphics, audio, video, and other media, and is well-suited for projects that require low-level control and performance optimization. OpenFrameworks can be used to create interactive installations, virtual and augmented reality experiences, and other multimedia applications.

* [TouchDesigner](https://derivative.ca/): is a node-based visual programming environment that is similar to Processing in terms of its emphasis on real-time graphics and interactive media. It is designed for creating interactive installations, live performances, and immersive experiences, and can be used to create dynamic visualizations and interactive interfaces. TouchDesigner provides a wide range of tools for working with graphics, video, audio, and sensors, and is well-suited for projects that require advanced multimedia integration and real-time control.

## Reference
* [Nexmaker](https://www.nexmaker.com/doc/10Interface-application-programming/processing.html)
* [Learning Processing](https://www.amazon.com/gp/product/0123944430/ref=as_li_ss_tl?ref_=nav_ya_signin&linkCode=sl1&tag=processing09-20&linkId=fb0eeedd8fb1016a790e83d538a1c030)

# Example Processing
Mouse Interaction: Draws squares in the screen with mouse movement, on click clears the screen and change background color.

<img src="https://i.ibb.co/KxZYPrf/sketch-230326a-2023-03-26-23-19-27-Adobe-Express.gif" alt="sketch-230326a-2023-03-26-23-19-27-Adobe-Express" border="0">

>Code

```C++
void setup() {
  size(1400, 800);
}

void draw() {
  // change color based on mouse position
  float r = map(mouseX, 0, width, 0, 255);
  float g = map(mouseY, 0, height, 0, 255);
  float b = map(mouseX + mouseY, 0, width + height, 0, 255);
  fill(r, g, b);

  // draw rectangle at mouse position
  rect(mouseX, mouseY, 50, 50);
}

void mouseClicked() {
  // clear screen
  background(255);
  
  // set random background color
  float r = random(255);
  float g = random(255);
  float b = random(255);
  background(r, g, b);
}
```

# Processing Minigame
Keyboard Interaction: Arrow keys controls a square in the screen while random particles are generated, capturing each particle increases the score in 1.

<img src="https://i.ibb.co/8bP9ZZK/square-eats-circle-the-game-2023-04-03-22-04-56-Adobe-Express.gif" alt="square-eats-circle-the-game-2023-04-03-22-04-56-Adobe-Express" border="0">

>Code

```C++
int playerX = 50;
int playerY = 50;
int playerSize = 50;

int score = 0;

int numCircles = 10;
int[] circleX = new int[numCircles];
int[] circleY = new int[numCircles];
int[] circleSize = new int[numCircles];
int[] circleXSpeed = new int[numCircles];
int[] circleYSpeed = new int[numCircles];

void setup() {
  size(400, 400);

  for (int i = 0; i < numCircles; i++) {
    circleX[i] = (int) random(width);
    circleY[i] = (int) random(height);
    circleSize[i] = (int) random(20, 50);
    circleXSpeed[i] = (int) random(-5, 5);
    circleYSpeed[i] = (int) random(-5, 5);
  }
}

void draw() {
  background(255);

  // draw circles
  for (int i = 0; i < numCircles; i++) {
    ellipse(circleX[i], circleY[i], circleSize[i], circleSize[i]);
    circleX[i] += circleXSpeed[i];
    circleY[i] += circleYSpeed[i];

    // check if circle is offscreen and reset its position and speed
    if (circleX[i] < 0 || circleX[i] > width || circleY[i] < 0 || circleY[i] > height) {
      circleX[i] = (int) random(width);
      circleY[i] = (int) random(height);
      circleXSpeed[i] = (int) random(-5, 5);
      circleYSpeed[i] = (int) random(-5, 5);
    }

    // check if player captured circle and increase score
    float distance = dist(circleX[i], circleY[i], playerX + playerSize/2, playerY + playerSize/2);
    if (distance < circleSize[i]/2 + playerSize/2) {
      score++;
      circleX[i] = (int) random(width);
      circleY[i] = (int) random(height);
      circleXSpeed[i] = (int) random(-5, 5);
      circleYSpeed[i] = (int) random(-5, 5);
    }
  }

  // draw player
  rect(playerX, playerY, playerSize, playerSize);

  // draw score
  textSize(20);
  fill(0);
  text("Score: " + score, 10, 25);
}

void keyPressed() {
  if (keyCode == UP) {
    playerY -= playerSize;
  } else if (keyCode == DOWN) {
    playerY += playerSize;
  } else if (keyCode == LEFT) {
    playerX -= playerSize;
  } else if (keyCode == RIGHT) {
    playerX += playerSize;
  }
}
```

## Processing and Arduino
In this example we will show how to control a LED Strip using processing to create GUI

>Materials Used:
* 1 Arduino UNO
* 1 RGB Strip
* Breadboard
* Jumper wires

>Circuit Diagram:

<img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2016/09/WS2812B-with-Arduino_bb.png?resize=700%2C423&quality=100&strip=all&ssl=1" alt="diagram" border="0">

>Arduino Code:

```C++
#include <Adafruit_NeoPixel.h>

const int numPixels = 256; // Number of pixels in the LED strip
const int pixelPin = 6; // Pin connected to the LED strip
Adafruit_NeoPixel pixels(numPixels, pixelPin, NEO_GRB + NEO_KHZ800); // NeoPixel object

void setup() {
  Serial.begin(9600); // Initialize serial communication
  pixels.begin(); // Initialize NeoPixel object
}

void loop() {
  if (Serial.available() > 0) { // If data is available on serial port
    char command = Serial.read(); // Read the command
    if (command == 'r') { // If command is 'r' (red)
      for (int i = 0; i < numPixels; i++) { // Loop through all pixels
        pixels.setPixelColor(i, pixels.Color(255, 0, 0)); // Set pixel color to red
      }
      pixels.show(); // Update the LED strip
    } else if (command == 'g') { // If command is 'g' (green)
      for (int i = 0; i < numPixels; i++) { // Loop through all pixels
        pixels.setPixelColor(i, pixels.Color(0, 255, 0)); // Set pixel color to green
      }
      pixels.show(); // Update the LED strip
    } else if (command == 'b') { // If command is 'b' (blue)
      for (int i = 0; i < numPixels; i++) { // Loop through all pixels
        pixels.setPixelColor(i, pixels.Color(0, 0, 255)); // Set pixel color to blue
      }
      pixels.show(); // Update the LED strip
    }
  }
}
```

>Processing Codes:

```C++
import controlP5.*;                              //import ControlP5 library
import processing.serial.*;

Serial port;

ControlP5 cp5;                                   //create ControlP5 object
PFont font;

void setup() {

  size(480, 360);                                //window size, (width, height)
  port = new Serial(this, "COM3", 9600);         //Change Your COM Port Here

  cp5 = new ControlP5(this);
  font = createFont("calibri light bold", 20);   //Custom Font
 
  cp5.addButton("red_on")                       //Name of the Button
    .setPosition(260, 60)                        //(x,y) top left Corner
    .setSize(180, 60)                            //(width, height)
    .setFont(font)
    .setColorBackground(color(255, 0, 0))
    ;
  cp5.addButton("green_on")                     //Name of the Button
    .setPosition(260, 160)                       //(x,y) top left Corner
    .setSize(180, 60)                            //(width, height)
    .setFont(font)
    .setColorBackground(color(0, 255, 0))
    ;
  cp5.addButton("blue_on")                      //Name of the Button
    .setPosition(260, 260)                       //(x,y) top left Corner
    .setSize(180, 60)                            //(width, height)
    .setFont(font)
    .setColorBackground(color(0, 0, 255))
    ;
}

void draw() {

  background(50, 50, 50);                        //background color of window (r, g, b)
  //Title
  fill(255, 255, 255);                           //text color (r, g, b)
  textFont(font);
  text("Simple RGB Control", 150, 30);           //("text", x, y)
}

void green_on() {
  port.write('g');
}

void blue_on() {
  port.write('b');
}

void red_on() {
  port.write('r');
}
```

# Output Result

<img src="https://i.ibb.co/Mg2VJxS/VID-20230403-231644-Adobe-Express.gif" alt="VID-20230403-231644-Adobe-Express" border="0">

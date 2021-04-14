 # Table of Contents
 
1. [Connections](#Connections)
 
 2. [Materials](#Materials)

3. [Build Instrucions](#BuildInstrucions)
 
4. [The Finished Project](#TheFinishedProject)

5. [Bugs](#Bugs)

 6. [Plans](#PlansFeatures)

 7. [Code](#Code)

 8. [Sources](#Sources)
 
 9. [Credits](#Credits)

 10. [Usage](#Usage) 
 
 
  # Motion Sensor LED light Strip Dart Board 
 
 The instrutions on making this project the motion sensor LED light strip dart board for CS 207. This project is a step by step on making the light up dart board, all the steps are provided down below.  

# Connections
1. ![Motion Sensor LED light_bb](https://user-images.githubusercontent.com/79604213/114316351-655e2880-9ac0-11eb-8b34-af85bee5b271.jpg)



2. ![Motion Sensor LED light_schem](https://user-images.githubusercontent.com/79604213/114316425-c554cf00-9ac0-11eb-97f9-64324b35567e.jpg)



# Materials

1. Arduino
2. BreadBoard
3. LED Light Strips (any length is good)
4. Motion Sensor - HC-SR04
5. Battery Pack (to be able to move around easier)
6. 9 cords
7. Dart board
8. Duck tape (hold up the lights)
9. 1 screw
10. A dart 


# Build Instrucions 

 1. To have all equipment ready
 2. Get your Arduino and Breadboard connected to your computer make sure to have <Adafruit_NeoPixel.h> located in the Sketch and Include Library.
 3. Connect the 5V and Ground cords from the arduino to the breadboard.
 4. Connect the Motion Sensor cords (the Motion Sensor are labelled) from Ground pin to ground on the bread board, connect the Echo pin to pin 8 on the Arduino, connect the Trig pin to pin 7 on the Arduino, and Vcc pin connect it to the 5V on the bread board.
 5. Connect the LED Strip Light ( the LED Strip Light is labelled) from the DO pin connect it to Ground on the bread board, the DI pin connect it to pin 2 on the Arduino, and the Vcc pin connect it to 5V on the bread board.
 6. Put the code the Arduino ( the code is at # code).
7. Upload it to your Arduino.
 8. Plug in the battery pack to your Arduino.
 9. Assemble the Arduino to dart board.
 10.  Make a platform or something to hold your Arduino up.
 11. Duck tape the lights around the dart board.
 12. Screw the Motion Sensor on the dart board.
 13. Try it out.





# The Finished Project
1. ![IMG_8079](https://user-images.githubusercontent.com/79604213/114316661-ae62ac80-9ac1-11eb-9325-913dd6ee87a6.JPG)


2. ![IMG_8078](https://user-images.githubusercontent.com/79604213/114316664-b15d9d00-9ac1-11eb-8040-4467c226a3d3.JPG)


3. https://www.youtube.com/watch?v=rn-BdLi8LR4






# Bugs

There was a few bugs to making this project: 

1. The code was diffault as the person that I was trying to follow had a bad code as they never gave good examples so I had to get help setting it up.
2. The equipment the LED strip light and motion sensor I never used those two equipment before so I got confused at the beginning.
3. The motion sensor can only go so far so hitting the dart board you would have to shot close to the motion sensor to activate it.
4. The motion sensor not being able to shut off while an object is infront of itfor a long time.

# Plans Features
The things that would have made it better would have been adding three more motion sensors to be able to reach the other sides of the dart board and not just get the one side of the dart board.


# Code

//written by Melina Young

#include <Adafruit_NeoPixel.h>
#ifdef _AVR_
#include <avr/power.h>
#endif

#define LED_PIN 2

//Setup the variables for the HC-SR04
const int trigPin = 8;
const int echoPin = 7;

#define NUM_LEDS 30



Adafruit_NeoPixel strip = Adafruit_NeoPixel(150, LED_PIN, NEO_GRB + NEO_KHZ800);

void setup() {

  Serial.begin(9600);
  strip.begin();
  strip.show();
}
void loop()
{ long duration, inches, cm;
  pinMode(trigPin, OUTPUT);
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  //
  pinMode(echoPin, INPUT);
  duration = pulseIn(echoPin, HIGH);
  inches = microsecondsToInches(duration);
  Serial.print(inches);
  Serial.println();

  if (inches <= 8) {
    // Send a theater pixel chase in...
    theaterChase(strip.Color(127, 127, 127), 50); //white
    theaterChase(strip.Color(127, 0, 0), 50); //Red
    theaterChase(strip.Color(127, 127, 127), 50); //white
    theaterChase(strip.Color(127, 0, 0), 50); //Red
    theaterChase(strip.Color(0, 0, 127), 50); //Blue
  }

  else if (inches >= 8) {
    for (int i = 0; i < strip.numPixels();
         i++) {
      strip.setPixelColor(i, 0, 0, 0);
    }
    strip.show(); // turn off LED strip
  }

  delay(100);
}

void theaterChase(uint32_t c, uint8_t wait)
{
  for (int j = 0; j < 10; j++) { //do 10 cycles of chasing
    for (int q = 0; q < 3; q++) {
      for (int i = 0; i < strip.numPixels(); i = i + 3) {
        strip.setPixelColor(i + q, c); //turn every third pixel on
      }
      strip.show();
      delay(wait);
      for (int i = 0; i < strip.numPixels(); i = i + 3) {
        strip.setPixelColor(i + q, 0); //turn every third pixel off
      }
    }
  }
}


long microsecondsToInches(long microseconds)
{
  return microseconds / 74. / 2;

}

# Usage 
This project can be used to have fun with friends and add a bit of light to the activity.



# Sources
https://www.youtube.com/watch?v=7fJ_bGO4FRU 


# Credits
1. My Lab Prof for helping with the code as it wasn't working 
2. My Dad for helping setup the Arduino to the dart board
3. The video that gave the idea https://www.youtube.com/watch?v=7fJ_bGO4FRU 


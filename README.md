# Arduino Bike GPS

This is a technical manual to create a LED powered GPS system for your bicycle.
BikeGPS is a way to visualize and hear the route a user has to ride on their bike to their destination while being able to keep two hands at the wheel at all times.

The LEDs and voice instructions on Bike GPS will make the driver know where he is headed. The driver can always have two hands at the wheel and is also more visible to others in traffic, because of the LEDs. The user uses Google Maps for the route, after which the user will connect to the Bike GPS device via Bluetooth, Bike GPS will set the light intensity, all set and done.

---
## What's needed?
### Software
- Arduino editor
- Adafruit Neopixel library
- Website with Google Maps API

### Hardware
- Arduino / NodeMCU
- BlueTooth module
- Neopixel straight LED strip with 5 LEDs
- LDR sensor
- Power source
- Wires

Connect the Neopixel to a digital pin, 5v and GND.
Connect the LDR to an analog pin, 3v3 and GND.

---
## Code
### Arduino

This code has every indicator for the directions, wrong turns or when you reached your destination.
```
#include <Adafruit_NeoPixel.h>
#ifdef __AVR__
  #include <avr/power.h>
#endif

#define PIN D1

int sensorPin = A0; // select the input pin for LDR
int sensorValue = 0; // variable to store the value coming from the sensor
int lum = (sensorValue / 4) + 10;;
// Parameter 1 = number of pixels in strip
// Parameter 2 = Arduino pin number (most are valid)
// Parameter 3 = pixel type flags, add together as needed:
//   NEO_KHZ800  800 KHz bitstream (most NeoPixel products w/WS2812 LEDs)
//   NEO_KHZ400  400 KHz (classic 'v1' (not v2) FLORA pixels, WS2811 drivers)
//   NEO_GRB     Pixels are wired for GRB bitstream (most NeoPixel products)
//   NEO_RGB     Pixels are wired for RGB bitstream (v1 FLORA pixels, not v2)
//   NEO_RGBW    Pixels are wired for RGBW bitstream (NeoPixel RGBW products)
Adafruit_NeoPixel strip = Adafruit_NeoPixel(5, PIN, NEO_GRB + NEO_KHZ800);

// IMPORTANT: To reduce NeoPixel burnout risk, add 1000 uF capacitor across
// pixel power leads, add 300 - 500 Ohm resistor on first pixel's data input
// and minimize distance between Arduino and first pixel.  Avoid connecting
// on a live circuit...if you must, connect GND first.

void setup() {
  Serial.begin(9600); //sets serial port for communication
  strip.begin();
  strip.show(); // Initialize all pixels to 'off'
}

void loop() {
  sensorValue = analogRead(sensorPin); // read the value from the sensor
  Serial.println(sensorValue); //prints the values coming from the sensor on the screen
  lum = (sensorValue / 4) + 10; //sets the intensity of the LEDs
  for(uint16_t i=0; i<strip.numPixels(); i++) {
    strip.setPixelColor(i, strip.Color( lum, lum, lum ));
    strip.show();
  }
  delay(1500);
  
  sensorValue = analogRead(sensorPin); // read the value from the sensor
  lum = (sensorValue / 4) + 10; //sets the intensity of the LEDs
  
  strip.setPixelColor( 0,  strip.Color( 0, lum, 0 ) );
  Serial.println(lum);
  strip.show();
  delay(1500);
  
  sensorValue = analogRead(sensorPin); // read the value from the sensor
  lum = (sensorValue / 4) + 10; //sets the intensity of the LEDs
  
  strip.setPixelColor( 1,  strip.Color( 0, lum, 0 ) );
  Serial.println(lum);
  strip.show();
  delay(1500);

  sensorValue = analogRead(sensorPin); // read the value from the sensor
  lum = (sensorValue / 4) + 10; //sets the intensity of the LEDs

  strip.setPixelColor( 2,  strip.Color( 0, lum, 0 ) );
  Serial.println(lum);
  strip.show();
  delay(1500);

  sensorValue = analogRead(sensorPin); // read the value from the sensor
  lum = (sensorValue / 4) + 10; //sets the intensity of the LEDs

  strip.setPixelColor( 3,  strip.Color( 0, lum, 0 ) );
  Serial.println(lum);

  strip.show();
  delay(1500);

  sensorValue = analogRead(sensorPin); // read the value from the sensor
  lum = (sensorValue / 4) + 10; //sets the intensity of the LEDs

  strip.setPixelColor( 4,  strip.Color( 0, lum, 0 ) );
  Serial.println(lum);
  strip.show();
  delay(1500);

  sensorValue = analogRead(sensorPin); // read the value from the sensor
  lum = (sensorValue / 4) + 10; //sets the intensity of the LEDs

  strip.setPixelColor( 0,  strip.Color( lum, 0, 0 ) );
  strip.setPixelColor( 1,  strip.Color( lum, lum, lum ) );
  strip.setPixelColor( 2,  strip.Color( lum, 0, 0 ) );
  strip.setPixelColor( 3,  strip.Color( lum, lum, lum ) );
  strip.setPixelColor( 4,  strip.Color( lum, 0, 0 ) );
  Serial.println(lum);

  strip.show();
  delay(4000);
  
  sensorValue = analogRead(sensorPin); // read the value from the sensor
  lum = (sensorValue / 4) + 10; //sets the intensity of the LEDs

  strip.setPixelColor( 0,  strip.Color( 0, lum, 0 ) );
  strip.setPixelColor( 1,  strip.Color( lum, lum, lum ) );
  strip.setPixelColor( 2,  strip.Color( 0, lum, 0 ) );
  strip.setPixelColor( 3,  strip.Color( lum, lum, lum ) );
  strip.setPixelColor( 4,  strip.Color( 0, lum, 0 ) );
  Serial.println(lum);

  strip.show();
  delay(4000);
}
```


# Topic

<br>
<div class="loader"><img src="https://i.ibb.co/WGWG8vZ/lamp-2.jpg" alt="Kazelight"/></div>

>Kazelight is a stylish table lamp that doubles as an air quality monitor. It uses a combination of air sensors and RGB Leds to create a visually appealing and interactive experience for users.

# SDGs
>We are aiming to SDG 3 and 13, Good health and well-being and also climate action.
>![#](https://i.ibb.co/64kXN61/E-SDG-Poster-2019-without-UN-emblem-WEB.png)
>![#](https://i.ibb.co/bzgTwzv/E-GIF-03.gif)

# User Research
Target Users: Health-conscious individuals, people with allergies or respiratory issues, and those interested in home decor and technology.

# Innovation
Features:

* Monitors indoor air quality and displays readings on a small LCD screen
* An RGB matrix changes the colors based on the air quality readings (e.g. green for good air quality, yellow for moderate, red for poor) the color from the LEDs is spread inside the lamp creating an atmospheric lighting
* Creates a visual-appealing and relaxing light effect, using a light pulse that change the frequency according to air quality measurings.

Benefits:

* Provides a fun and interactive way to monitor indoor air quality
* Helps users identify and address sources of indoor air pollution
* Enhances the aesthetic of a room with its sleek design and color-changing lights
* Reduces stress at work or helps to sleep at night.
* Promotes better indoor air quality and overall health and well-being

<br>

# Market

<br>
<div class="loader"><img src="https://media.istockphoto.com/id/1310961723/photo/tranquil-millennial-female-napping-on-couch-with-hands-behind-head.jpg?s=612x612&w=0&k=20&c=vp1wBOY6H_lD2rYlhWFStmlVTU9HvB2iz_2424JGjIM=" alt="#" /></div>

>Similar products to Kazelight include:
<br>
* <span style="color: green;">Awair:</span>
A smart air quality monitor that uses sensors to track temperature, humidity, CO2, VOCs, and dust levels. Awair also offers a companion app for tracking and analysis.
* <span style="color: green;">Foobot:</span> A smart air monitor that tracks VOCs, particulate matter, and temperature and humidity. Foobot also offers integration with smart home devices and services.
* <span style="color: green;">Dyson Pure Cool:</span> A smart air purifier and fan that uses HEPA filters to clean the air and also doubles as an air quality monitor.
<br>
<br><div class="loader"><img src="https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T1/images/S/aplus-media/vc/a6bc06fb-a35b-4df0-8ee5-ad920d2a8490.__CR117,0,300,300_PT0_SX300_V1___.jpg" alt="#" /></div>
<div class="loader"><img src="https://dyson-h.assetsadobe2.com/is/image/content/dam/dyson/for-business/business-refresh/air-treatment/cool-me/Pure-Cool-Me_PDP_module2.jpg?$responsive$&cropPathE=mobile&fit=stretch,1&fmt=pjpeg&wid=640" alt="#" /></div>
<br>
<br>The market for indoor air quality monitoring products is growing, driven by increasing awareness of the negative health impacts of poor indoor air quality. According to a report by Allied Market Research, the global indoor air quality monitoring market is expected to grow at a compound annual growth rate (CAGR) of 11.3% from 2020 to 2027.
<br>
<br>Kazelight has a unique selling proposition (USP) in its combination of air quality monitoring and decorative table lamp functions. This combined functionality sets it apart from other, more basic air quality monitors, and appeals to consumers who are looking for both practical and aesthetic solutions for their indoor air quality needs.
<br>
<br>In terms of competition, Kazelight will face competition from established players in the indoor air quality monitoring market, such as Awair and Foobot. However, Kazelight's focus on design and style may give it an edge over more utilitarian-looking products.
<br>

# Design and Prototype
Materials and technology used:
* Arduino Board
* Air Quality Sensor
* Temperature and Humidity sensor
* RGB light source
* LCD Screen
* A lamp diffuser

<br>
<br>Steps to build the design:

> 1- Connect the sensors to the Arduino board according to the respective data sheets.
> <br>2- Write a code for the Arduino that reads the sensor data and displays it on the screen and the light.
> <br>3- Design and produce an enclosure solution for the base and lamp diffuser.
> <br>4- Assemble the project
> <br>5- Test and calibrate the sensors inside the 3D printed lamp
> <br>6- Program the moodlight pattern: blue light when the quality is good, yellow when temperature is high and green whe humidity is high.
> <br>7- Test and debug the project.
> <br>8- Finalize and assemble the final prototype.

## Circuit diagram
Click in the picture for more detail

<a href="https://ibb.co/ZGFpH8L"><img src="https://i.ibb.co/17Ptsqv/2023-04-04-083204.png" alt="2023-04-04-083204" border="0"></a><br>

## Coding
```C++
#include <Adafruit_NeoPixel.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <DHT.h>
#include <SoftwareSerial.h>

#define DHTPIN 2
#define DHTTYPE DHT11

DHT dht(DHTPIN, DHTTYPE);

#define LED_PIN    6
#define LED_COUNT  256

Adafruit_NeoPixel strip(LED_COUNT, LED_PIN, NEO_GRB + NEO_KHZ800);

#define PM25_RX_PIN 10
#define PM25_TX_PIN 11
// define colors
const uint32_t GREEN = strip.Color(0, 255, 0);
const uint32_t BLUE = strip.Color(0, 0, 255);
const uint32_t YELLOW = strip.Color(255, 255, 0);
const uint32_t RED = strip.Color(255, 0, 0);
const uint32_t CYAN = strip.Color(0, 255, 255);
const uint32_t PURPLE = strip.Color(255, 0, 255);
const uint32_t WHITE = strip.Color(255, 255, 255);

SoftwareSerial pm25(PM25_RX_PIN, PM25_TX_PIN);

LiquidCrystal_I2C lcd(0x3F, 16, 2); // Set the LCD I2C address and size

void setup() {
  Serial.begin(9600);
  pm25.begin(9600);
  dht.begin();
  strip.begin();
  strip.show();
  lcd.init(); // Initialize the LCD screen
  lcd.backlight(); // Turn on the backlight
}

void loop() {
  float temperature = dht.readTemperature();
  float humidity = dht.readHumidity();
  static float hue = 0; // Initialize the hue variable
  if (isnan(temperature) || isnan(humidity)) {
    Serial.println("Failed to read DHT11 sensor!");
    return;
  }
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.print("C, Humidity: ");
  Serial.print(humidity);
  Serial.println("%");

  pm25.listen();
  delay(1000);
  if (pm25.available()) {
    int pm25value = pm25.read();
    pm25value += 2.5* pm25value;
    Serial.print("PM2.5: ");
    Serial.println(pm25value);
    int air_quality = map(pm25value, 0, 500, 0, 255);
    int temperature_color = map(temperature, 0, 40, 0, 255);
    int humidity_color = map(humidity, 0, 100, 0, 255);
    updateLCD(temperature, humidity, air_quality);
    animateStrip(temperature_color, humidity_color, air_quality);
    return;
  }
}

void animateStrip(int temperature, int humidity, int air) {
  // calculate pulse speed based on temperature and humidity
  int pm25value = pm25.read();
  float pulse_speed = 20; // (1.0 + pm25value / (1.0 + temperature + humidity));

  // calculate color gradient based on air quality
  uint32_t color1, color2;
  if (pm25value <= 20) {
    color1 = BLUE;
    color2 = GREEN;
  } else if (pm25value <= 60) {
    color1 = GREEN;
    color2 = YELLOW;
  } else if (pm25value <= 70) {
    color1 = YELLOW;
    color2 = RED;
  }  else if (pm25value = 0) {
    color1 = WHITE;
    color2 = WHITE;
  } else {
    color1 = RED;
    color2 = PURPLE;
  }

  // animate pulse with color gradient
  for (int i = 0; i <= 255; i++) {
    float val = (exp(sin(i / pulse_speed * PI)) - 0.36787944) * 108.0;
    uint8_t r = (val / 256.0) * ((color2 >> 16) - (color1 >> 16)) + (color1 >> 16);
    uint8_t g = (val / 256.0) * (((color2 >> 8) & 0xFF) - ((color1 >> 8) & 0xFF)) + ((color1 >> 8) & 0xFF);
    uint8_t b = (val / 256.0) * ((color2 & 0xFF) - (color1 & 0xFF)) + (color1 & 0xFF);

    for (int j = 0; j < LED_COUNT; j++) {
      strip.setPixelColor(j, strip.Color(r, g, b));
    }
    strip.show();
    delay(10);
  }
}
void updateLCD(float temperature, float humidity, int air_quality) {
int pm25value = pm25.read();
delay(250);
  lcd.setCursor(0, 0); // Set the cursor to the first column of the first row
  lcd.print("Temp: ");
  lcd.print(temperature);
  lcd.print("C");
  lcd.setCursor(0, 1); // Set the cursor to the first column of the second row
  lcd.print("Humidity: ");
  lcd.print(humidity);
  lcd.print("%");
  delay(500);
  lcd.clear(); // Clear the screen
  lcd.setCursor(0, 0); // Set the cursor to the first column of the first row
  lcd.print("Air quality: ");
  lcd.setCursor(0, 1); // Set the cursor to the first column of the second row
  if (pm25value <= 50) {
    lcd.print("AQI ");
    lcd.print(pm25value);
  } else if (pm25value <= 20) {
    lcd.print("very good ");
    lcd.print(pm25value);
  } else if (pm25value <= 50) {
    lcd.print("good ");
    lcd.print(pm25value);
  } else if (pm25value <= 100) {
    lcd.print("poor ");
    lcd.print(pm25value);
  } else if (pm25value = 0) {
    lcd.print("reading ");
    lcd.print(pm25value);
  } else {
    lcd.print("hazardous ");
    lcd.print(pm25value);
  }
}
```

<img src="https://i.ibb.co/qY1C3CH/IMG-20230328-013626.jpg" alt="IMG-20230328-013626" border="0" />
<br><br>

## Material and how to make it
We used laser cutting for engraving and cutting acrylic panels for the lamp, and cardboard for the box that contains the Arduino board. 

<br><img src="https://i.ibb.co/3TQ3csQ/VID-20230331-235215-Adobe-Express.gif" alt="VID-20230331-235215-Adobe-Express" border="0" /></a>

<br><img src="https://i.ibb.co/Vgq74BS/process.jpg" alt="process" border="0">

<img src="https://i.ibb.co/41Z6jbv/testing.jpg" alt="testing" border="0">

## Testing the prototype
Click to see the videos<br>
<a href="https://ibb.co/mBFhf7t"><img src="https://i.ibb.co/1nJRFxK/t1.gif" alt="t1" border="0"></a>
<a href="https://ibb.co/PGjthQj"><img src="https://i.ibb.co/9HgGTtg/t2.gif" alt="t2" border="0"></a>
<a href="https://ibb.co/gPNxKfm"><img src="https://i.ibb.co/mXk3W2b/VID-20230404-063743-1.gif" alt="VID-20230404-063743-1" border="0"></a>
<br><br>

# Key Technology

> Main Components
- Arduino Uno Microcontroller
- PM2.5 Air sensor

?>The PM2.5 air sensor is a device that measures the concentration of fine particulate matter (PM) in the air with a diameter of 2.5 micrometers or less. These small particles can be harmful to human health if inhaled, as they can penetrate deep into the lungs and even into the bloodstream. The PM2.5 air sensor works by using a laser to detect the number of particles in a given volume of air and converting this data into a concentration measurement. It is commonly used in air quality monitoring systems to track pollution levels and inform decisions related to public health and safety.
- WS2812B 16x16 RGB LED Matrix

?>The WS2812B LED is a type of addressable RGB LED that is commonly used in electronics projects. Each LED contains a tiny microcontroller that allows it to be controlled individually or as part of a larger array using a single data pin. This means that you can program the color and brightness of each LED in the array separately, creating complex lighting effects and animations. The WS2812B LED is available in a variety of package sizes and can be easily integrated with popular microcontrollers such as the Arduino. It requires a 5V power supply and can draw up to 60mA per LED at full brightness.

- DHT11 Temperature and Humidity Sensor
- Standard size I2C LCD Screen


## Future versions
* Can be used as a table lamp with adjustable brightness and color options (future versions)
* Compact and portable design, perfect for use in a bedroom or office space (future versions)
* Can connect to a smartphone app for real-time air quality updates and tracking (future versions)
* The case can be designed to protect the internal components from the environment, a gas sensor can be incorporated along with a buzzer if correctly isolated to avoid accidents.
* This prototype encountered many challenges related to reading the values from the sensors fast enough to give real-time feedback, it is expected to be solved in the future versions.
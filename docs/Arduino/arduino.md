# Project containing LED, motor and screen

List of Components:
- An Arduino Uno board
- A breadboard
- One red LED
- One DC motor
- 16x2 LCD Screen
- Jumper wires
- A 10k potentiometer (optional)

<br><img src="https://i.ibb.co/9V0hcJq/2023-03-31-154228.png" alt="2023-03-31-154228" border="0" />
<br>

>We used the following code:
```C++
#include <LiquidCrystal.h>

// set up the screen
LiquidCrystal lcd(7, 6, 5, 4, 3, 2);

void setup() {
  // set the LED pin as an output
  pinMode(13, OUTPUT);
  // set the motor pin as an output
  pinMode(9, OUTPUT);
  // initialize the screen
  lcd.begin(16, 2);
  // print a message on the screen
  lcd.print("Hello, world!");
}

void loop() {
  // turn on the LED for one second
  digitalWrite(13, HIGH);
  delay(1000);
  // turn off the LED for one second
  digitalWrite(13, LOW);
  delay(1000);
  // turn on the motor for one second
  digitalWrite(9, HIGH);
  delay(1000);
  // turn off the motor for one second
  digitalWrite(9, LOW);
  delay(1000);
}
```
<div>
  <img src="https://i.ibb.co/QH71Lfw/VID-20230401-002410-Adobe-Express.gif" alt="VID-20230401-002410-Adobe-Express" border="0" />
  <img src="https://i.ibb.co/n0Pm5BR/VID-20230401-002816-Adobe-Express.gif" alt="VID-20230401-002816-Adobe-Express" border="0" />
<div>
<br><br>

# Environmental monitoring project

List of Components:
- An Arduino Uno board
- A breadboard
- One switch
- Temperature and humidity sensor (DHT11)
- 16x2 LCD Screen
- Jumper wires
- A 10k potentiometer (optional)

<br><img src="https://i.ibb.co/WVDZbhf/2023-03-31-162535.png" alt="2023-03-31-162535" border="0" />
<br>

We used the following code:
```C++
#include <LiquidCrystal.h>    // include the library for the LCD screen
#include <DHT.h>              // include the library for the temperature and humidity sensor

#define PIN_LED 6             // define the pin for the RGB matrix
#define PIN_DHT 7             // define the pin for the temperature and humidity sensor
#define DHT_TYPE DHT11        // define the sensor type

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);    // initialize the LCD screen
DHT dht(PIN_DHT, DHT_TYPE);               // initialize the temperature and humidity sensor

void setup() {
  lcd.begin(16, 2);                      // initialize the LCD screen
  dht.begin();                           // initialize the temperature and humidity sensor
}
void loop() {
  // Read the sensor data
  float temperature = dht.readTemperature();  // read the temperature
  float humidity = dht.readHumidity();        // read the humidity

  // Display the data on the LCD screen
  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.print(temperature);
  lcd.print(" C");

  lcd.setCursor(0, 1);
  lcd.print("Humidity: ");
  lcd.print(humidity);
  lcd.print("%");
}
```
<br>
<div>
  <img src="https://i.ibb.co/qY1C3CH/IMG-20230328-013626.jpg" alt="IMG-20230328-013626" border="0" />
  <img src="https://i.ibb.co/wYkJqkt/VID-20230328-013652-Adobe-Express.gif" alt="VID-20230328-013652-Adobe-Express" border="0" />
<div>
<br><br>
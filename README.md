# NIVEL-DE-AGUA-CON-LCD

# Practica ESP32 con HC-SR04, RELAY y LCD
Este repositorio muestra como podemos programar una ESP32 con el sensor HC-SR04 y al mismo tiempo una pantalla LCD que nos muestre la información recibida por este y de igual manera en los **RELAYS**, indicandonos en este caso el nivel de agua de un recipiente en 4 niveles.

## Introducción

### Descripción

La ```ESP32``` la utilizamos en un entorno de adquisición de datos, en esta práctica ocuparemos el sensor (```HC-SR04```) para adquirir los datos de distancia , de un la proximidad del agua en un recipiente para determinar los niveles en los RELAYS y una pantalla LCD para poder visualizar los datos .  Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/).


## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- Relay
- Sensor HC-SR04
- Pantalla LCD 16x2 ILC



## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente programación:

```
// defines pins numbers
const int trigPin = 4;
const int echoPin = 15;
const int led1 = 2;
const int led2 = 5;
const int led3 = 16;
const int led4 = 17;

#include <LiquidCrystal_I2C.h> //Libreria de LCD
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

// defines variables
long duration;
int distance;
int safetyDistance;
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(led1, OUTPUT);
pinMode(led2, OUTPUT);
pinMode(led3, OUTPUT);
pinMode(led4, OUTPUT);
Serial.begin(9600); // Starts the serial communication
lcd.init();
lcd.backlight();
}


void loop() {
// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);

// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);

// Calculating the distance
distance= duration*0.034/2;

safetyDistance = distance;
if (safetyDistance>=2 && safetyDistance<=10)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
lcd.clear();  
lcd.setCursor(0, 0);
lcd.print("NIVEL DE TANQUE ");
lcd.setCursor(6, 1);
lcd.print(" 90% ");
delay(2000);
}
else if(safetyDistance>=11 && safetyDistance<=20) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  lcd.clear();
   lcd.setCursor(0, 0);
 lcd.print("NIVEL DE TANQUE ");
 lcd.setCursor(6, 1);
 lcd.print(" 75% ");
  delay(2000);
}
else if(safetyDistance>=21 && safetyDistance<=30) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, LOW);
  lcd.clear(); 
  lcd.setCursor(0, 0);
lcd.print("NIVEL DE TANQUE ");
lcd.setCursor(6, 1);
lcd.print(" 50% ");
delay(2000);
}
else if(safetyDistance>=31 && safetyDistance<=40) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
  lcd.clear(); 
  lcd.setCursor(0, 0);
lcd.print("NIVEL DE TANQUE ");
lcd.setCursor(6, 1);
lcd.print(" 25% ");
delay(2000);
}
else
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  lcd.clear(); 
  lcd.setCursor(0, 0);
lcd.print("NIVEL DE TANQUE ");
lcd.setCursor(6, 1);
lcd.print(" 0% ");
delay(2000);
}

// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println(distance);
delay (2000);
}

```
2. Instalar las librerías:
- **LiquidCrystal I2C**

![](https://github.com/Ricardoramosdelapaz/NIVEL-DE-AGUA-CON-LCD/blob/main/LIBN.PNG?raw=true).

3. Hacer la conexion de **DHT2** con el sensor HC-SR04**, junto con la pantalla LCD y los 4 relays como se muestra en la siguiente imagen.

![](https://github.com/Ricardoramosdelapaz/NIVEL-DE-AGUA-CON-LCD/blob/main/CONN.PNG?raw=true).

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
4. colocar la distancia dando click* al sensor ultrasonico **HC-SR04** (simulando el nivel de agua).

## Resultados

Al iniciar la simulacion, verás los valores dentro del monitor serial y la pantalla LCD y los leds de los relays como se muestra en la siguente imagen.

![](https://github.com/Ricardoramosdelapaz/NIVEL-DE-AGUA-CON-LCD/blob/main/RESN1.PNG?raw=true).
![](https://github.com/Ricardoramosdelapaz/NIVEL-DE-AGUA-CON-LCD/blob/main/RESN2.PNG?raw=true).
![](https://github.com/Ricardoramosdelapaz/NIVEL-DE-AGUA-CON-LCD/blob/main/RESN3.PNG?raw=true).
![](https://github.com/Ricardoramosdelapaz/NIVEL-DE-AGUA-CON-LCD/blob/main/RES%20N4.PNG?raw=true).



# Créditos

Desarrollado por Ing. Ricardo Ramos De la paz

- [GitHub](https://github.com/Ricardoramosdelapaz)

# Practica-ULTRASONICO-con-LCD
## Descripción
En esta agregaremos una pantalla ```LCD 16x2 I2C``` que hará que visualcemos los valores datos que queramos tambien agregaremos un ```ultrasonico``` el cual lo utilizaremos para dar lecturas de una distacia, utilizando el simulado de la ESP32 de WOKWI
## Material
- Tarjeta ```ESP32```
- Pantalla ```LCD 16x2 I2C```
- El sensor ```HC-SR04 ULTRASONIC DISTANCE SENSOR```
- La libreria ```LiquidCrystal I2C```
## Instrucciones
1. Abrir WOKWI en el navegar y escogemos el simulador ESP32
![](https://github.com/vicentealexhm-VAHM/Practica-DHT11/blob/main/1.png?raw=true)
2. Bajar hasta ``Starter Templates`` y elegir la ``ESP32``
![](https://github.com/vicentealexhm-VAHM/Practica-DHT11/blob/main/2.png?raw=true)
3. Una vez adentro nos vamos a la pestaña que dice ``Library Manager`` y hay buscamos la libreria antes mencionada presionando en el circulo con el simbolo de mas
![]()
4. Una vez agregada regresamos a la pestaña de sketch donde agregaremos y conectaremos el ultrasonico y la lcd a la tarjeta y para agregarlo hacemos click en el circulo azul con el simbolo de mas y lo buscamos como ``HC-SR04 Ultrasonic Distance Sensor`` y ``lcd 16x2(l2c)``
![]()
5. Una vez que lo agregamo realizamos la conexion haciendo click sobre los pines o sobre los puntos amarrillos y lo llebamos a donde lo deceamos conectar
![]()
6. En el sketch colocamos el siguiente codigo:

```
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();

}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms

  lcd.clear();
  lcd.setCursor(3, 0);
  lcd.print("Bienvenidos");
  lcd.setCursor(4,1);
  lcd.print("Modulo 5");
  delay(2000);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Vicente H.");
  lcd.setCursor(0,1);
  lcd.print("Ing. Mecanica");
  delay(2000);

  lcd.clear();
  lcd.setCursor(1, 0);
  lcd.print("  Distancia: ");
  lcd.setCursor(5, 1);
  lcd.print(d);
  lcd.print("cm");
  delay(2000);
}
```
7. Ya que lo tengamos damos click al boton de play para que se inicie el simulador y se podra visualizar las lecturas del ultrsonico en la pantalla LCD.
![]()

## Resultados
Como resultado aprendimos a como visualizar los datos en una pantalla y con el codigo podemos escoger lo que queremos que aparezca en la pantalla
## Créditos
Desarrollado por Vicente Alexander Hernandez Maldonado

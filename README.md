# Practica-ULTRASONICO-con-LCD
## Descripción
En esta agregaremos una pantalla ```LCD 16x2 I2C``` que hará que visualcemos los valores datos que queramos tambien agregaremos un ```ultrasonico``` el cual lo utilizaremos para dar lecturas de una distacia. Utilisando el simulado de la ESP32 de WOKWI
## Material
- Tarjeta ```ESP32```
- Pantalla ```LCD 16x2 I2C```
- El sensor ```HC-SR04 ULTRASONIC DISTANCE SENSOR```
- Las librerias ```DHT sensor library for ESPx``` y ```LiquidCrystal I2C```
## Instrucciones
1. Abrir el simulador WOKWI en el navegador ![](https://wokwi.com/projects/new/esp32)

![](https://github.com/EfrenQA/Reporte-1/blob/main/wokwi.png?raw=true)

3. Elegir la tarjeta ```ESP32```

 ![](https://github.com/EfrenQA/Reporte-1/blob/main/ESP32.png?raw=true)

4. Selección del sketch

![](https://github.com/EfrenQA/Reporte-1/blob/main/ESP32-2.png?raw=true)

5. Al seleccionar el skecth se mostrara una interfas como se muestra en la imagen

![](https://github.com/EfrenQA/Reporte-1/blob/main/INTERFAS.png?raw=true)

6. Se hará la selección de la libreria ```LCD 16x2 I2C``` para el LCD, para esto se tiene que dirigir Library Manager

![](https://github.com/EfrenQA/Reporte-1/blob/main/AGREGAR%20LIBRERIA.png?raw=true)

7. Una ves en la pestaña de librerias, se tiene que clickear sobre el botón de "+", seguido de esto se abrira un cuadro de busqueda donde se buscara la libreria "LiquidCrystal I2C"

![](https://github.com/EfrenQA/REPORTE-2/blob/main/libreria%20liquid%20crystal.png?raw=true)

8. Para colocar el LCD y el ultrasonico en el espacio de simulación se tiene que clickear en el botón de "+" que esta en el cuadro de simuación.

![](https://github.com/EfrenQA/Reporte-1/blob/main/AGREGAR%20COMPONENTES.png?raw=true)

9. Para la selección del ultrasonico y del LCD, podemos escribir su nombre en la barra de buscador o desplazarnos en las opciones.

![](https://github.com/EfrenQA/Reporte-3/blob/main/selecci%C3%B3n%20de%20ultrasonico%20.png?raw=true)
![](https://github.com/EfrenQA/REPORTE-2/blob/main/sleccion%20de%20lcd.png?raw=true)

10. Una vez que se tengan los tres componentes en el cuadro de simulación, se procede a la conección entre la tarjeta y los dos componentes de la siguiente forma:
- PIN GND del ultrasonico al PIN GND de la tarjeta.
- PIN VCC del ultrasonico al PIN VCC de la tarjeta.
- PIN TRIG del ultrasonico al PIN 4 de la tarjeta.
- PIN ECHO del ultrasonico al PIN 15 de la tarjeta.

- PIN GND del LCD al PIN GND de la tarjeta.
- PIN VCC del LCD al PIN VCC de la tarjeta.
- PIN SDA del LCD al PIN 21 de la tarjeta.
- PIN SCL del LCD al PIN 22 de la tarjeta.


![](https://github.com/EfrenQA/Reporte-3/blob/main/layout3.png?raw=true)
10. En el lado de "SKETCH" se debe colocar el siguiente código:
```
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor

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
      lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("BIENVENIDOS");
  lcd.setCursor(0, 1);
  lcd.print("MODULO 5");

delay(1500);
 lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("EFREN QUIROZ");
  lcd.setCursor(0, 1);
  lcd.print("ING.INDUSTRIAL");
 
delay(1500);
lcd.clear();
lcd.setCursor(0, 1);
  lcd.print("Distancia: ");
  lcd.print(d);      //Enviamos serialmente el valor de la distancia
  lcd.print("cm");
  delay(1000);          //Hacemos una pausa de 100ms
}

```
11. como último paso se inicia el simulador con el botón de "play" y se podra visualizar las lecturas del ultrsonico.

## Instrucciones de operación
1. Iniciar simulación con el botón de "PLAY"
2. Visualizar los datos que se mostrarán en LCD
3. Descargar valores
![](https://github.com/EfrenQA/Reporte-3/blob/main/simulaci%C3%B3n%203.png?raw=true)
## Resultados
Al finalizar cada paso se podrá obtener datos desde la simulación del LCD
![](https://github.com/EfrenQA/Reporte-3/blob/main/simulaci%C3%B3n%203.png?raw=true)
## Créditos
Autor Ing. Efren David Quiroz Ayala 

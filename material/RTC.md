## Módulo con RTC 1302

Un RTC es un Reloj de Tiempo Real, es decir un reloj capaz de medir el paso del tiempo, normalmente dotado de una pila para que no se pierda la fecha y que se puede comunicar con Arduino

![](./images/RTC_1302_bb.png)

La [librería DS1302](http://playground.arduino.cc/uploads/Main/DS1302RTC.zip) :

1. Real Time Clock read/write (8 bytes)
2. Battery backed RAM read/write (31 bytes)
3. Power save mode manipulation (start/stop clock)
4. Trickle charger setup
5. Burst mode read/write
6. 24 hour format only (12 hour format is function Time library)

Whether used with the DS1302, the user is responsible for ensuring reads and writes do not exceed the device's address space (0x80-0x90 for DS1302 clock data and 0xC0-0xFC RAM data); no bounds checking is done by this library.

El DS1302 usa un 3-wire interface (The "Chip Enable" pin was called "/Reset):

* bidirectional data.
* clock
* chip select

No es I2C, ni OneWire, ni SPI. 



## Montaje

![montaje](./images/RTC_ds1302_LCDMega_bb.png)

![Montaje visual](./images/MontajeVisual.jpg)

[Más detalles](http://playground.arduino.cc/Main/DS1302RTC)

[Otro tutorial](http://www.instructables.com/id/Real-Time-Clock-DS1302/)


## Código


``` C++
// Basado en  Timur Maksiomv 2014
//
// A quick demo of how to use DS1302-library to make a quick
// clock using a DS1302 and a 16x2 LCD.
//
// I assume you know how to connect the DS1302 and LCD.
// DS1302:  CE pin    -> Arduino Digital 27
//          I/O pin   -> Arduino Digital 29
//          SCLK pin  -> Arduino Digital 31
//          VCC pin   -> Arduino Digital 33
//          GND pin   -> Arduino Digital 35
//
// LCD I2C: 
//          SDA       -> Arduino Digital 20
//          SCL       -> Arduino Digital 21
//          GND       -> ND
//          Vcc       -> 5V

// Includes del LCD
#include <Wire.h> 
#include <LiquidCrystal_I2C.h>

#include <DS1302RTC.h>
#include <Time.h>

// Init the DS1302
// Set pins:  CE, IO,CLK
DS1302RTC RTC(27, 29, 31);

// Optional connection for RTC module
#define DS1302_GND_PIN 33
#define DS1302_VCC_PIN 35

// Init the LCD
LiquidCrystal_I2C lcd(0x27,16,2); 

void showMessage(String texto){
	Serial.print(texto);
	lcd.setCursor(0,0);
	lcd.print(texto);
}


void setup()
{
    lcd.init(); 
    lcd.backlight();

	// Activate RTC module
	digitalWrite(DS1302_GND_PIN, LOW);
	pinMode(DS1302_GND_PIN, OUTPUT);

	digitalWrite(DS1302_VCC_PIN, HIGH);
	pinMode(DS1302_VCC_PIN, OUTPUT);

	showMessage("RTC activated");

	delay(500);

	// Check clock oscillation  
	lcd.clear();
	if (RTC.haltRTC())
	   showMessage("Clock stopped!");
	else
	   showMessage("Clock working.");

	// Check write-protection
	if (RTC.writeEN())
		showMessage("Write allowed.");
	else
		showMessage("Write protected.");

	delay ( 2000 );

	// Setup Time library  
	showMessage("RTC Sync");
	setSyncProvider(RTC.get); // the function to get the time from the RTC
	if(timeStatus() == timeSet)
		showMessage(" Ok!");
	else
		showMessage(" FAIL!");

	delay ( 2000 );

	lcd.clear();
}

void loop()
{

	// Display time centered on the upper line
	lcd.setCursor(3, 0);
	print2digits(hour());
	lcd.print("  ");
	print2digits(minute());
	lcd.print("  ");
	print2digits(second());

	// Display abbreviated Day-of-Week in the lower left corner
	lcd.setCursor(0, 1);
	lcd.print(dayShortStr(weekday()));

	// Display date in the lower right corner
	lcd.setCursor(5, 1);
	lcd.print(" ");
	print2digits(day());
	lcd.print("/");
	print2digits(month());
	lcd.print("/");
	lcd.print(year());

	// Warning!
	if(timeStatus() != timeSet) {
	lcd.setCursor(0, 1);
	lcd.print(F("RTC ERROR: SYNC!"));
	}

	delay ( 1000 ); // Wait approx 1 sec
}

void print2digits(int number) {
	// Output leading zero
	if (number >= 0 && number < 10) {
	lcd.write('0');
	}
	lcd.print(number);
}
```

Uniendo los ejemplos de RTC, keypad y lcd podemos hacer un reloj despertador co alarma como el de este proyecto

[Reloj despertador con alarma](https://www.hackster.io/SurtrTech/simple-alarm-clock-with-ds1302-rtc-a92d7b)

![Montaje Reloj despertador con alarma](https://hackster.imgix.net/uploads/attachments/662150/schematic_378LzRlzTi.png)
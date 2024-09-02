# emrtex-Iot
emerex internship related all document
/*To Interface Potentiometer - POT [Variable Resistance] to Arduino UNO, Read the Analog values & Print it on CLCD and Test ADC */

// My Comment
/*Comment said by Mam*/


/* To use I2C/TWI[Two Wired Interface] Protocol and LCD Library, including 2 Libraries */
/* I2C Library */
#include <Wire.h>
/* LCD Library with I2C */
#include <LiquidCrystal_I2C.h>    //This is not In-Built, we have to Install; Tools -> Manage Libraries -> Search & Install LiquidCrystal_I2C version 1.1.2

/* Creating the Object of LCD with I2C address of 0x27 (default), 2 Lines Display with 16 Characters each */
LiquidCrystal_I2C lcd(0x27, 16, 2);               //SYNTAX : LiquidCrystal_I2C object_name (address,column,rows); {0x27 is fixed for this 'lcd hd44780 i2c'}

void setup() 
{
  // put your setup code here, to run once:
  /* Initializing the LCD */      //SYNTAX : object_name.function();
  lcd.init();
  /* Turning on the BackLight */
  lcd.backlight();      //Tried running Program without this background function; Executed Normally in Simulation
  /* Clearing the LCD Screen (To erase all the old contents if present) */
  lcd.clear();
  /* To set Cursor to the First Position */
  lcd.home();

  lcd.setCursor(0,0);     //SYNTAX : object_name.setCursor(column, row); This sets the Position to 1st Column and 1st Row {Indexing from 0}
  lcd.print("ADC TEST");
}

void loop()
{
  String ADC_VAL;                       //We have to take DataType as a STRING, since LCD only supports ASCII Characters

  /*To Read Values from POT at A0 */
  ADC_VAL = String(analogRead(A0));     //As this returns an Integer & ADC_VAL is a String Type, TYPE CASTING is Done here

  lcd.setCursor(0,1);                   //This sets the Position to 1st Column and 2nd Row {Indexing from 0} since 1st Line contains String "ADC TEST"
  lcd.print(ADC_VAL); 

  // We have to Refresh the Previous Value to see new value; Hence Clear function is used repeatedly also to take multiple inputs
   delay(500);
   lcd.clear();
}

// Refer 1st Program (Blinking the LCD) for the Steps of Exporting HEX File and to Run [Use Potentiometers(1st One) in Module -> Spare Parts -> Output]

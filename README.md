/* Arduino Kill/Death/Killstreak Counter
  By ARDUINO TUTORIALS (youtube)
  https://youtu.be/F7HxgVo9y44
  
 Wiring
 * 3 buttons attached to digital pins 0, 1 and 13
 * LCD Screen attached to pins 2,3,4,5,11,12
 * 3 LEDs (green pin 6,red pin 9,ultrabright pin 10)
 * Buzzer attached to pin 8
 
Description
 * 3 buttons attached to a breadboard. When you kill press the 1st button
 * When you die press the 2nd button 
 * When you make a killstreak of more than 10 press the 3rd
 * 
 * An ongoing total of these stats will appear both on the liquidCrystal display and serial monitor
 * Different coloured LEDs will light up when you press these buttons
 
This code is open source and is freely available for others to use

  */
#include <LiquidCrystal.h>
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

//storing the digitalread value variables
int kill;
int death;
int killStreak;

//the variable which will increase as the button is pressed
int killCounter = 0;
int deathCounter = 0;
int killStreakCounter = 0;

//the pins the buttons are attached to
const int killButton = 0;
const int deathButton = 1;
const int killStreakButton = 2;

//the pins the LEDs are attached to
const int killLed = 6;
const int deathLed = 9;
const int killStreakLed = 10;

void setup(){
 
  
  lcd.begin(20,4);
  pinMode(killButton, INPUT);
  pinMode(deathButton, INPUT);
  pinMode(killStreakButton, INPUT);
  pinMode(killLed, OUTPUT);
  pinMode(deathLed, OUTPUT);
  pinMode(killStreakLed, OUTPUT);
  Serial.begin(9600);
}
void loop(){
kill = digitalRead(killButton);
if (kill == HIGH){
  killCounter = killCounter + 1;
  digitalWrite(killLed, HIGH);
  tone(8, 440, 200);
  delay(200);

}
death = digitalRead(deathButton);
if (death == HIGH){
  deathCounter = deathCounter + 1;
  digitalWrite(deathLed, HIGH);
  tone(8, 494, 500);
  delay(500);

}
killStreak = digitalRead(killStreakButton);
if (killStreak == HIGH){
  killStreakCounter = killStreakCounter + 1;
  digitalWrite(killStreakLed, HIGH);
tone(8, 523, 300);
  delay(300);
}
lcd.setCursor(0,0);
lcd.print("Kill/Death counter");
lcd.setCursor(0,1);
lcd.print("Kills: "+killCounter);
lcd.setCursor(0,2);
lcd.print("Deaths: "+deathCounter);
lcd.setCursor(0,3);
lcd.print("Kill Streaks: "+killStreakCounter);
Serial.println("Kill/Death counter");
Serial.println("Kills: "+killCounter);
Serial.println("Deaths: "+deathCounter);
Serial.println("Killstreaks: "+killStreakCounter);
delay(1000);
}

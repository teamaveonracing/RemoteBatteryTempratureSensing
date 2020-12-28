# RemoteBatteryTempratureSensing
<h2 >This projects shows how we automated to get messages of our E-ATV's battery's temperature remotely to our phones, while the ATV is on track !</p>
<h3 allign="right">The project's construction requirments are:</h3>
1-Arduino board and its accessories</p>
2-Temprature sensor (Thermistor)</p>
3-GSM module</p>
<h3 > The program is as follows (C++/Arduino) :</p>
<allign="center">#include <SoftwareSerial.h></p>
SoftwareSerial SIM900A(10,11); // RX | TX</p>
// Connect the SIM900A TX to Arduino pin 2 RX. </p>
// Connect the SIM900A RX to Arduino pin 3 TX. </p>
int ThermistorPin = 0;   // analog pin 0 for taking input from thermistor to Arduino board</p>
int Vo;                            // voltage between thermistor and know resistor</p>
float R1 = 10000;</p>
float logR2, R2, T;</p>
float A = 1.009249522e-03, B = 2.378405444e-04, C = 2.019202697e-07;</p>
</p>
void setup() {</p>
  SIM900A.begin(9600);   // Setting the baud rate of GSM Module  </p>
  Serial.begin(9600);    // Setting the baud rate of Serial Monitor (Arduino)</p>
  Serial.println ("SIM900A Ready");</p>
  delay(1000);</p>
}</p>
</p>
void Sendmessage(){</p>
  // defining function that sends temperature as message</p>
  mySerial.println("AT+CMGF=1");    //Sets the GSM Module in Text Mode</p>
  delay(1000);  </p>
  mySerial.println("AT+CMGS=\"+911234567890\"\r"); // Setting the mobile no. to which temperature will be sent</p>
  delay(1000);</p>
  mySerial.println("Temp (degree_celcius) = ")</p>
  delay(100)</p>
  mySerial.println(c);// The temp to be sent</p>
  delay(100);</p>
   mySerial.println((char)26);// ASCII code of CTRL+Z</p>
  delay(1000);</p>
  mySerial.println("\n\n\n")    // Next message showing temp will be easily distinguishable </p>
}</p>
</p>
void loop() {</p>
  Vo = analogRead(ThermistorPin);</p>
  R2 = R1 * (1023.0 / (float)Vo - 1.0);</p>
  logR2 = log(R2);</p>
  T = (1.0 / (A + B*logR2 + C*logR2*logR2*logR2));</p>
  T = T - 273.15;                     // add T = (T * 9.0)/ 5.0 + 32.0; in next line to make temp in fahrenheitv</p>
  Sendmessage()</p>
  delay(3000) // after every 3 seconds the mobile no. entered above will recieve a new message showing the current temperature</p>
}</p>
<h2> The circuit is as follows : </p>
<img src="circuit.png" width="641" height="456"/>
          

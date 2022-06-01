# Codi 1ra part

#include <Arduino.h>
#include <WiFi.h>
#include <WebServer.h>
// SSID & Password
const char* ssid = "MOVISTAR_721A"; // Enter your SSID here
const char* password = "B8CD5566CCD48A4BCD74"; //Enter your Password here
WebServer server(80); // Object of WebServer(HTTP port, 80 is defult)

void handle_root(void);

void setup() {
Serial.begin(115200);
Serial.println("Try Connecting to ");
Serial.println(ssid);
// Connect to your wi-fi modem
WiFi.begin(ssid, password);
// Check wi-fi is connected to wi-fi network
while (WiFi.status() != WL_CONNECTED) {
delay(1000);
Serial.print(".");
}
Serial.println("");
Serial.println("WiFi connected successfully");
Serial.print("Got IP: ");
Serial.println(WiFi.localIP()); //Show ESP32 IP on serial
server.on("/", handle_root);
server.begin();
Serial.println("HTTP server started");
delay(100);
}
void loop() {
server.handleClient();
}
// HTML & CSS contents which display on web server
String HTML = "<!DOCTYPE html>\
<html>\
<body>\
<h1>My Primera Pagina con ESP32 - Station Mode &#128522;</h1>\
</body>\
</html>";
// Handle root url (/)
void handle_root() {
server.send(200, "text/html", HTML);
}

# Funcionament del programa

Aquest prpgrama genera una pàgina web connectant-se a una wifi la qual se li ha d'especificar.
Posteriorment el programa ens fa saber si s'ha connectat al wifi i es disposara a crear la pàgina automàticament seguint les indicacions 
del codi html inserit dins del codi cpp.

Es mostrarà per pantalla el següent:

![image](https://user-images.githubusercontent.com/101355262/171424383-72a605cc-9b35-4781-9b06-d0990c830918.png)



# Codi 2a part

#include "BluetoothSerial.h"
#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif
BluetoothSerial SerialBT;
void setup() {
Serial.begin(115200);
SerialBT.begin("ESP32test"); //Bluetooth device name
Serial.println("The device started, now you can pair it with bluetooth!");
}
void loop() {
if (Serial.available()) {
SerialBT.write(Serial.read());
}
if (SerialBT.available()) {
Serial.write(SerialBT.read());
}
delay(20);
}


# Funcionament

Aquesta pràctica consisteix a poder veure la comunicació bluetooth, entre un dispositiu bluetooth rebent missatges que rebrà, 
des d'un dispositiu mòbil, des d'on s'enviaran aquests missatges. Per això inicialment necessitem inicialitzar la nostra ESP32 
perquè aquesta sigui capaç de rebre els missatges. Caldrà executar el codi, que un cop pujat a la placa ens permetrà aparellar-la 
amb el nostre dispositiu mòbil.

Aixì sabrem si el ESP32 s'ha connectat al dispositiu mitjançant bluetooth:

![image](https://user-images.githubusercontent.com/101355262/171425761-f03d7553-2377-430c-83d9-d1f2d9ae1c36.png)





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

![image](https://user-images.githubusercontent.com/101355262/171424178-a01c9e97-9d44-4253-b365-392fa309eba7.png)


# Codi 2a part





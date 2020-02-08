# ESP8266/32 Webservers using SPIFFS
Making Webservers on ESP8266/32 is very useful where using third party servers like Blynk, Adafruit.io is overkilled and only require local webserver to connect and use basic application like making simple weather station

## Why need SPIFFS?
Including HTML/CSS/JS is a big hassle in code and ultimately lead to dead code you are working on
SPIFFS help to organise code effectively and hence placing/editing files in a root directory is easy then finding a line of code in arduino and also you cant check outside which makes a lot of hassle!

## Initial Requirements:
- [Arduino IDE](https://www.arduino.cc/en/main/software)
- ESP8266/32 based microcontrollers
- [ESP8266 sketch data upload](https://github.com/esp8266/arduino-esp8266fs-plugin)
- Updated Libraries and boards!
- Text editor of choice, I use [Atom](https://atom.io)
- Knowledge of HTML/CSS/JSS

# Making program of your choice:
You can implement whatever you want, and start from scratch like this:   
    
      #include <ESP8266mDNS.h>
      #include <ESP8266WebServer.h>
      #include <FS.h>
      #define ssid      "SSID"      // WiFi SSID
      #define password  "PASSWORD"      // WiFi password


      ESP8266WebServer server ( 80 );

      void setup() {
    
      Serial.begin ( 115200 );

      WiFi.begin ( ssid, password );
      // Wait for connection
      while ( WiFi.status() != WL_CONNECTED ) {
      delay ( 500 ); Serial.print ( "." );
      }
      // WiFi connexion is OK
      Serial.println ( "" );
      Serial.print ( "Connected to " ); Serial.println ( ssid );
      Serial.print ( "IP address: " ); Serial.println ( WiFi.localIP() );

      if (!SPIFFS.begin())
      {
        // Serious problem
       Serial.println("SPIFFS Mount failed");
       } else {
       Serial.println("SPIFFS Mount succesfull");
       }

       server.serveStatic("/", SPIFFS, "/index.html");

       server.begin();
       Serial.println ( "HTTP server started" );

       }

       void loop() {
       // put your main code here, to run repeatedly:
       server.handleClient();
       MDNS.update();
       }

### Now make HTML/CSS/JSS:
Make a *data* folder in root 

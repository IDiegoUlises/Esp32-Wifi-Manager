# Esp32-Wifi-Manager

### Codigo no probado se debe mejorar
ahi que descargar la libreria de wifi manger
```c++
#include <WiFiManager.h> 

void setup() {
    WiFi.mode(WIFI_STA); // explicitly set mode, esp defaults to STA+AP

    Serial.begin(115200);
    pinMode(LED_BUILTIN, OUTPUT);
    digitalWrite(LED_BUILTIN, HIGH);
    
    WiFiManager wiFiManager;

    // reset settings - wipe stored credentials for testing
    wiFiManager.resetSettings();

    // Automatically connect using saved credentials,
    // if connection fails, it starts an access point with the specified name ( "AutoConnectAP"),
    // if empty will auto generate SSID, if password is blank it will be anonymous AP (wiFiManager.autoConnect())
    // then goes into a blocking loop awaiting configuration and will return success result

    bool res;
    // res = wiFiManager.autoConnect(); // auto generated AP name from chipid
    // res = wiFiManager.autoConnect("AutoConnectAP"); // anonymous ap
    res = wiFiManager.autoConnect("AutoConnectAP","12345678"); // password protected ap

    if(!res) {
        Serial.println("Failed to connect!");
        // ESP.restart();
    } 
    else {
        Serial.println("Connected :)");
        // Serial.println("IP address: ");
        // Serial.println(WiFi.localIP());   
    }

}

void loop() {
    digitalWrite(LED_BUILTIN, LOW);
    delay(1000);
    digitalWrite(LED_BUILTIN, HIGH);
    delay(1000);
}
```

### Codigo 2 
```c++
#include <WiFiManager.h> 

void setup() 
{
    //El WiFi inicia en modo estacion como punto de acceso, como configuracion inicial

    //Aqui poner el codigo de la configuracion del programa
    Serial.begin(115200);
    
    //Se inicializa WiFiManager y se crea el objeto
    WiFiManager wm;

    //Solo utilizar (descomentar) cuando se necesite cambiar de conexion Wifi   
    // wm.resetSettings(); //Borra las credenciales guardadas

    //Automaticamente se conecta usando las credenciales guardadas
    //Si la conexion falla, comienza un punto de acesso con el nombre ("AutoConnectAP") o con el nombre que se asigne
    //Luego entra en un bucle de configuracion hasta devolver un resultado exitoso

    bool res;

    //Son tres opciones que se pueden elegir, en este caso se eligio la tercera
    //res = wm.autoConnect(); //Crea un punto de acceso abierto con el nombre del Chip-ID del esp32
    //res = wm.autoConnect("AutoConnectAP"); //Se le da nombre a la red WiFi pero no se necesita contraseña para conectarse, es una red abierta
    res = wm.autoConnect("AutoConnectAP","password"); //Se le asigna ssid de la red y contraseña

    if(!res) 
    {
        Serial.println("Error al conectar");
        
        //Para reinciar el Esp32, esta linea esta comentada
        //ESP.restart(); //Solo utilizar en caso las credenciales esten equivocadas
    } 
    else 
    {
        //Si llegas hasta aqui es porque la conexion Wifi es exitosa    
        Serial.println("conectado... :)");
    }

}

void loop() 
{
  //Aqui el codigo principal  
}
```

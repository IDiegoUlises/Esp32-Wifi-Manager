# Esp32 Wifi Manager

### Codigo 
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
        //ESP.restart(); //Solo utilizar en caso que las credenciales esten equivocadas
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

<img src="https://github.com/IDiegoUlises/Esp32-Wifi-Manager/blob/main/images/Modificado-WiFi.jpg" width="600" height="800" />

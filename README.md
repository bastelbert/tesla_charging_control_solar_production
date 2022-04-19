# Tesla charging control based on solar power production
Charge your Tesla at a Tesla Wall Connector Gen3 with spare solar power.

This repository contains a Node-RED flow as a template for your own charge control.
In this example, the current electricity consumption and the solar production are determined via Loxone.
The amp value is adjusted directly in the car every 10 seconds via Node-RED based on the current power consumption and the solar production. 

The flow has no claim to perfection (I am not a professional programmer). Please feel free to contribute improvements.

![image](https://user-images.githubusercontent.com/32751381/164049949-51bd12fd-5416-4d37-82dc-9d4eda0d4444.png)

Configuration guide:
- update your Tesla Model at least to 2021.36.5.5 (required for command "setChargingAmps")
- install a Node-RED instance, e.g. in Docker: https://github.com/node-red/node-red-docker
- install nodes: 
  -  https://github.com/onokje/node-red-contrib-tesla
  -  https://github.com/codmpm/node-red-contrib-loxone
- configure Tesla API (add your account and select your car)
- configure connection to Loxone Miniserver

The flow was tested on Node-RED v.2.2.2 with a Loxone Miniserver Gen1, a Tesla Wall Connector Gen3 and a Tesla Model 3.

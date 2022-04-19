# Tesla charging control based on solar power production
Charge your Tesla at a Tesla Wall Connector v3 with spare solar power.
The amp value is adjusted directly in the car every 10 seconds via Node-RED based on the current power consumption and the solar production. 

This repository contains a Node-RED flow as a template for your own charge control.
In this example, the current electricity consumption and the solar production are determined via Loxone.

Used nodes:
node-red-contrib-loxone, node-red-contrib-tesla

The flow has no claim to perfection (I am not a professional programmer). Please feel free to contribute improvements.

![image](https://user-images.githubusercontent.com/32751381/164049949-51bd12fd-5416-4d37-82dc-9d4eda0d4444.png)

# Configuration
In order to get a working configuration replace the following placeholder with correct data:

- <VEHICLE_ID> -> tesla vehicle id
- ...

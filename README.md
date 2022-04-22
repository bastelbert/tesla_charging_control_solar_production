# Tesla charging control based on solar power production
Charge your Tesla Model at a Tesla Wall Connector Gen3 (or any other wallbox) with spare solar power.

This repository contains a Node-RED flow as a template for your own charge control.
In this example, the current electricity consumption and the solar production are determined via Loxone (can be replaced with any other source).
<br>Based on the current power consumption and the solar production, the surplus solar power is determined in Node-RED every 10 seconds and the ampere value to be set is calculated from this. If the value changes, the new ampere value is set directly in the car via a message to the Tesla API.


<br>![image](https://user-images.githubusercontent.com/32751381/164721807-c8c43d53-c609-46aa-9031-90f7f4f57dac.png)

<br>Configuration guide:
- update your Tesla Model to at least 2021.36.5.5 (required for command "setChargingAmps")
- install a Node-RED instance, e.g. in Docker: https://github.com/node-red/node-red-docker
- install nodes: 
  -  https://github.com/onokje/node-red-contrib-tesla
  -  https://github.com/codmpm/node-red-contrib-loxone
  -  https://github.com/Writech/node-red-contrib-controltimer
- configure Tesla API (add your account and select your car)
- set up the connection to your Loxone Miniserver (optional - you can use your preferred data source)
- adjust the IP address in the "http request" to reach your Wallbox

<br>Fun fact:<br>
It's possible to set amp values smaller than 5, e.g. 2A will be used and shown in the Tesla App.
Just edit the function node "calculate ampvalue" to your needs. 
But please bear in mind that I cannot make any statement about the extent to which values lower than 5A can lead to problems on the car or during charging!

<br>The flow was tested on Node-RED v.2.2.2 with a Loxone Miniserver Gen1, a Tesla Wall Connector Gen3 and a Tesla Model 3.

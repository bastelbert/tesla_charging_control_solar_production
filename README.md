# Tesla charging control based on solar power production
Charge your Tesla Model at a Tesla Wall Connector Gen3 (or any other wallbox) with spare solar power.

This repository contains two Node-RED flows as templates for your own charge control.

In both flows, the current electricity consumption and the solar production are determined via Loxone (can be replaced with any other source).
<br>Based on the current power consumption and the solar production, the surplus solar power is determined in Node-RED every 10 to 15 seconds and the ampere value to be set is calculated from this. If the value changes, the new ampere value is set directly in the car via a message to the Tesla API.

<br>Description 01_automatic_flow.json:
<br>In this flow, some default values can be given and additionally customized in the dashboard via sliders to automatically start and stop loading processes.
<br>It requires a running instance of Teslamate to get data from the car: https://github.com/adriankumpf/teslamate

<img width="1406" alt="image" src="https://user-images.githubusercontent.com/32751381/172206177-2bb7ddc0-d029-4235-8e21-a974d685a3c7.png">

<br>Dashboard:
<br><img width="314" alt="image" src="https://user-images.githubusercontent.com/32751381/172207592-734682b9-eda5-4256-a8fb-5161358ec089.png">


<br>Configuration guide:
- update your Tesla Model to at least 2021.36.5.5 (required for command "setChargingAmps")
- install a Node-RED instance, e.g. in Docker: https://github.com/node-red/node-red-docker
- install nodes: 
  -  https://github.com/onokje/node-red-contrib-tesla
  -  https://github.com/codmpm/node-red-contrib-loxone
  -  https://github.com/dkern/node-red-throttle
- configure Tesla API (add your account and select your car)
- set up the connection to your Loxone Miniserver (optional - you can use your preferred data source)
- set up the MQTT connection to fetch data from Teslamate (optional - you can use your preferred data source)
- adjust the IP address in the "http request" to reach your Wallbox

<br>Default values:
- min_charge_level_16A : 10, // charge with full power (but not more than max_ampere) until battery level reaches 10% 
- min_charge_level_pv : 50, // charge mostly with solar power, but at least with min_ampere till battery level 50%
- max_charge_level : 80, // stop charge process at battery level 80%
- activate_charge_control : true, // activate/deactivate the charge controller
- allow_autocharge : false, // allow charge processes
- phases : 3, // how many phases does the wall connector have?
- min_ampere : 2, // don't charge below this
- max_ampere : 16, // don't charge above this
- buffer : 250, // value to decrease available power (watt)
- start_stop_cooldown : 5*60*1000 // start/stop requests shouldn't be sent to quickly, in this case only five minutes after the last start/stop


<br>
<br>Description 02_manual_flow.json:

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
It's possible to set amp values smaller than 5 by sending the value two times, e.g. 3A will be used and shown in the Tesla App.
Just edit the function node "calculate ampvalue" to your needs, e.g.:
<br>"if (context.ladekapa_current < 2100) { ampvalue = 3"

<br>Please bear in mind that I cannot make any statement about the extent to which values lower than 5A can lead to problems on the car or during charging!

<br>The flow was tested on Node-RED v.2.2.2 with a Loxone Miniserver Gen1, a Tesla Wall Connector Gen3 and a Tesla Model 3.

# baxi-node-red
A node red flow to communicate with Baxi thermostat Mago (BDR Thermea compatible)

# Introduction
After the implementation of the My Baxi app, the node red script I found online didn't work anymore since Baxi (aka BDR Thermea Group) moved their platform to Azure and implemented OAuth 2.0 authentication protocol. After some more searching, I discovered this repository <link>https://github.com/msvisser/remeha_home</link> for integrate the Remeha Thermostat (same BRD Thermea Group) in Home Assistant.

After reverse engineering the python code, changed all the "remeha" strings to "baxi", with some help of Postman, I was able to replicate the integration for Node-Red.

(BTW if you want to use the msvisser's HA integration for Baxi, just replace the strings in all the files, as mentioned earlier).

# How it works
### Get Token Once
the first part gets the first access token through a four step http request. The node automatically inject the request once at startup and store the tokens for later use.

<b>Notice to set your Baxi email and password (the same used to access the "My Baxi" app) in the function node called "Step 2".</b>

### Get Refresh Token every 1h
The second Part request a new access token every hour and store the received tokens in the flow.

### Get All Data From Thermostat
This part get all the possible data from the thermostat, you can see all the available information published by the thermostat in the Data Debug Node. The flow stores the climate-zone-id needed for the commands/requests to the thermostat.

### Commands
With the following commands you'll be able to controll the themostat.

<b>Manual</b> Manually change the setpoint of the thermostat indefinitely

<b>temporary-override</b> Change the setpoint of the thermostat until the next schedule occurs

<b>schedule</b> Reset to the shedule you choose (I have only one, so I set "1" to "heatingProgramId" in the function flow

<b>anti-frost</b> Turn Off the thermostat

<b>Fireplace</b> Enable/Disable the fireplace mode

![Node-Red Flow](https://github.com/alessandromatera/baxi-node-red/blob/main/baxi-node-red-flow.png)

### The Node-Red Flow
Finally here you have the flow: <link>https://github.com/alessandromatera/baxi-node-red/blob/main/baxi-node-red-flow.json</link>
Just copy and paste in your Node-Red

Enjoy!

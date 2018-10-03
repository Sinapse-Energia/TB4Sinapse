# TB4Sinapse
PoC managing Sinapse devices through ThingsBoard

# Introduction

The goal of this project is to make a proof of concept about the integration of a little part of Sinapse devices (SD) into the ThingsBoard IoT Platform. 
Basically it is needed to listen (subscribe) and process some MQTT messages published by a Sinapse Device named DDP trough a Broker and send (publish) some MQTT messages.

# Global Behaviour

A DDP will publish a message depending of the light & presence conditions of a room:

- LIGHT ON: If the DDP detects presence and the quantity of light is not enough will publish a "Light ON" message (text format) in a topic (TOPIC/EXAMPLE/MEASUREMENTS) like:

L3_DDP_COND_POC;$ID;1;$LUX_VALUE;$PRESENCE_VALUE;$TIMESTAMP; 

- LIGHT OFF: If the DDO does not detect presence or the quantity of light is enough will publish a "Light OFF" message (text format) in a topic (TOPIC/EXAMPLE/MEASUREMENTS) like:

L3_DDP_COND_POC;$ID;0;$LUX_VALUE;$PRESENCE_VALUE;$TIMESTAMP;

Where $ are variables with the next meaning:

$ID : ID of the device
$LUX_VALUE: Number identifying the quantity of light
$PRESENCE_VALUE: Boolean identifying the presence
$TIMESTAMP: Unix timestamp;

The TB Platform will receive these messages and should perform 2 actions:

- Process the message in order to save the data and create charts, tables, etc.
- Publish a MQTT message depending the value of $LUX_VALUE in a topic (TOPIC/EXAMPLE/ACT) like:

L3_DMX;$ID;$COLOR; 

Where $ID is the same of the received in the message and $COLOR can be:

NONE if $LUX_VALUE < 200
RED if 200 <= $LUX_VALUE < 300
BLUE if 300 <= $LUX_VALUE < 400
GREEN if 400 <= $LUX_VALUE
 

# Specific requirements

TBD by RAE

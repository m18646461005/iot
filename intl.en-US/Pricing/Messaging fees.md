# Messaging fees

IoT Platform charges messaging fees. The messaging fee is calculated based on the number of messages and has no minimum charge.

## Billing items

For more information about billing items, see the following table. For billable operations, see the appendix in this documentation.

|Item|Description|
|:---|:----------|
|Messaging fee \(Device\)

|Messages sent from devices by calling the Pub operation|
|Requests sent from devices by calling the RPC operation|
|RRPC responses sent from devices to the server|
|Messages received by devices by calling the Sub operation|
|Messages sent and received by devices by calling TSL model related operations|
|Messaging fee \(Server\)

|Messages sent from the server by calling the Pub and PubBroadcast operations|
|RPC responses sent from the server to devices|
|Messages sent from the server by calling the RRPC operation|
|Messages sent from the server by calling sub-device related operations|
|Messages sent from the server by calling device shadow related operations|
|Messages sent from the server by calling TSL model related operations|
|Free messages|-   Connect
-   Connect Ack
-   Disconnect
-   PingReq
-   PingResp
-   Publish ACK
-   Subscribe
-   Subscribe ACK
-   Unsubscribe
-   Unsubscribe Ack
-   Messages forwarded by the rules engine

**Note:** You can use the rules engine to forward messages for free. However, fees are charged when you transfer data to other cloud services. |

## Billing method

Tiered pricing

|Messages N \(per Month\)|Unit price \(Yuan/1,000,000 Messages\)|
|:-----------------------|:-------------------------------------|
|N ≤ 100,000,000|1.8|
|100,000,000 < N ≤ 1,000,000,000|1.4|
|1,000,000,000 < N|1|

|Messages N \(per Month\)|Unit price \(USD/1,000,000 Messages\)|
|:-----------------------|:------------------------------------|
|N ≤ 100,000,000|0.5|
|100,000,000 < N ≤ 1,000,000,000|0.4|
|1,000,000,000 < N|0.3|

Billing details

-   Fees are calculated based on the number of messages. For more information about billing items, see the preceding table.
-   The first 1 million messages are free of charge for each month. The free quota takes effect at 00:00:00 on the first day of each month. Unused quota cannot be carried over to the next month. The fees are calculated when the number of messages exceeds 1 million for each month.

How to count messages

-   If a message is less than or equal to 512 bytes in size, the message is counted as one billable message.
-   If a message is more than 512 bytes in size, the message is counted as two or more billable messages.
-   To calculate the number of billable messages, divide the message size into bytes by 512, and round the resulting value up to the nearest integer.

Billing dates

-   The messaging fee is calculated and charged on a daily basis.
-   Fees are rounded up to the nearest cent.

**Note:** This document is for reference only. Refer to your bill for accurate information.

## Appendix: Billable operations

|MQTT Publish|IOT\_CMP\_OTA\_Start|
|IOT\_CMP\_OTA\_Get\_Config|
|IOT\_CMP\_OTA\_Request\_Image|
|IOT\_CMP\_Send|
|IOT\_MQTT\_Publish|
|IOT\_OTA\_ReportVersion|
|IOT\_OTA\_RequestImage|
|IOT\_OTA\_ReportProgress|
|IOT\_OTA\_GetConfig|
|IOT\_Shadow\_Construct|
|IOT\_Shadow\_RegisterAttribute|
|IOT\_Shadow\_Push|
|IOT\_Shadow\_Push\_Async|
|IOT\_Shadow\_Pull|
|IOT\_Subdevice\_Register|
|IOT\_Subdevice\_Unregister|
|IOT\_Subdevice\_Login|
|IOT\_Subdevice\_Logout|
|IOT\_Gateway\_Get\_TOPO|
|IOT\_Gateway\_Get\_Config|
|IOT\_Gateway\_Publish\_Found\_List|
|IOT\_Gateway\_Publish|
|IOT\_Gateway\_RRPC\_Response|
|linkkit\_answer\_service|
|linkkit\_invoke\_raw\_service|
|linkkit\_trigger\_event|
|linkkit\_invoke\_fota\_service|
|linkkit\_invoke\_cota\_get\_config|
|linkkit\_invoke\_cota\_service|
|CoAP Send|IOT\_CoAP\_SendMessage|
|HTTP Send|IOT\_HTTP\_SendMessage|
|You can call these operations for free. However, you may be charged for receiving messages.|IOT\_CMP\_Register|
|IOT\_MQTT\_Subscribe|
|IOT\_Gateway\_Subscribe|
|IOT\_Gateway\_RRPC\_Register|

|API|Description|
|:--|:----------|
|Pub|Publish messages.|
|PubBroadcast|Publish broadcast messages.|
|RRpc|Use RRPC method to send requests to devices.|
|DeleteDevice|When you delete a sub-device, a message of `/sys/{productKey}/{deviceName}/thing/delete`is triggered.|
|DisableThing|When you disable a sub-device, a message of `/sys/${productKey}/${deviceName}/thing/disable` is triggered.|
|EnableThing|When you enable a sub-device, a message of `/sys/${productKey}/${deviceName}/thing/enable` is triggered.|
|NotifyAddThingTopo|When you add a topological relationship, a message of `/sys/${productKey}/${deviceName}/thing/topo/add/notify` is triggered.|
|UpdateDeviceShadow|Update the shadow information of a device.|
|InvokeThingService|When you invoke a service provided by a device, a message of `/sys/${productKey}/${deviceName}/thing/service/${tsl.service.identitier}` is triggered.|
|InvokeThingsService|When you invoke multiple services provided by multiple devices, multiple messages of `/sys/{productKey}/{deviceName}/thing/service/{tsl.service.identitier}` are triggered.|
|SetDeviceProperty|When you set properties for a device, a message of `/sys/${productKey}/${deviceName}/thing/service/property/set` is triggered.|
|SetDevicesProperty|When you set properties for multiple devices, multiple messages of `/sys/{productKey}/{deviceName}/thing/service/property/set` are triggered.|


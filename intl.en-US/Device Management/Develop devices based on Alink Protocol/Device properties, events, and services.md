---
keyword: [Alink protocol, TSL model, set properties, call services, report data, response, data structure of messages, IoT Platform, IoT, data structure, message structure, request topic, response topic]
---

# Device properties, events, and services

If you define a Thing Specification Language \(TSL\) model for a product, the devices of the product can report properties and events to IoT Platform. IoT Platform can send commands to devices. These commands are used to set device properties and call services.

A TSL model includes device properties, events, and services. For more information about the data format of TSL models, see [Format of a TSL model](/intl.en-US/Device Management/TSL/What is a TSL model?.md).

Device data is reported in the following formats: Alink JSON and custom. You can use one of the formats to report device data. We recommend that you use the Alink JSON format.

-   ICA standard data format \(Alink JSON\): A device generates data in the standard format that is defined by IoT Platform, and reports the data to IoT Platform.
-   Custom: If the custom mode is used, a device sends raw data such as a binary data stream to IoT Platform. IoT Platform runs the script that you have submitted to convert the raw data into a standard format. For more information, see [Data parsing scripts](/intl.en-US/Device Management/Data parsing/What is data parsing?.md). IoT Platform generates data in the Alink JSON format. Before the data is sent to devices, the data is converted into binary data.

    ![TSL model-based pass-through](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5392039951/p39981.png)


## Report device properties

Upstream data in the custom format:

-   Request topic: `/sys/{productKey}/{deviceName}/thing/model/up_raw`
-   Response topic: `/sys/{productKey}/{deviceName}/thing/model/up_raw_reply`

Raw data that is reported by a device is sent to the request topic.

**Note:** Raw data that is transmitted over MQTT is in the hexadecimal format.

Example:

```
0x00002233441232013fa00000
```

**Note:**

Example of downstream data:

```
{
    "id":"123",
    "code": 200,
    "data":{}
}
```

Upstream data in the Alink JSON format

-   Request topic: `/sys/{productKey}/{deviceName}/thing/event/property/post`
-   Response topic: `/sys/{productKey}/{deviceName}/thing/event/property/post`

Sample request in the Alink JSON format:

```
{
  "id": "123",
  "version": "1.0",
  "params": {
    "Power": {
      "value": "on",
      "time": 1524448722000
    },
    "WF": {
      "value": 23.6,
      "time": 1524448722000
    }
  },
  "method": "thing.event.property.post"
}
```

|Parameter|Type|Description|
|:--------|:---|:----------|
|id|String|The message ID. Valid values: 0 to 4294967295. Each message ID must be unique for the device.|
|version|String|The version of the protocol. Valid value: 1.0.|
|method|String|The request method. Valid value: thing.event.property.post.|
|params|Object|The request parameters. In the preceding example, the device reports the Power and WF properties. Each property includes the report time and reported value.|
|time|Long|The UTC timestampwhen the property was reported. Unit: milliseconds. Optional. You can specify a timestamp based on your business requirements. If a device sends messages at a high frequency, we recommend that you specify a timestamp for each message to identify the order in which the messages are sent.|
|value|Object|The value of the property.|

Response format:

```
{
  "id": "123",
  "code": 200,
  "data": {}
}
```

|Parameter|Type|Description|
|:--------|:---|:----------|
|id|String|The message ID. Valid values: 0 to 4294967295. Each message ID must be unique for the device.|
|code|Integer|The HTTP status code. For more information, see [Common codes on devices](/intl.en-US/Device Management/Develop devices based on Alink Protocol/Common codes on devices.md).|
|data|Object|The response data in the case of a successful request.|

|HTTP status code|Error message|Description|
|:---------------|:------------|:----------|
|460|request parameter error|The error message returned because one or more request parameters are invalid.|
|6106|map size must less than 200|The error message returned because the number of reported properties exceeds 200.|
|6313|tsl service not available|The TSL verification service is unavailable.

IoT Platform verifies properties that are reported by a device based on the defined TSL model.

Only valid properties are reserved after the verification. A successful verification is indicated even if all properties are screened.

If the TSL verification service is unavailable, the 6313 HTTP status code is returned. |

You can use the [data forwarding feature of the rules engine](/intl.en-US/Communications/Data Forwarding/Configure data forwarding rules.md) to forward properties that are reported by devices to the required cloud services. For more information about the required topics and data formats, see [Report device properties](/intl.en-US/Communications/Data formats.md).

## Set device properties

You can call the [SetDeviceProperty](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/SetDeviceProperty.md) or [SetDevicesProperty](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/SetDevicesProperty.md) API operation to send commands to devices to set properties.

Downstream data in the custom format:

-   Request topic: `/sys/{productKey}/{deviceName}/thing/model/down_raw`
-   Response topic: `/sys/{productKey}/{deviceName}/thing/model/down_raw_reply`

Downstream data in the Alink JSON format:

-   Request topic: `/sys/{productKey}/{deviceName}/thing/service/property/set`
-   Response topic: `/sys/{productKey}/{deviceName}/thing/service/property/set_reply`

Sample request in the Alink JSON format:

```
{
  "id": "123",
  "version": "1.0",
  "params": {
    "temperature": "30.5"
  },
  "method": "thing.service.property.set"
}
```

|Parameter|Type|Description|
|:--------|:---|:----------|
|id|String|The message ID. Valid values: 0 to 4294967295. Each message ID must be unique for the device. |
|version|String|The version of the protocol. Valid value: 1.0.|
|params|Object|The properties to set. In the preceding example, use the `{ "temperature": "30.5" }` key-value pair to set the temperature property to 30.5.|
|method|String|The request method. Valid value: thing.service.property.set.|

Sample response in the Alink JSON format:

```
{
  "id": "123",
  "code": 200,
  "data": {}
}
```

|Parameter|Type|Description|
|:--------|:---|:----------|
|id|String|The message ID. Valid values: 0 to 4294967295. Each message ID must be unique for the device.|
|code|Integer|For more information about HTTP status codes, see [Common codes on devices](/intl.en-US/Device Management/Develop devices based on Alink Protocol/Common codes on devices.md).|
|data|Object|The response data in the case of a successful request.|

You can use the [data forwarding feature of the rules engine](/intl.en-US/Communications/Data Forwarding/Configure data forwarding rules.md) to forward property setting results to the required cloud services. For more information about the required topics and data formats, see [Submit responses to downstream requests](/intl.en-US/Communications/Data formats.md).

## Submit device events

Upstream \(passthrough\)

-   Request topic: `/sys/{productKey}/{deviceName}/thing/model/up_raw`
-   Response topic: `/sys/{productKey}/{deviceName}/thing/model/up_raw_reply`

The raw data of a request message:

```
0xff0000007b00
```

**Note:**

Response message from IoT Platform:

```
{
    "id":"123",
    "code": 200,
    "data":{}
}
```

Upstream data in the Alink JSON format:

-   Request topic: `/sys/{productKey}/{deviceName}/thing/event/{tsl.event.identifier}/post`
-   Response topic: `/sys/{productKey}/{deviceName}/thing/event/{tsl.event.identifier}/post`

Sample request in the Alink JSON format:

```
{
  "id": "123",
  "version": "1.0",
  "params": {
    "value": {
      "Power": "on",
      "WF": "2"
    },
    "time": 1524448722000
  },
  "method": "thing.event.{tsl.event.identifier}.post"
}
```

|Parameter|Type|Description|
|:--------|:---|:----------|
|id|String|The message ID. Valid values: 0 to 4294967295. Each message ID must be unique for the device.|
|version|String|The protocol version. Valid value: 1.0.|
|method|String|The request method. Valid value: thing.event.\{tsl.event.identifier\}.post. Replace `{tsl.event.identifier}` with the ID of an event that you have defined in the TSL model. For more information, see [Add a TSL feature](/intl.en-US/Device Management/TSL/Add a TSL feature.md).|
|params|Object|The parameters of the event.|
|value|Object|The values of the parameters. Example: ```
{
      "Power": "on",
      "WF": "2"
    }
``` |
|time|Long|Optional. The UTC timestamp that is generated for the event. Unit: milliseconds. You can specify a timestamp based on your business requirements. If a device sends messages at a high frequency, we recommend that you specify a timestamp for each message to identify the order in which the messages are sent. |

Sample response in the Alink JSON format:

```
{
  "id": "123",
  "code": 200,
  "data": {}
}
```

|Parameter|Type|Description|
|:--------|:---|:----------|
|id|String|The message ID. Valid values: 0 to 4294967295. Each message ID must be unique for the device.|
|code|Integer|The HTTP status code. For more information, see [Common codes on devices](/intl.en-US/Device Management/Develop devices based on Alink Protocol/Common codes on devices.md). **Note:** IoT Platform verifies all the events that are reported by devices. IoT Platform compares the format of each reported property with the predefined format in the TSL model to verify the validity of the property. IoT Platform drops an invalid event and returns an error code. |
|data|Object|The response data in the case of a successful request.|

Sample event in the Alink JSON format:

The following example shows the alarm event that is defined in the TSL model of a product:

```
{
  "schema": "https://iot-tsl.oss-cn-shanghai.aliyuncs.com/schema.json",
  "link": "/sys/${productKey}/airCondition/thing/",
  "profile ":{
    "productKey": "Replace ${productKey} with your product key",
    "deviceName": "Replace airCondition with your device name"
  },
  "events": [
    {
      "identifier": "alarm",
      "name": "alarm",
      "desc": "Fan alert",
      "type": "alert",
      "required": true,
      "outputData": [
        {
          "identifier": "errorCode",
          "name": "Error code",
          "dataType": {
            "type": "text",
            "specs": {
              "length": "255"
            }
          }
        }
      ],
      "method": "thing.event.alarm.post"
    }
  ]
}
```

Sample request in the Alink JSON format when a device reports the event:

```
{
  "id": "123",
  "version": "1.0",
  "params": {
    "value": {
      "errorCode": "error"
    },
    "time": 1524448722000
  },
  "method": "thing.event.alarm.post"
}
```

You can use the [data forwarding feature of the rules engine](/intl.en-US/Communications/Data Forwarding/Configure data forwarding rules.md) to forward events that are reported by devices to the required cloud services. For more information about the required topics and data formats, see [Reporting of device events](/intl.en-US/Communications/Data formats.md).

## Invoke device services in an asynchronous manner

IoT Platform allows you to invoke services in a synchronous or asynchronous manner. When you define a [service](/intl.en-US/Device Management/TSL/Add a TSL feature.md), you must specify the invocation method for the service. For more information, see [Service invocation process in Alink](/intl.en-US/Device Management/Develop devices based on Alink Protocol/Communications over Alink protocol.md).

-   Synchronous method: You can call the [InvokeThingService](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/InvokeThingService.md) or [InvokeThingsService](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/InvokeThingsService.md) API operation to invoke services. IoT Platform uses the Revert-RPC \(RRPC\) method to push requests to devices. If the service invocation method is synchronous, IoT Platform subscribes to the RRPC topic. For more information about how to implement RRPC, see [What is RRPC?](/intl.en-US/Communications/RRPC/What is RRPC?.md)
-   Asynchronous method: You can call the [InvokeThingService](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/InvokeThingService.md) or [InvokeThingsService](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/InvokeThingsService.md) API operation to invoke services. IoT Platform pushes requests to devices in an asynchronous manner, and the devices return results in an asynchronous manner. If the service invocation method is asynchronous, IoT Platform subscribes to the asynchronous response topic.

    You can use the [data forwarding feature of the rules engine](/intl.en-US/Communications/Data Forwarding/Configure data forwarding rules.md) to obtain the results from an asynchronous invocation. For more information about the required topics and data formats, see [Submit responses to downstream requests](/intl.en-US/Communications/Data formats.md).


Downstream data in the custom format:

-   Request topic: `/sys/{productKey}/{deviceName}/thing/model/down_raw`
-   Response topic: `/sys/{productKey}/{deviceName}/thing/model/down_raw_reply`

Downstream data in the Alink JSON format:

-   Request topic: `/sys/{productKey}/{deviceName}/thing/service/{tsl.service.identifier}`
-   Response topic: `/sys/{productKey}/{deviceName}/thing/service/{tsl.service.identifier}_reply`

Sample request in the Alink JSON format:

```
{
  "id": "123",
  "version": "1.0",
  "params": {
    "Power": "on",
    "WF": "2"
  },
  "method": "thing.service.{tsl.service.identifier}"
}
```

|Parameter|Type|Description|
|:--------|:---|:----------|
|id|String|The message ID. Valid values: 0 to 4294967295. Each message ID must be unique for the device. |
|version|String|The version of the protocol. Valid value: 1.0.|
|params|Object|The parameters that are required to invoke the service. You must specify the identifier and value of the service. Example: ```
{
      "Power": "on",
      "WF": "2"
    }
``` |
|method|String|The request method. Valid value: thing.service.\{tsl.service.identifier\}. **Note:** Replace `{tsl.service.identifier}` with the ID of a service that is defined in the TSL model. For more information, see [Add a TSL feature](/intl.en-US/Device Management/TSL/Add a TSL feature.md). |

Sample response in the Alink JSON format:

```
{
  "id": "123",
  "code": 200,
  "data": {}
}
```

|Parameter|Type|Description|
|:--------|:---|:----------|
|id|String|The message ID. Valid values: 0 to 4294967295. Each message ID must be unique for the device.|
|code|Integer|The HTTP status code. For more information, see [Common codes on devices](/intl.en-US/Device Management/Develop devices based on Alink Protocol/Common codes on devices.md).|
|data|Object|The response data. The value of the parameter is based on the TSL model of the product. If the service does not return a response, the value of the data parameter is empty. If the service returns a response, the returned data follows the service definition in the TSL model. |

Sample service in the Alink JSON format:

The following example shows the SetWeight service that is defined in the TSL model of a product:

```
{
  "schema": "https://iotx-tsl.oss-ap-southeast-1.aliyuncs.com/schema.json",
  "profile ":{
    "productKey": "testProduct01"
  },
  "services": [
    {
      "outputData": [
        {
          "identifier": "OldWeight",
          "dataType": {
            "specs": {
              "unit": "kg",
              "min": "0",
              "max": "200",
              "step": "1"
            },
            "type": "double"
          },
          "name": "OldWeight"
        },
        {
          "identifier": "CollectTime",
          "dataType": {
            "specs": {
              "length": "2048"
            },
            "type": "text"
          },
          "name": "CollectTime"
        }
      ],
      "identifier": "SetWeight",
      "inputData": [
        {
          "identifier": "NewWeight",
          "dataType": {
            "specs": {
              "unit": "kg",
              "min": "0",
              "max": "200",
              "step": "1"
            },
            "type": "double"
          },
          "name": "NewWeight"
        }
      ],
      "method": "thing.service.SetWeight",
      "name": "Set weight",
      "required": false,
      "callType": "async"
    }
  ]
}
```

Sample service invocation request in the Alink JSON format:

```
{
  "method": "thing.service.SetWeight",
  "id": "105917531",
  "params": {
    "NewWeight": 100.8
  },
  "version": "1.0"
}
```

Sample response in the Alink JSON format:

```
{
  "id": "105917531",
  "code": 200,
  "data": {
    "CollectTime": "1536228947682",
    "OldWeight": 100.101
  }
}
```

## Report data in batches from a gateway

A gateway can report its own properties and events in batches. The gateway can also report the properties and events of the connected sub-devices in batches.

**Note:**

-   A gateway can report a maximum of 200 properties and 20 events at a time.
-   A gateway can report the data of a maximum of 20 sub-devices at a time.

Upstream data in the custom format:

-   Request topic: `/sys/{productKey}/{deviceName}/thing/model/up_raw`
-   Response topic: `/sys/{productKey}/{deviceName}/thing/model/up_raw_reply`

The raw data of a request message:

```
0xff0000007b00
```

**Note:**

Sample response from IoT Platform:

```
{
  "id": "123",
  "code": 200,
  "data": {}
}
```

Upstream data in the Alink JSON format:

-   Request topic: `/sys/{productKey}/{deviceName}/thing/event/property/pack/post`
-   Response topic: `/sys/{productKey}/{deviceName}/thing/event/property/pack/post_reply`

Sample request in the Alink JSON format:

```
{
  "id": "123",
  "version": "1.0",
  "params": {
    "properties": {
      "Power": {
        "value": "on",
        "time": 1524448722000
      },
      "WF": {
        "value": { },
        "time": 1524448722000
      }
    },
    "events": {
      "alarmEvent1": {
        "value": {
          "param1": "on",
          "param2": "2"
        },
        "time": 1524448722000
      },
      "alertEvent2": {
        "value": {
          "param1": "on",
          "param2": "2"
        },
        "time": 1524448722000
      }
    },
    "subDevices": [
      {
        "identity": {
          "productKey": "",
          "deviceName": ""
        },
        "properties": {
          "Power": {
            "value": "on",
            "time": 1524448722000
          },
          "WF": {
            "value": { },
            "time": 1524448722000
          }
        },
        "events": {
          "alarmEvent1": {
            "value": {
              "param1": "on",
              "param2": "2"
            },
            "time": 1524448722000
          },
          "alertEvent2": {
            "value": {
              "param1": "on",
              "param2": "2"
            },
            "time": 1524448722000
          }
        }
      }
    ]
  },
  "method": "thing.event.property.pack.post"
}
```

|Parameter|Type|Description|
|:--------|:---|:----------|
|id|String|The message ID. Valid values: 0 to 4294967295. Each message ID must be unique for the device.|
|version|String|The version of the protocol. Set this parameter to 1.0.|
|params|Object|The request parameters.|
|properties|Object|The properties. You must specify the identifier, value, and time for each property. The time parameter is optional. You can specify a timestamp based on your business requirements. If a device sends messages at a high frequency, we recommend that you specify a timestamp for each message to identify the order in which the messages are sent. |
|events|Object|The events. You must specify the identifier, value, and time for each event. The time parameter is optional. You can specify a timestamp based on your business requirements. If a device sends messages at a high frequency, we recommend that you specify a timestamp for each message to identify the order in which the messages are sent. |
|subDevices|Object|The device information.|
|productKey|String|The product key of each sub-device.|
|deviceName|String|The name of the sub-device.|
|method|String|The request method. Valid value: thing.event.property.pack.post.|

Sample response in the Alink JSON format:

```
{
  "id": "123",
  "code": 200,
  "data": {}
}
```

|Parameter|Type|Description|
|:--------|:---|:----------|
|id|String|The message ID. Valid values: 0 to 4294967295. Each message ID must be unique.|
|code|Integer|The response code. The 200 value indicates a successful request. **Note:** IoT Platform verifies whether devices, topological relationships, reported properties, and reported events follow the definition of the TSL model for a product. If one of the preceding items cannot pass the verification, devices fail to report data. |
|data|Object|The response data in the case of a successful request.|

## Report the historical data of a TSL model

Upstream data:

-   Request topic: `/sys/{productKey}/{deviceName}/thing/event/property/history/post`
-   Response topic: `/sys/{productKey}/{deviceName}/thing/event/property/history/post`

Sample request in the Alink JSON format:

```
{
  "id": 123, 
  "version": "1.0", 
  "method": "thing.event.property.history.post", 
  "params": [
    {
      "identity": {
        "productKey": "", 
        "deviceName": ""
      }, 
      "properties": [
        {
          "Power": {
            "value": "on", 
            "time": 123456
          }, 
          "WF": {
            "Value": "3" 
            "time": 123456
          }
        }, 
        {
          "Power": {
            "value": "on", 
            "time": 123456
          }, 
          "WF": {
            "Value": "3" 
            "time": 123456
          }
        }
      ], 
      "events": [
        {
          "alarmEvent": {
            "value": {
              "Power": "on", 
              "WF": "2"
            }, 
            "time": 123456
          }, 
          "alertEvent": {
            "value": {
              "Power": "off", 
              "WF": "3"
            }, 
            "time": 123456
          }
        }
      ]
    }, 
    {
      "identity": {
        "productKey": "", 
        "deviceName": ""
      }, 
      "properties": [
        {
          "Power": {
            "value": "on", 
            "time": 123456
          }, 
          "WF": {
            "value": "3", 
            "time": 123456
          }
        }
      ], 
      "events": [
        {
          "alarmEvent": {
            "value": {
              "Power": "on", 
              "WF": "2"
            }, 
            "time": 123456
          }, 
          "alertEvent": {
            "value": {
              "Power": "off", 
              "WF": "3"
            }, 
            "time": 123456
          }
        }
      ]
    }
  ]
}
```

|Parameter|Type|Description|
|:--------|:---|:----------|
|id|String|The message ID. Valid values: 0 to 4294967295. Each ID must be unique for the device.|
|version|String|The version of the protocol. Valid value: 1.0.|
|method|String|The request method. Valid value: thing.event.property.history.post.|
|params|Object|The request parameters.|
|identity|String|The certificate information of the device to which the historical data belongs. You must specify the productKey and deviceName parameters. **Note:** A directly connected device can report only the historical data of its own TSL model. A gateway can report the historical data of the TSL model for sub-devices that are attached to the gateway. If a gateway reports the historical data of a sub-device, the identity parameter includes the sub-device information. |
|properties|Object|The properties. You must specify the identifier, value, and time parameters for each property.|
|events|Object|The events. You must specify the identifier, value, and time parameters for each event.|

Sample response in the Alink JSON format:

```
{
    "id":"123",
    "code": 200,
    "data":{}
}
```

You can use the [data forwarding feature of the rules engine](/intl.en-US/Communications/Data Forwarding/Configure data forwarding rules.md) to forward the reported historical data of a TSL model to the required cloud services. For more information about the required topics and data formats, see [Format of historical data for a TSL model](/intl.en-US/Communications/Data formats.md).


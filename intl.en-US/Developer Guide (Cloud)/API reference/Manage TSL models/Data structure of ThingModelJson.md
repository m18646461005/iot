---
keyword: [IoT, ThingModelJson, extendConfig]
---

# Data structure of ThingModelJson

When you call API operations related to Thing Specification Language \(TSL\), the request parameters or response parameters may contain the ThingModelJson parameter. The value of this parameter indicates the TSL data structure that is stored in IoT Platform. This TSL data structure is different from the original TSL data structure.

All fields in ThingModelJson are sorted by key in alphabetical order.

## Data structure

```
{
  "_ppk":{
       "description":"test",
       "version":"159244410****"
  }
  "events":[],
  "productKey":"al12345****",
  "properties":[],
  "services":[]
}
```

|Parameter|Data type|Description|
|---------|---------|-----------|
|productKey|String|The key of the product to which the TSL belongs.|
|\_ppk|String|The information of the TSL version, including the version and description parameters.|
|version|String|The version of the TSL. This parameter is available only for published TSLs.|
|description|String|The description of the TSL version. This parameter is available only for published TSLs.|
|properties|List|The property list of the TSL. For more information about the parameters of the property data, see [Specifications for the property data](#section_2ra_ly5_hdb).In each property, you can use the extendConfig parameter to define the extended information of the TSL. For more information, see [Specifications for the extendConfig data](#section_6bu_yuq_41z). If you do not need to define the extended information, do not specify the extendConfig parameter. |
|services|List|The service list of the TSL. For more information about the parameters of the service data, see [Specifications for the service data](#section_ltc_ec1_kmx).In each service, you can use the extendConfig parameter to define the extended information of the TSL. For more information, see [Specifications for the extendConfig data](#section_6bu_yuq_41z). If you do not need to define the extended information, do not specify the extendConfig parameter. |
|events|List|The event list of the TSL. For more information about the parameters of the event data, see [Specifications for the event data](#section_211_jtv_7kn).In each event, you can use the extendConfig parameter to define the extended information of the TSL. For more information, see [Specifications for the extendConfig data](#section_6bu_yuq_41z). If you do not need to define the extended information, do not specify the extendConfig parameter. |

## Specifications for the property data

The following table lists the parameters that are included in the property data.

|Parameter|Data type|Required|Description|
|---------|---------|--------|-----------|
|productKey|String|Yes|The key of the product to which the TSL belongs.|
|identifier|String|Yes|The identifier of the property. The identifier must be 1 to 50 characters in length, and can contain letters, digits, and underscores \(\_\). **Note:** The identifier cannot be one of the following words: set, get, post, property, event, time, and value. |
|dataType|String|Yes|The data type of the property value. Valid values: ARRAY, STRUCT, INT, FLOAT, DOUBLE, TEXT, DATE, ENUM, and BOOL.

You can specify different parameters based on the data type. For more information, see the specifications for the corresponding data types in this article. |
|name|String|Yes|The name of the property. The name must be 1 to 30 characters in length, and can contain letters, digits, hyphens \(-\), underscores \(\_\), and periods \(.\). It must start with a letter or digit.|
|rwFlag|String|Yes|The type of operation that IoT Platform can perform on the property. Valid values: -   READ\_WRITE: read and write
-   READ\_ONLY: read-only
-   WRITE\_ONLY: write-only |
|dataSpecs|Object|No|If you set dataType to INT, FLOAT, DOUBLE, TEXT, DATE, or ARRAY, the data specifications are included in the dataSpecs parameter. **Note:**

-   The dataSpecs parameter excludes the data that is used to define properties, services, events, and parameters.
-   You must specify the dataSpecs or dataSpecsList parameter based on the actual data type. |
|dataSpecsList|List|No|If you set the dataType to ENUM, BOOL, or STRUCT, the data specifications are included in the dataSpecsList parameter. **Note:**

-   The dataSpecs parameter excludes the data that is used to define properties, services, events, and parameters.
-   You must specify the dataSpecs or dataSpecsList parameter based on the actual data type. |
|required|Boolean|Yes|Specifies whether the property is required for the standard category. Valid values: -   true: yes
-   false: no |
|custom|Boolean|Yes|Specifies whether the TSL feature is a self-defined feature. Valid values: -   true: yes
-   false: no |

## Specifications for the service data

The following table lists the parameters that are included in the service data.

|Parameter|Data type|Required|Description|
|---------|---------|--------|-----------|
|productKey|String|Yes|The key of the product to which the TSL belongs.|
|identifier|String|Yes|The identifier of the service. The identifier must be 1 to 50 characters in length, and can contain letters, digits, and underscores \(\_\). **Note:** The identifier cannot be one of the following words: set, get, post, property, event, time, and value. |
|serviceName|String|Yes|The name of the service. The name must be 1 to 30 characters in length, and can contain letters, digits, hyphens \(-\), underscores \(\_\), and periods \(.\). It must start with a letter or digit.|
|inputParams|List|No|The input parameters of the service. For more information, see [Specifications for the input and output parameters](#section_owk_mxx_wq8).|
|outputParams|List|No|The output parameters of the service. For more information, see [Specifications for the input and output parameters](#section_owk_mxx_wq8).|
|required|Boolean|Yes|Specifies whether the service is required for the standard category. Valid values: -   true: yes
-   false: no |
|callType|String|Yes|The method that is used to call the service. -   ASYNC: asynchronously calls the service
-   SYNC: synchronously calls the service |
|custom|Boolean|Yes|Specifies whether the TSL feature is a self-defined feature. Valid values: -   true: yes
-   false: no |

## Specifications for the event data

The following table lists the parameters that are included in the event data.

|Parameter|Data type|Required|Description|
|---------|---------|--------|-----------|
|productKey|String|Yes|The key of the product to which the TSL belongs.|
|identifier|String|Yes|The identifier of the event. The identifier must be 1 to 50 characters in length, and can contain letters, digits, and underscores \(\_\). **Note:** The identifier cannot be one of the following words: set, get, post, property, event, time, and value. |
|eventName|String|Yes|The name of the event. The name must be 1 to 30 characters in length, and can contain letters, digits, hyphens \(-\), underscores \(\_\), and periods \(.\). It must start with a letter or digit.|
|eventType|String|Yes|The type of the event. Valid values: -   INFO\_EVENT\_TYPE: information
-   ALERT\_EVENT\_TYPE: alert
-   ERROR\_EVENT\_TYPE: error |
|outputdata|List|No|The output parameters of the event. For more information, see [Specifications for the input and output parameters](#section_owk_mxx_wq8).|
|required|Boolean|Yes|Specifies whether the event is required for the standard category. Valid values: -   true: yes
-   false: no |
|custom|Boolean|Yes|Specifies whether the TSL feature is a self-defined feature. Valid values: -   true: yes
-   false: no |

## Specifications for the input and output parameters

The following table lists the parameters that are included in the input and output parameters of a service or event.

|Parameter|Data type|Required|Description|
|---------|---------|--------|-----------|
|dataType|String|Yes|The data type of the parameter. Valid values: ARRAY, STRUCT, INT, FLOAT, DOUBLE, TEXT, DATE, ENUM, and BOOL.

For more information, see the specifications for each data type in this article. |
|identifier|String|Yes|The identifier of the input parameter. The identifier must be 1 to 50 characters in length, and can contain letters, digits, and underscores \(\_\). **Note:** The identifier cannot be one of the following words: set, get, post, property, event, time, and value. |
|name|String|Yes|The name of the parameter. The name must be 1 to 30 characters in length, and can contain letters, digits, hyphens \(-\), underscores \(\_\), and periods \(.\). It must start with a letter or digit.|
|direction|String|Yes|Specifies whether the parameter is an input parameter or an output parameter. Valid values: -   PARAM\_INPUT: input parameter
-   PARAM\_OUTPUT: output parameter |
|paraOrder|Integer|Yes|The serial number of the parameter. The serial number starts from 0 and must be unique.|
|dataSpecs|Object|No|If you set dataType to INT, FLOAT, DOUBLE, TEXT, DATE, or ARRAY, the data specifications are included in the dataSpecs parameter. **Note:**

-   The dataSpecs parameter excludes the data that is used to define properties, services, events, and parameters.
-   You must specify the dataSpecs or dataSpecsList parameter based on the actual data type. |
|dataSpecsList|List|No|If you set dataType to ENUM, BOOL, or STRUCT, the data specifications are included in the dataSpecsList parameter.**Note:**

-   The dataSpecs parameter excludes the data that is used to define properties, services, events, and parameters.
-   You must specify the dataSpecs or dataSpecsList parameter based on the actual data type. |
|custom|Boolean|Yes|Specifies whether the parameter belongs to a self-defined feature. Valid values: -   true: yes
-   false: no |

## Specifications for INT, FLOAT, and DOUBLE

The following table lists the parameters that are included in the data of the INT, FLOAT, and DOUBLE types.

|Parameter|Data type|Required|Description|
|---------|---------|--------|-----------|
|dataType|String|Yes|The type of the data. Valid values: INT, FLOAT, and DOUBLE.|
|max|String|Yes|The maximum value. Valid data types: INT, FLOAT, and DOUBLE.|
|min|String|Yes|The minimum value. Valid data types: INT, FLOAT, and DOUBLE.|
|step|String|Yes|The step size. Valid data types: INT, FLOAT, and DOUBLE.|
|precise|String|No|The precision of the value. You can specify this parameter when the dataType parameter is set to FLOAT or DOUBLE.|
|defaultValue|String|No|You can specify this parameter to set a default value.|
|unit|String|Yes|The symbol of the unit.|
|unitName|String|Yes|The name of the unit.|
|custom|Boolean|Yes|Specifies whether the TSL feature is a self-defined feature. Valid values: -   true: yes
-   false: no |

## Specifications for DATE and TEXT

The following table lists the parameters that are included in the data of the DATE and TEXT types.

|Parameter|Data type|Required|Description|
|---------|---------|--------|-----------|
|dataType|String|Yes|The type of the data. Valid values: DATE and TEXT.|
|length|Long|Yes|The length of the data. Maximum value: 2048. Unit: bytes. You must specify this parameter if the dataType parameter is set to TEXT.|
|defaultValue|String|No|You can specify this parameter to set a default value.|
|custom|Boolean|Yes|Specifies whether the TSL feature is a self-defined feature. Valid values: -   true: yes
-   false: no |

## Specifications for ARRAY

The following table lists the parameters that are included in the data of the ARRAY type.

|Parameter|Data type|Required|Description|
|---------|---------|--------|-----------|
|dataType|String|Yes|The type of the data. The value is set to ARRAY.|
|size|Long|Yes|The number of elements in the array.|
|childDataType|String|Yes|The data type of the elements in the array. Valid values: STRUCT, INT, FLOAT, DOUBLE, and TEXT.|
|dataSpecs|Object|No|If you set dataType to INT, FLOAT, DOUBLE, TEXT, DATE, or ARRAY, the data specifications are included in the dataSpecs parameter. **Note:**

-   The dataSpecs parameter excludes the data that is used to define properties, services, events, and parameters.
-   You must specify the dataSpecs or dataSpecsList parameter based on the actual data type. |
|dataSpecsList|List|No|If you set dataType to ENUM, BOOL, or STRUCT, the data specifications are included in the dataSpecsList parameter. **Note:**

-   The dataSpecs parameter excludes the data that is used to define properties, services, events, and parameters.
-   You must specify the dataSpecs or dataSpecsList parameter based on the actual data type. |
|custom|Boolean|Yes|Specifies whether the TSL feature is a self-defined feature. Valid values: -   true: yes
-   false: no |

## Specifications for ENUM and BOOL

The following table lists the parameters that are included in the data of the BOOL and ENUM types.

|Parameter|Data type|Required|Description|
|---------|---------|--------|-----------|
|dataType|String|Yes|The type of the data. Valid values: BOOL and ENUM.|
|name|String|Yes|The name of an enumerate item. The name must be 1 to 20 characters in length, and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter or digit.|
|value|Integer|Yes|The value of an enumerate item.|
|custom|Boolean|Yes|Specifies whether the TSL feature is a self-defined feature. Valid values: -   true: yes
-   false: no |

## Specifications for STRUCT

The following table lists the parameters that are included in the data of the STRUCT type.

|Parameter|Data type|Required|Description|
|---------|---------|--------|-----------|
|dataType|String|Yes|The type of the data. The value is set to STRUCT.|
|identifier|String|Yes|The identifier of the sub-parameter in the struct. The identifier must be 1 to 50 characters in length, and can contain letters, digits, and underscores \(\_\). **Note:** The identifier cannot be one of the following words: set, get, post, property, event, time, and value. |
|name|String|Yes|The name of the sub-parameter in the struct. The name must be 1 to 30 characters in length, and can contain letters, digits, hyphens \(-\), underscores \(\_\), and periods \(.\). It must start with a letter or digit.|
|childDataType|String|No|The data type of the sub-parameter in the struct. Valid values: INT, FLOAT, DOUBLE, TEXT, DATE, ENUM, and BOOL. |
|childName|String|Yes|The name of the sub-parameter in the struct. The name must be 1 to 30 characters in length, and can contain letters, digits, hyphens \(-\), underscores \(\_\), and periods \(.\). It must start with a letter or digit.|
|dataSpecs|Object|No|If you set dataType to INT, FLOAT, DOUBLE, TEXT, DATE, or ARRAY, the data specifications are included in the dataSpecs parameter.

**Note:**

-   The dataSpecs parameter excludes the data that is used to define properties, services, events, and parameters.
-   You must specify the dataSpecs or dataSpecsList parameter based on the actual data type. |
|dataSpecsList|List|No|If you set dataType to ENUM, BOOL, or STRUCT, the data specifications are included in the dataSpecsList parameter. **Note:**

-   The dataSpecs parameter excludes the data that is used to define properties, services, events, and parameters.
-   You must specify the dataSpecs or dataSpecsList parameter based on the actual data type. |
|custom|Boolean|Yes|Specifies whether the TSL feature is a self-defined feature. Valid values: -   true: yes
-   false: no |

## Specifications for the extendConfig data

In each property, event, and service, you can use the extendConfig to define the extended information of the TSL. The extended information indicates the mapping between the connection protocol and the standard TSL of the device.

**Note:** The configCode parameter is the unique identifier generated by IoT Platform. The identifier is used to define the extended information of a TSL feature.

If the gateway connection protocol of a device is set to Modbus, OPC UA, or custom, you can define the extended information of the device. Different types of extended information have different data specifications:

**Modbus type**

If the gateway connection protocol of a device is set to Modbus, you can define the extended information of the properties.

**Note:** To fully demonstrate the structure of the extendConfig data, the following example includes all parameters. However, the parameters may vary in actual scenarios. The following table describes these parameters.

```
{
  "identifier":"extend1",
  "writeFunctionCode":0,
  "writeOnly":0,
  "registerAddress":"0xFE",
  "operateType":"coilStatus",
  "scaling":0.1,
  "pollingTime":1000,
  "trigger":1,
  "bitMask":128,
  "originalDataType":{
     "type":"uint64",
     "specs":{
        "registerCount":4,
        "swap16":0,
        "reverseRegister":0}
  }
}
```

|Parameter|Data type|Description|
|---------|---------|-----------|
|identifier|String|The identifier of a property. It must be unique in a product.|
|registerAddress|String|The address of the register. It must start with 0x. Valid values: 0x0 to 0xFFFF, for example, 0xFE.|
|operateType|String|The type of the operation. Valid values:-   coilStatus: coil status
-   inputStatus: discrete input
-   holdingRegister: holding register
-   inputRegister: input register |
|writeFunctionCode|Integer|The read and write operations. The value varies based on the operation type that is specified by the operateType parameter.-   coilStatus:
    -   5: read and write \(read 0x01, write 0x05\)
    -   15: read and write \(read 0x01, write 0x0F\)
    -   0: read-only 0x01
    -   6: write-only 0x05
    -   15: write-only 0x0F
-   inputStatus:
    -   0: read-only 0x02
-   holdingRegister:
    -   6: read and write \(read 0x03, write 0x06\)
    -   16: read and write \(read 0x03, write 0x10\)
    -   0: read-only 0x03
    -   6: write-only 0x06
    -   16: write only 0x10
-   inputRegister:
    -   0: read-only 0x04 |
|writeOnly|Integer|Specifies whether the operation is write-only. Valid values:-   0: non-write-only
    -   If the writeFunctionCode parameter is not set to 0, the extendConfig parameter supports read and write operations. If you set the writeOnly parameter to 0, the extendConfig parameter supports read and write operations.
    -   If the writeFunctionCode parameter is set to 0, the extendConfig parameter supports only read operations. You must set the writeOnly parameter to 0.
-   1: write-only

If the writeFunctionCode parameter is not set to 0, the extendConfig parameter supports read and write operations. If you set the writeOnly parameter to 1, the extendConfig parameter supports only write operations. |
|scaling|Number|The scaling factor. The value cannot be 0.This parameter is unavailable for data of the string and bool types. |
|pollingTime|Integer|The collection interval. Unit: ms. You do not need to specify this parameter. The configured collection interval of the device is used.|
|trigger|Integer|The report method. Valid values: 1 and 2, where 1 refers to reporting data at a specific time and 2 refers to reporting changes.|
|bitMask|Integer|The parameters that are specific to data of the bool type.The mask. Valid values: 1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048, 4096, 8192, 16384, and 32768. |
|originalDataType|Object|The description of the original data type.|
|type|String|The type of the original data. It must be one of the following basic data types: int16, uint16, int32, uint32, int64, uint64, float, double, string, bool, and customized \(hex data that is returned in big-endian order\).|
|specs|Object|The parameters that are specific to some data types.|
|registerCount|Integer|The parameters that are specific to data of the string and customized types.The number of registers. |
|swap|Integer|The parameters that are specific to data of all types except for the string and customized types.Specifies whether to switch the high byte and low byte in the register. If so, the first and last 8 bits of the 16-bit integer in the register \(byte1byte2 -\> byte2byte1\) are swapped. Valid values:

-   0: The high byte and low byte are not swapped.
-   1: The high byte and low byte are swapped. |
|reverseRegister|Integer|The parameters that are specific to data of all types except for the string and customized types.Specifies whether to switch the high byte and low byte in the register. If so, the first and last 16 bits of the 32-bit integer in the register \(byte1byte2byte3byte4 -\> byte3byte4byte1byte2\) are swapped. Valid values:

-   0: The high byte and low byte are not swapped.
-   1: The high byte and low byte are swapped. |

**OPC UA type**

If the gateway connection protocol of a device is set to OPC UA, you can define the extended information of the properties, services, and events.

```
{
  "identifier":"extend2",
  "displayName":"Action",
  "inputData":[
    {
      "identifier":"xxxx",
      "index":1
    },
    {
      "identifier":"xxxx",
      "index":2 
    }
  ],
  "outputData":[
     {
      "identifier":"xxxx",
      "index":1
    },
    {
      "identifier":"xxxx",
      "index":2
    }
  ]
}
```

|Parameter|Data type|Description|
|---------|---------|-----------|
|identifier|String|The identifiers of the property, service, or event. It must be unique in a product.|
|displayName|String|You must specify the displayName parameter for a property or an event. You do not need to specify the displayName parameter for a service.|
|inputData|List|The input data.|
|outputData|List|The output data.|
|identifier|String|The identifier of the input data or output data. It must be unique in a product.|
|index|Integer|The index. It must be unique in both inputData and outputData.|

**Custom type**

If the gateway connection protocol of a device is set to custom, you can define the extended information of the properties, services, and events.

```
{
  "identifier":"xxx",
  "customize":{}
}
```

|Parameter|Data type|Description|
|---------|---------|-----------|
|identifier|String|The identifier of the property, service, or event. It must be unique in a product.|
|customize|Object|The custom JSON file.|

## Verify the ThingModelJson parameter

You can use the [json-schema](https://github.com/everit-org/json-schema) file to verify the input parameters in the ThingModelJson parameter.

Sample code:

```
package com.aliyun.iot.thingmodel;

import java.io.InputStream;
import java.util.ArrayList;
import java.util.Arrays;

import org.everit.json.schema.Schema;
import org.everit.json.schema.ValidationException;
import org.everit.json.schema.loader.SchemaLoader;
import org.json.JSONObject;
import org.json.JSONTokener;

/**
 * @author: ***
 * @date: 2020-01-14 15:11
 */
public class ThingModelJsonValidator {

    public static void main(String[] args) throws Exception {

        try (InputStream inputStream = ThingModelJsonValidator.class.getClassLoader().getResourceAsStream(
            "thing-model-schema.json")) {
            JSONObject rawSchema = new JSONObject(new JSONTokener(inputStream));
            Schema schema = SchemaLoader.load(rawSchema);
            long start = System.currentTimeMillis();
            JSONObject object = new JSONObject();
            String jsonStr = "{\n"
                + "\t\t\t\"productKey\": \"a1Q1Yrc****\",\n"
                + "\t\t\t\"name\": \"Alert event\",\n"
                + "\t\t\t\"identifier\": \"alarmEvent\",\n"
                + "\t\t\t\"eventName\": \"Alert event\",\n"
                + "\t\t\t\"eventType\": \"ALERT_EVENT_TYPE\",\n"
                + "\t\t\t\"outputData\": [\n"
                + "\t\t\t\t{\n"
                + "\t\t\t\t\t\"paraOrder\": 0,\n"
                + "\t\t\t\t\t\"direction\": \"PARAM_OUTPUT\",\n"
                + "\t\t\t\t\t\"dataSpecsList\": [\n"
                + "\t\t\t\t\t\t{\n"
                + "\t\t\t\t\t\t\t\"dataType\": \"ENUM\",\n"
                + "\t\t\t\t\t\t\t\"name\": \"Anti-tampering alert\",\n"
                + "\t\t\t\t\t\t\t\"value\": 0\n"
                + "\t\t\t\t\t\t},\n"
                + "\t\t\t\t\t\t{\n"
                + "\t\t\t\t\t\t\t\"dataType\": \"ENUM\",\n"
                + "\t\t\t\t\t\t\t\"name\": \"Anti-tampering alert is canceled.\",\n"
                + "\t\t\t\t\t\t\t\"value\": 1\n"
                + "\t\t\t\t\t\t}\n"
                + "\t\t\t\t\t],\n"
                + "\t\t\t\t\t\"dataType\": \"ENUM\",\n"
                + "\t\t\t\t\t\"identifier\": \"alarmType\",\n"
                + "\t\t\t\t\t\"name\": \"Alert type\",\n"
                + "\t\t\t\t\t\"index\": 0,\n"
                + "\t\t\t\t\t\"custom\": true\n"
                + "\t\t\t\t}\n"
                + "\t\t\t],\n"
                + "\t\t\t\"outputParams\": [\n"
                + "\t\t\t\t{\n"
                + "\t\t\t\t\t\"index\": 0,\n"
                + "\t\t\t\t\t\"identifier\": \"alarmType\"\n"
                + "\t\t\t\t}\n"
                + "\t\t\t],\n"
                + "\t\t\t\"custom\": true\n"
                + "\t\t}";

            object.put("properties", new ArrayList<>());
            object.put("services", new ArrayList<>());
            object.put("events", Arrays.asList(com.alibaba.fastjson.JSONObject.parseObject(jsonStr)));
            object.put("productKey", "a1Q1Yrc****");
            schema.validate(object); // throws a ValidationException if this object is invalid
            //}
            System.out.println(System.currentTimeMillis() - start);
        }
        catch (ValidationException exception) {
            System.out.println(exception);
        }
    }

}
```

The following section describes the data structure that is defined in the json\_schema file:

```
{
  "id": "http://json-schema.org/draft-04/schema#",
  "$schema": "http://json-schema.org/draft-04/schema#",
  "description": "Core schema meta-schema",
  "definitions": {
    "nameDefinition": {
      "type": "string",
      "pattern": "^[\\u4E00-\\u9FA5a-zA-Z0-9][\\u4E00-\\u9FA5a-zA-Z0-9_\\-\\(\\)\\uFF08\\uFF09\\u0020\\s\\.]{0,39}$"
    },
    "identifierDefinition": {
      "type": "string",
      "pattern": "[_a-zA-Z0-9]{1,50}"
    },
    "descriptionDefinition": {
      "type": "string",
      "pattern": ".{1,2048}"
    },
    "rwFlagDefinition": {
      "type": "string",
      "pattern": "(READ_WRITE|READ_ONLY|WRITE_ONLY)"
    },
    "callTypeDefinition": {
      "type": "string",
      "pattern": "(ASYNC|SYNC)"
    },
    "eventTypeDefinition": {
      "type": "string",
      "pattern": "(INFO_EVENT_TYPE|ALERT_EVENT_TYPE|ERROR_EVENT_TYPE)"
    },
    "requiredDefinition": {
      "type": "boolean"
    },
    "customDefinition": {
      "type": "boolean"
    },
    "directionDefinition": {
      "type": "string",
      "pattern": "(PARAM_INPUT|PARAM_OUTPUT)"
    },
    "argumentDefinition": {
      "required": [
        "identifier",
        "name",
        "dataType",
        "custom",
        "direction",
        "paraOrder"
      ],
      "properties": {
        "direction": {
          "$ref": "#/definitions/directionDefinition"
        },
        "paraOrder": {
          "type": "integer"
        },
        "identifier": {
          "$ref": "#/definitions/identifierDefinition"
        },
        "name": {
          "$ref": "#/definitions/nameDefinition"
        },
        "dataType": {
          "$ref": "#/definitions/dataTypeDefinition"
        },
        "description": {
          "$ref": "#/definitions/descriptionDefinition"
        },
        "custom": {
          "$ref": "#/definitions/customDefinition"
        },
        "dataSpecs": {
          "type": "object"
        },
        "dataSpecsList": {
          "type": "array"
        }
      }
    },
    "propertyDefinition": {
      "required": [
        "identifier",
        "name",
        "dataType",
        "productKey",
        "rwFlag",
        "custom",
        "required"
      ],
      "properties": {
        "identifier": {
          "$ref": "#/definitions/identifierDefinition"
        },
        "name": {
          "$ref": "#/definitions/nameDefinition"
        },
        "dataType": {
          "$ref": "#/definitions/dataTypeDefinition"
        },
        "rwFlag": {
          "$ref": "#/definitions/rwFlagDefinition"
        },
        "required": {
          "$ref": "#/definitions/requiredDefinition"
        },
        "description": {
          "$ref": "#/definitions/descriptionDefinition"
        },
        "custom": {
          "$ref": "#/definitions/customDefinition"
        },
        "dataSpecs": {
          "type": "object"
        },
        "dataSpecsList": {
          "type": "array"
        }
      }
    },
    "serviceDefinition": {
      "required": [
        "identifier",
        "serviceName",
        "productKey",
        "callType",
        "custom",
        "required"
      ],
      "properties": {
        "identifier": {
          "$ref": "#/definitions/identifierDefinition"
        },
        "serviceName": {
          "$ref": "#/definitions/nameDefinition"
        },
        "callType": {
          "$ref": "#/definitions/callTypeDefinition"
        },
        "required": {
          "$ref": "#/definitions/requiredDefinition"
        },
        "description": {
          "$ref": "#/definitions/descriptionDefinition"
        },
        "custom": {
          "$ref": "#/definitions/customDefinition"
        },
        "inputParams": {
          "type": "array",
          "items": {
            "$ref": "#/definitions/argumentDefinition"
          }
        },
        "outputParams": {
          "type": "array",
          "items": {
            "$ref": "#/definitions/argumentDefinition"
          }
        }
      }
    },
    "eventDefinition": {
      "required": [
        "identifier",
        "eventName",
        "eventType",
        "productKey",
        "custom",
        "required"
      ],
      "properties": {
        "identifier": {
          "$ref": "#/definitions/identifierDefinition"
        },
        "eventName": {
          "$ref": "#/definitions/nameDefinition"
        },
        "eventType": {
          "$ref": "#/definitions/eventTypeDefinition"
        },
        "required": {
          "$ref": "#/definitions/requiredDefinition"
        },
        "description": {
          "$ref": "#/definitions/descriptionDefinition"
        },
        "custom": {
          "$ref": "#/definitions/customDefinition"
        },
        "outputData": {
          "type": "array",
          "items": {
            "$ref": "#/definitions/argumentDefinition"
          }
        }
      }
    },
    "dataTypeDefinition": {
      "enum": [
        "ARRAY",
        "STRUCT",
        "INT",
        "FLOAT",
        "DOUBLE",
        "TEXT",
        "DATE",
        "ENUM",
        "BOOL"
      ]
    },
    "dataSpecsDefinition": {
      "type": "object",
      "required": [
        "identifier",
        "isStd",
        "dataType",
        "childName",
        "name",
        "childDataType",
        "childSpecsDTO"
      ]
    }
  },
  "type": "object",
  "properties": {
    "productKey": {
      "type": "string"
    },
    "properties": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/propertyDefinition"
      }
    },
    "services": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/serviceDefinition"
      }
    },
    "events": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/eventDefinition"
      }
    }
  }
}
```


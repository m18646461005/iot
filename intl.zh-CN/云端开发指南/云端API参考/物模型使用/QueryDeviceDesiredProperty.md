# QueryDeviceDesiredProperty

调用该接口查询指定设备的期望属性值。

## 限制说明

-   只读属性不支持查询期望属性值。
-   一次调用最多能查询10个属性的期望值。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceDesiredProperty&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceDesiredProperty|系统规定参数。取值：QueryDeviceDesiredProperty。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|要查询的设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|light|要查询的设备名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|Identifier.N|RepeatList|否|Temperature|要查询期望值的属性的标识符（identifier）列表。

 设备的属性identifier，可在控制台中，设备所属产品的功能定义中查看。

 -   单次调用，最多能传入10个标识符。
-   不可输入重复的属性标识符。
-   若不传入此参数，将返回该设备所有属性的期望值。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的数据（**List**）。 |
|List|Array of DesiredPropertyInfo| |返回的期望属性信息（**DesiredPropertyInfo**）。 |
|DesiredPropertyInfo| | | |
|DataType|String|int|属性数据类型。 |
|Identifier|String|Temperature|属性标识符。 |
|Name|String|airconditioning|属性名称。 |
|Time|String|1579335899000|期望属性值的修改时间，单位是毫秒。 |
|Unit|String|℃|属性单位。 |
|Value|String|34|期望属性值。 |
|Version|Long|1|当前期望属性值的版本号。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceDesiredProperty
&IotId=SR8FiTu1R9tlUR2****0010300
&Identifier.1=Weight
&Identifier.2=Circle
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceDesiredPropertyResponse>
  <Data>
        <List>
              <DesiredPropertyInfo>
                    <Name>温度</Name>
                    <Value>35</Value>
                    <Time>1581778567154</Time>
                    <DataType>float</DataType>
                    <Version>1</Version>
                    <Identifier>Temperature</Identifier>
                    <Unit>°C</Unit>
              </DesiredPropertyInfo>
        </List>
  </Data>
  <RequestId>F0B1F7C8-A799-44C3-BDF8-1B8F9E91E675</RequestId>
  <Success>true</Success>
</QueryDeviceDesiredPropertyResponse>
```

`JSON` 格式

```
{
  "Data": {
    "List": {
      "DesiredPropertyInfo": [
        {
          "Name": "温度", 
          "Value": "35", 
          "Time": "1581778567154", 
          "DataType": "float", 
          "Version": 1, 
          "Identifier": "Temperature", 
          "Unit": "°C"
        }
      ]
    }
  }, 
  "RequestId": "F0B1F7C8-A799-44C3-BDF8-1B8F9E91E675", 
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


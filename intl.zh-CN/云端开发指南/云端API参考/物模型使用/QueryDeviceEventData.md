# QueryDeviceEventData

调用该接口查询指定设备的事件记录。

## 限制说明

-   仅能查询最近30天内的事件记录数据。

**说明：** 数据存储时间从事件生成当日起开始计算。

-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceEventData&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceEventData|系统规定参数。取值：QueryDeviceEventData。 |
|EndTime|Long|是|1516541900303|要查询的事件记录的结束时间。格式为毫秒级的13位时间戳，例如1516541900303。 |
|StartTime|Long|是|1516541900303|要查询的事件记录的开始时间。格式为毫秒级的13位时间戳，例如1516538300303。

 **说明：** 只能查询最近30天内的数据。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|PageSize|Integer|否|10|返回结果中每页显示的记录数。数量限制：每页最多可显示50条。默认值是10。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|要查询的设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|light|要查询的设备名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|Identifier|String|否|PowerOff|要查询的事件标识符。设备的事件Identifier，可在控制台中设备所属的产品的功能定义中查看；也可以调用[QueryThingModel](~~150321~~)，从返回的物模型信息中查看。 |
|EventType|String|否|info|要查询的事件类型。取值：

 -   **info**：信息。
-   **alert**：告警。
-   **error**：故障。 |
|Asc|Integer|否|0|返回结果中事件记录的排序方式，取值：

 -   **0**：倒序。
-   **1**：正序。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要查询的设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的设备事件记录。 |
|List|Array of EventInfo| |事件集合。每个元素代表一个事件。 |
|EventInfo| | | |
|EventType|String|info|事件类型。

 -   **info**：信息。
-   **alert**：告警。
-   **error**：故障。 |
|Identifier|String|PowerOff|事件标识符。 |
|Name|String|设备关机|事件名称。 |
|OutputData|String|\{"structArgs":\{"structchildFLOATf71c20e":1.23\}\}|事件的输出参数，map格式的字符串。 |
|Time|String|1579163099000|事件发生时间。毫秒级时间戳。 |
|NextTime|Long|1579163099000|下一页面中的事件记录的起始时间。毫秒级时间戳。

 调用本接口查询下一页事件记录时，该值可作为入参**StartTime**的值。 |
|NextValid|Boolean|true|是否有下一页事件记录。

 -   **true**：有。
-   **false**：没有。

 返回**NextValid**为**true**时，可以将**NextTime**的值作为下次查询的**StartTime**，继续查询本次查询不显示的数据。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceEventData
&IotId=abcdef1234567************
&ProductKey=al**********
&DeviceName=device1
&EventType=info
&Identifier=lightLevel
&StartTime=1516538300303L
&EndTime=1516541900303L
&PageSize=10
&Asc=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceEventDataResponse>
  <Data>
        <NextValid>false</NextValid>
        <NextTime>1579249151177</NextTime>
        <List>
              <EventInfo>
                    <Name>testEventInfoName</Name>
                    <Time>1516517974638</Time>
                    <OutputData>{"structArgs":{"structchildFLOATf71c20e":1.23,"structchildINT6b6b626":3,"structchildDATE663436a":"1516517966152","structchildDOUBLE08d0f74":1.23,"structchildTEXTdc764f9":"07b68264b0ba42c18e5f","structchildBOOLd260729":0,"structchildENUMbe62590":1},"enumArgs":0,"boolArgs":0,"floatArgs":2.3,"dateArgs":"1516517966152","intArgs":1,"doubleArgs":2.3,"textArgs":"dV56zbkzjBjw1Ti1dA52"}</OutputData>
                    <EventType>info</EventType>
                    <Identifier>testEventInfo</Identifier>
              </EventInfo>
        </List>
  </Data>
  <RequestId>45391E10-446B-4986-863E-1BA8CC44748F</RequestId>
  <Success>true</Success>
</QueryDeviceEventDataResponse>
```

`JSON` 格式

```
{
  "Data": {
    "NextValid": false, 
    "NextTime": 1579249151177, 
    "List": {
      "EventInfo": [
        {
          "Name": "testEventInfoName", 
          "Time": 1516517974638, 
          "OutputData": "{\"structArgs\":{\"structchildFLOATf71c20e\":1.23,\"structchildINT6b6b626\":3,\"structchildDATE663436a\":\"1516517966152\",\"structchildDOUBLE08d0f74\":1.23,\"structchildTEXTdc764f9\":\"07b68264b0ba42c18e5f\",\"structchildBOOLd260729\":0,\"structchildENUMbe62590\":1},\"enumArgs\":0,\"boolArgs\":0,\"floatArgs\":2.3,\"dateArgs\":\"1516517966152\",\"intArgs\":1,\"doubleArgs\":2.3,\"textArgs\":\"dV56zbkzjBjw1Ti1dA52\"}", 
          "EventType": "info", 
          "Identifier": "testEventInfo"
        }
      ]
    }
  }, 
  "RequestId": "45391E10-446B-4986-863E-1BA8CC44748F", 
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


# QueryDeviceServiceData

调用该接口查询指定设备的服务调用记录。

## 限制说明

-   仅能查询最近30天内的服务数据。

**说明：** 数据存储时间从调用服务当日开始计算。

-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享该阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceServiceData&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceServiceData|系统规定参数。取值：QueryDeviceServiceData。 |
|EndTime|Long|是|1579249499000|要查询的服务调用记录的结束时间。取值为毫秒值时间戳，例如1579249499000。 |
|StartTime|Long|是|1579249499000|要查询的服务调用记录的开始时间。取值为毫秒值时间戳，例如1579249499000。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要查询的设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|要查询的设备所隶属的产品**ProductKey**。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|light|要查询的设备名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|Identifier|String|否|Set|要查询的服务标识符。设备的服务Identifier。可在控制台中，设备所属的产品的功能定义中查看；或调用[QueryThingModel](~~150321~~)。 |
|Asc|Integer|否|0|返回结果中，服务调用记录按时间排序的方式。取值：

 -   **0**：倒序。
-   **1**：正序。 |
|PageSize|Integer|否|10|返回结果中每页显示的记录数。数量限制：每页最多可显示50条。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的设备服务调用记录。 |
|List|Array of ServiceInfo| |服务调用记录集合。每个元素代表一个服务执调用录。 |
|ServiceInfo| | | |
|Identifier|String|Set|服务标识符。 |
|InputData|String|\{\\"code\\":200,\\"data\\":\{\},\\"id\\":\\"100686\\",\\"message\\":\\"success\\",\\"version\\":\\"1.0\\"\}|服务的输入参数，MAP格式的字符串，结构为key:value。 |
|Name|String|设置温度|服务名称。 |
|OutputData|String|\{\\"LightAdjustLevel\\":123\}|服务的输出参数，MAP格式的字符串，结构为key:value。 |
|Time|String|1579249499000|调用服务的时间。 |
|NextTime|Long|1579335899000|下一页面中的服务调用记录的起始时间。

 调用本接口查询下一页服务调用记录时，该值可作为请求**StartTime**的值。 |
|NextValid|Boolean|true|是否有下一页服务调用记录。

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
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceServiceData
&ProductKey=a1BwAGV****
&DeviceName=device1
&Identifier=set
&StartTime=1516538300303
&EndTime=1516541900303
&PageSize=10
&Asc=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceServiceDataResponse>
  <Data>
        <NextValid>true</NextValid>
        <NextTime>1517315865197</NextTime>
        <List>
              <ServiceInfo>
                    <Name>set</Name>
                    <Time>1517315865198</Time>
                    <OutputData>{"code":200,"data":{},"id":"100686","message":"success","version":"1.0"}</OutputData>
                    <InputData>{"LightAdjustLevel":123}</InputData>
                    <Identifier>set</Identifier>
              </ServiceInfo>
        </List>
  </Data>
  <RequestId>A44C818E-FA7F-4765-B1E7-01D14AE01C6A</RequestId>
  <Success>true</Success>
</QueryDeviceServiceDataResponse>
```

`JSON` 格式

```
{
  "Data": {
    "NextValid": true, 
    "NextTime": 1517315865197, 
    "List": {
      "ServiceInfo": [
        {
          "Name": "set", 
          "Time": 1517315865198, 
          "OutputData": "{\"code\":200,\"data\":{},\"id\":\"100686\",\"message\":\"success\",\"version\":\"1.0\"}", 
          "InputData": "{\"LightAdjustLevel\":123}", 
          "Identifier": "set"
        }
      ]
    }
  }, 
  "RequestId": "A44C818E-FA7F-4765-B1E7-01D14AE01C6A", 
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


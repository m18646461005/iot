# QueryDevicePropertiesData

调用该接口批量查询指定设备的属性上报数据。

## 限制说明

-   一次调用最多可查询10个属性的历史数据。
-   每个属性最多返回100条数据。
-   仅能查询最近30天内的属性数据。

**说明：** 数据存储时间从属性生成当日开始计算。

-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDevicePropertiesData&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDevicePropertiesData|系统规定参数。取值：QueryDevicePropertiesData。 |
|Asc|Integer|是|0|返回结果中，属性记录按时间排序的方式。取值：

 -   **0**：倒序。倒序查询时，**StartTime**必须大于**EndTime**。
-   **1**：正序。正序查询时，**StartTime**必须小于**EndTime**。 |
|DeviceName|String|是|airconditioning|要查询的设备名称。 |
|EndTime|Long|是|1579249499000|属性记录的结束时间。取值为13位毫秒值时间戳，例如1579249499000。 |
|Identifier.N|RepeatList|是|temperature|属性的标识符列表。

 不可输入重复的属性Identifier。

 设备的属性Identifier信息，可在控制台中，设备所属的产品的功能定义中查看；或调用[QueryThingModel](~~150321~~)，从返回的物模型信息中查看。 |
|PageSize|Integer|是|10|单个属性可返回的数据记录数量。最大值为100。

 任意一个属性返回的数据记录数量不超过该值。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|要查询设备所属的产品ProductKey。 |
|StartTime|Long|是|1579249499000|属性记录的开始时间。取值为13位毫秒值时间戳，例如1579249499000。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要查询的设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** **IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|NextTime|Long|1579249499000|下一页属性记录的起始时间。

 可以将**NextTime**的值作为下次查询的**StartTime**，继续查询本次查询不显示的数据。 |
|NextValid|Boolean|true|是否有下一页属性记录。

 -   **true**：有。
-   **false**：没有。

 返回**NextValid**为**true**时，可以将**NextTime**的值作为下次查询的**StartTime**，继续查询本次查询不显示的数据。 |
|PropertyDataInfos|Array of PropertyDataInfo| |调用成功时，返回的属性信息列表（**PropertyDataInfo**）。 |
|PropertyDataInfo| | | |
|Identifier|String|temperature|属性的标识符。 |
|List|Array of PropertyInfo| |属性数据列表。 |
|PropertyInfo| | | |
|Time|Long|1579249499000|属性上报时间。取值为毫秒值时间戳，例如1579249499000。 |
|Value|String|21.3|属性值。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDevicePropertiesData
&Asc=0
&DeviceName=water
&EndTime=1540115948152
&Identifier.1=Temperature
&Identifier.2=Humidity
&PageSize=100
&ProductKey=a1bdOxkDbGC
&StartTime=1540116010723
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDevicePropertiesData>
  <NextValid>false</NextValid>
  <RequestId>CC4CAC00-ED4C-4004-9E8D-E8B4A78552FA</RequestId>
  <PropertyDataInfos>
        <PropertyDataInfo>
              <List>
                    <PropertyInfo>
                          <Value>32.46</Value>
                          <Time>1579249151178</Time>
                    </PropertyInfo>
              </List>
              <Identifier>Temperature</Identifier>
        </PropertyDataInfo>
        <PropertyDataInfo>
              <List>
                    <PropertyInfo>
                          <Value>48</Value>
                          <Time>1579249151178</Time>
                    </PropertyInfo>
              </List>
              <Identifier>Humidity</Identifier>
        </PropertyDataInfo>
  </PropertyDataInfos>
  <Success>true</Success>
</QueryDevicePropertiesData>
```

`JSON` 格式

```
{
  "NextValid": false, 
  "RequestId": "CC4CAC00-ED4C-4004-9E8D-E8B4A78552FA", 
  "PropertyDataInfos": {
    "PropertyDataInfo": [
      {
        "List": {
          "PropertyInfo": [
            {
              "Value": "32.46", 
              "Time": 1579249151178
            }
          ]
        }, 
        "Identifier": "Temperature"
      }, 
      {
        "List": {
          "PropertyInfo": [
            {
              "Value": "48", 
              "Time": 1579249151178
            }
          ]
        }, 
        "Identifier": "Humidity"
      }
    ]
  }, 
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


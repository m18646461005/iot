# QueryDevicePropertyStatus

调用该接口查询指定设备的属性快照。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为200。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDevicePropertyStatus&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDevicePropertyStatus|系统规定参数。取值：QueryDevicePropertyStatus。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要查询的设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|要查询的设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|light|要查询的设备名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的数据，详情请参见**List**包含的参数。 |
|List|Array of PropertyStatusInfo| |返回的属性集合信息（**PropertyStatusInfo**）。 |
|PropertyStatusInfo| | | |
|DataType|String|int|属性格式类型，取值：

 -   **int**：整型。
-   **float**：单精度浮点型。
-   **double**：双精度浮点型。
-   **enum**：枚举型。
-   **bool**：布尔型。
-   **text**：字符型。
-   **date**：时间型（String类型的UTC时间戳，单位是毫秒）。
-   **array**：数组型。
-   **struct**：结构体类型。 |
|Identifier|String|Temperture|属性标识符。 |
|Name|String|temperature|属性名称。 |
|Time|String|1517553572362|属性修改的时间，单位是毫秒。 |
|Unit|String|°C|属性值的单位。 |
|Value|String|25|属性值。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDevicePropertyStatus
&ProductKey=a1rYuVF****
&DeviceName=device1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDevicePropertyStatusResponse>
  <Data>
        <List>
              <PropertyStatusInfo>
                    <Name>湿度</Name>
                    <Value>48</Value>
                    <Time>1579249151178</Time>
                    <DataType>int</DataType>
                    <Identifier>Humidity</Identifier>
                    <Unit>%</Unit>
              </PropertyStatusInfo>
              <PropertyStatusInfo>
                    <Name>温度</Name>
                    <Value>32.46</Value>
                    <Time>1579249151178</Time>
                    <DataType>float</DataType>
                    <Identifier>Temperature</Identifier>
                    <Unit>°C</Unit>
              </PropertyStatusInfo>
        </List>
  </Data>
  <RequestId>84BAD25B-9879-4BA1-9213-F576C6558D77</RequestId>
  <Success>true</Success>
</QueryDevicePropertyStatusResponse>
```

`JSON` 格式

```
{
	"Data": {
		"List": {
			"PropertyStatusInfo": [
				{
					"Name": "湿度",
					"Value": "48",
					"Time": "1579249151178",
					"DataType": "int",
					"Identifier": "Humidity",
					"Unit": "%"
				},
				{
					"Name": "温度",
					"Value": "32.46",
					"Time": "1579249151178",
					"DataType": "float",
					"Identifier": "Temperature",
					"Unit": "°C"
				}
			]
		}
	},
	"RequestId": "84BAD25B-9879-4BA1-9213-F576C6558D77",
	"Success": true
}
```


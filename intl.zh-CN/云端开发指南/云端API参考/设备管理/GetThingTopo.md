# GetThingTopo

调用该接口查询指定设备的拓扑关系。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=GetThingTopo&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetThingTopo|系统规定参数。取值：GetThingTopo。 |
|PageNo|Integer|是|1|从返回结果中的第几页开始显示。 |
|PageSize|Integer|是|10|返回结果中每页显示的记录数量。数量限制：每页最多可显示50条记录。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|要查询的设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|light|要查询的设备的名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要查询的设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的数据。详情请参见以下参数。 |
|CurrentPage|Integer|1|当前页面号。 |
|List|Array of deviceInfo| |设备信息集合（**deviceInfo**）。 |
|deviceInfo| | | |
|DeviceName|String|light|设备名称。 |
|IotId|String|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。 |
|ProductKey|String|a1BwAGV\*\*\*\*|设备所隶属的产品ProductKey。 |
|PageCount|Long|1|总页数。 |
|PageSize|Integer|10|每页显示的记录数。 |
|Total|Long|1|总记录数。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=GetThingTopo
&ProductKey=a1BwAGV****
&DeviceName=device1
&PageSize=10
&PageNo=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetThingTopoResponse>
  <Data>
        <PageCount>1</PageCount>
        <PageSize>2</PageSize>
        <CurrentPage>1</CurrentPage>
        <List>
              <deviceInfo>
                    <DeviceName>APItest</DeviceName>
                    <ProductKey>a1T27vz****</ProductKey>
                    <IotId>vWxNur6BUApsqjv****000100</IotId>
              </deviceInfo>
        </List>
        <Total>1</Total>
  </Data>
  <RequestId>93F05C63-9FD1-4CC8-B0FF-6D6C1A6632D1</RequestId>
  <Success>true</Success>
</GetThingTopoResponse>
```

`JSON` 格式

```
{
	"Data": {
		"PageCount": 1,
		"PageSize": 2,
		"CurrentPage": 1,
		"List": {
			"deviceInfo": [
				{
					"DeviceName": "APItest",
					"ProductKey": "a1T27vz****",
					"IotId": "vWxNur6BUApsqjv****000100"
				}
			]
		},
		"Total": 1
	},
	"RequestId": "93F05C63-9FD1-4CC8-B0FF-6D6C1A6632D1",
	"Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


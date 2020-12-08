# GetGatewayBySubDevice

调用该接口，根据挂载的子设备信息，查询对应的网关设备信息。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享该阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=GetGatewayBySubDevice&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetGatewayBySubDevice|系统规定参数。取值：GetGatewayBySubDevice。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|子设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|light|子设备名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|子设备ID。物联网平台为该子设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的网关设备的详细信息。 |
|DeviceName|String|gateway|网关设备名称。 |
|DeviceSecret|String|dCYdTU3gw5Z77bsHjPk6lPHPVnBT\*\*\*\*|网关设备密钥。 |
|FirmwareVersion|String|V1.0.1|网关设备的固件版本号。 |
|GmtActive|String|2019-12-18 23:25:30|网关设备的激活时间，GMT格式，是用户所在地的当地时间。 |
|GmtCreate|String|2019-12-18 16:58:33|网关设备的创建时间，GMT格式，是用户所在地的当地时间。 |
|GmtOnline|String|2020-01-20 17:41:04|网关设备最近一次上线的时间，GMT格式，是用户所在地的当地时间。 |
|IpAddress|String|106.\*\*.1\*\*.\*\*|网关设备的IP地址。 |
|NodeType|String|1|节点类型，取值为1，表示该设备为网关设备。 |
|ProductKey|String|a1BwAGV\*\*\*\*|网关设备隶属的产品**ProductKey**。 |
|ProductName|String|LinkIoT|网关设备隶属的产品名称。 |
|Status|String|online|网关设备状态。取值：

 -   **online**：设备在线。
-   **offline**：设备离线。
-   **unactive**：设备未激活。
-   **disable**：设备已禁用 |
|UtcActive|String|2019-12-18T15:25:30.176Z|网关设备的激活时间，UTC格式，世界标准时间。用户所在地实际时间，可根据当地时差计算。 |
|UtcCreate|String|2019-12-18T08:58:33.000Z|网关设备的创建时间，UTC格式，世界标准时间。用户所在地实际时间，可根据当地时差计算。 |
|UtcOnline|String|2020-01-20T09:41:04.879Z|网关设备最近一次上线的时间，UTC格式，世界标准时间。用户所在地实际时间，可根据当地时差计算。 |
|iotId|String|WuyjPSDQE1L22z1d\*\*\*\*000100|物联网平台为该网关设备颁发的ID，作为该设备的唯一标识符。 |
|region|String|cn-shanghai|网关设备所在地域（与控制台上的地域对应）。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=GetGatewayBySubDevice
&ProductKey=a1BwAGV****
&DeviceName=XTzosqEOgxFXKPRgd8zl
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetGatewayBySubDeviceResponse>
  <Data>
        <region>cn-shanghai</region>
        <DeviceName>gateway_04</DeviceName>
        <GmtActive>2019-12-18 23:25:30</GmtActive>
        <ProductKey>a1vL7cp****</ProductKey>
        <IpAddress>106.**.1**.**</IpAddress>
        <GmtCreate>2019-12-18 16:58:33</GmtCreate>
        <UtcCreate>2019-12-18T08:58:33.000Z</UtcCreate>
        <UtcOnline>2020-01-20T09:41:04.879Z</UtcOnline>
        <UtcActive>2019-12-18T15:25:30.176Z</UtcActive>
        <Status>online</Status>
        <NodeType>1</NodeType>
        <GmtOnline>2020-01-20 17:41:04</GmtOnline>
        <ProductName>LinkIoTEdge_Gateway</ProductName>
        <iotId>WuyjPSDQE1L22z1****000100</iotId>
  </Data>
  <RequestId>0377D5A9-BDE1-48C2-96C9-BDC048899186</RequestId>
  <Success>true</Success>
</GetGatewayBySubDeviceResponse>
```

`JSON` 格式

```
{
	"Data": {
		"region": "cn-shanghai",
		"DeviceName": "gateway_04",
		"GmtActive": "2019-12-18 23:25:30",
		"ProductKey": "a1vL7cp****",
		"IpAddress": "106.**.1**.**",
		"GmtCreate": "2019-12-18 16:58:33",
		"UtcCreate": "2019-12-18T08:58:33.000Z",
		"UtcOnline": "2020-01-20T09:41:04.879Z",
		"UtcActive": "2019-12-18T15:25:30.176Z",
        "Status": "online",
		"NodeType": 1,
		"GmtOnline": "2020-01-20 17:41:04",
		"ProductName": "LinkIoTEdge_Gateway",
		"iotId": "WuyjPSDQE1L22z1****000100"
	},
	"RequestId": "0377D5A9-BDE1-48C2-96C9-BDC048899186",
	"Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


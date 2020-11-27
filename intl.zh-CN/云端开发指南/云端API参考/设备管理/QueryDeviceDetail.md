# QueryDeviceDetail

调用该接口查询指定设备的详细信息。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceDetail&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceDetail|系统规定参数。取值：QueryDeviceDetail。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|要查询的设备所隶属的产品Key。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|light|指定要查询的设备的名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要查询的设备ID。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回设备的详细信息。 |
|DeviceName|String|light|设备名称。 |
|DeviceSecret|String|mz2Canp4GB7qRVf1OYPNtRqB2anu\*\*\*\*|设备密钥。 |
|FirmwareVersion|String|V1.0.0.0|设备的固件版本号。 |
|GmtActive|String|2018-08-06 10:48:41|设备的激活时间，GMT格式。 |
|GmtCreate|String|2018-08-06 10:47:50|设备的创建时间，GMT格式。 |
|GmtOnline|String|2018-08-06 13:43:12|设备最近一次上线的时间，GMT格式。 |
|IotId|String|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|物联网平台为该设备颁发的ID，作为该设备的唯一标识符。 |
|IpAddress|String|10.0.0.1|设备的IP地址。 |
|Nickname|String|detectors\_in\_beijing|设备的备注名称。 |
|NodeType|Integer|0|节点类型，取值：

 -   **0**：设备。设备不能挂载子设备。可以直连物联网平台，也可以作为网关的子设备连接物联网平台。
-   **1**：网关。网关可以挂载子设备，具有子设备管理模块，维持子设备的拓扑关系，和将拓扑关系同步到物联网平台。 |
|Owner|Boolean|true|API调用者是否是该设备的拥有者。 |
|ProductKey|String|a1rYuVF\*\*\*\*|设备所属产品的ProductKey。 |
|ProductName|String|test|设备所属产品的名称。 |
|Region|String|cn-shanghai|设备所在地区（与控制台上的物联网地平台服务地域对应）。 |
|Status|String|ONLINE|设备状态。取值：

 -   **ONLINE**：设备在线。
-   **OFFLINE**：设备离线。
-   **UNACTIVE**：设备未激活。
-   **DISABLE**：设备已禁用。 |
|UtcActive|String|2018-08-06T02:48:41.000Z|设备的激活时间，UTC格式。 |
|UtcCreate|String|2018-08-06T02:47:50.000Z|设备的创建时间，UTC格式。 |
|UtcOnline|String|2018-08-06T05:43:12.000Z|设备最近一次上线的时间，UTC格式。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceDetail
&ProductKey=a1rYuVF****
&DeviceName=device1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceDetailResponse>
  <Data>
        <Owner>true</Owner>
        <GmtActive>2020-01-16 13:33:37</GmtActive>
        <DeviceName>Humidity</DeviceName>
        <ProductKey>a1ttsqu****</ProductKey>
        <DeviceSecret>sLefbFmN9SYfnWLJTePG893XNuRV****</DeviceSecret>
        <IpAddress>42.120.75.144</IpAddress>
        <GmtCreate>2020-01-08 14:47:08</GmtCreate>
        <UtcCreate>2020-01-08T06:47:08.000Z</UtcCreate>
        <IotId>dwnS41bhNxjslDAIF****00100</IotId>
        <Status>OFFLINE</Status>
        <UtcOnline>2020-01-17T08:19:11.091Z</UtcOnline>
        <Region>cn-shanghai</Region>
        <UtcActive>2020-01-16T05:33:37.830Z</UtcActive>
        <Nickname>温湿度</Nickname>
        <NodeType>0</NodeType>
        <GmtOnline>2020-01-17 16:19:11</GmtOnline>
        <ProductName>光照温湿度传感器</ProductName>
  </Data>
  <RequestId>D2D2DE90-DD0F-44EA-9F56-63F07A59F65B</RequestId>
  <Success>true</Success>
</QueryDeviceDetailResponse>
```

`JSON` 格式

```
{
	"Data": {
		"Owner": true,
		"GmtActive": "2020-01-16 13:33:37",
		"DeviceName": "Humidity",
		"ProductKey": "a1ttsqu****",
		"DeviceSecret": "sLefbFmN9SYfnWLJTePG893XNuRV****",
		"IpAddress": "42.120.75.144",
		"GmtCreate": "2020-01-08 14:47:08",
		"UtcCreate": "2020-01-08T06:47:08.000Z",
		"IotId": "dwnS41bhNxjslDAIF****00100",
		"Status": "OFFLINE",
		"UtcOnline": "2020-01-17T08:19:11.091Z",
		"Region": "cn-shanghai",
		"UtcActive": "2020-01-16T05:33:37.830Z",
		"Nickname": "温湿度",
		"NodeType": 0,
		"GmtOnline": "2020-01-17 16:19:11",
		"ProductName": "光照温湿度传感器"
	},
	"RequestId": "D2D2DE90-DD0F-44EA-9F56-63F07A59F65B",
	"Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


# BatchQueryDeviceDetail

调用该接口批量查询设备详情。

## 限制说明

-   单次调用最多能查询100个设备。
-   只能批量查询当前阿里云账号下的设备详情。如果传入的设备信息中，有设备不属于当前账号，则直接返回失败结果。
-   若传入的设备信息中，包含不存在的设备，则只返回存在的设备详情。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchQueryDeviceDetail&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchQueryDeviceDetail|系统规定参数。取值：BatchQueryDeviceDetail。 |
|DeviceName.N|RepeatList|是|light|要查询的设备名称列表。最多可包含100个设备名称。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|设备所隶属的产品ProductKey。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Array of Data| |调用成功时，返回设备的详细信息。 |
|Data| | | |
|DeviceName|String|light|设备名称。 |
|DeviceSecret|String|mz2Canp4GB7qRVf1OYPNtRqB2anu\*\*\*\*|设备密钥。 |
|FirmwareVersion|String|V1.0.0.0|设备的固件版本号。 |
|GmtActive|String|2019-06-21 20:33:00|设备的激活时间，GMT格式。 |
|GmtCreate|String|2019-06-21 20:31:42|设备的创建时间，GMT格式。 |
|IotId|String|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|物联网平台为该设备颁发的ID，设备的唯一标识符。 |
|Nickname|String|智能路灯|设备的备注名称。 |
|NodeType|Integer|0|节点类型，取值：

 -   **0**：设备。设备不能挂载子设备。可以直连物联网平台，也可以作为网关的子设备连接物联网平台。
-   **1**：网关。网关可以挂载子设备，具有子设备管理模块，维持子设备的拓扑关系，和将拓扑关系同步到物联网平台。 |
|ProductKey|String|a1BwAGV\*\*\*\*|设备所隶属的产品ProductKey |
|ProductName|String|路灯产品|设备所隶属的产品名称。 |
|Region|String|cn-shanghai|设备所在地域（与控制台上物联网平台服务地域对应）。 |
|Status|String|ONLINE|设备状态。取值：

 -   **ONLINE**：设备在线。
-   **OFFLINE**：设备离线。
-   **UNACTIVE**：设备未激活。
-   **DISABLE**：设备已禁用。 |
|UtcActive|String|2019-06-21T12:31:42.000Z|​设备的激活时间，UTC格式。 |
|UtcCreate|String|2019-06-21T12:31:42.000Z|​设备的创建时间，UTC格式。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=BatchQueryDeviceDetail
&ProductKey=a1fce6J****
&DeviceName.1=firstDeviceName
&DeviceName.2=secondDeviceName
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchQueryDeviceDetailResponse>
  <Data>
        <Data>
              <DeviceName>Humidity</DeviceName>
              <GmtActive>2020-01-16 13:33:37</GmtActive>
              <ProductKey>a1ttsqu****</ProductKey>
              <DeviceSecret>sLefbFmN9SYfnWLJTePG893XNuRV****</DeviceSecret>
              <GmtCreate>2020-01-08 14:47:08</GmtCreate>
              <UtcCreate>2020-01-08T06:47:08.000Z</UtcCreate>
              <IotId>dwnS41bhNxjslDAIF****00100</IotId>
              <Status>OFFLINE</Status>
              <UtcActive>2020-01-08T06:47:08.000Z</UtcActive>
              <Region>cn-shanghai</Region>
              <Nickname>温湿度</Nickname>
              <NodeType>0</NodeType>
              <ProductName>光照温湿度传感器</ProductName>
        </Data>
        <Data>
              <Status>OFFLINE</Status>
              <GmtActive>2020-01-17 16:23:15</GmtActive>
              <DeviceName>TH_sensor</DeviceName>
              <Region>cn-shanghai</Region>
              <UtcActive>2020-01-17T03:39:14.000Z</UtcActive>
              <ProductKey>a1ttsqu****</ProductKey>
              <NodeType>0</NodeType>
              <DeviceSecret>dCYdTU3gw5Z77bsHjPk6lPHPVnBT****</DeviceSecret>
              <ProductName>光照温湿度传感器</ProductName>
              <GmtCreate>2020-01-17 11:39:14</GmtCreate>
              <UtcCreate>2020-01-17T03:39:14.000Z</UtcCreate>
              <IotId>RKYkCRstfGBh5SZXL****00100</IotId>
        </Data>
  </Data>
  <RequestId>D4C12DD8-4390-4877-B1DC-4049CF4868BC</RequestId>
  <Success>true</Success>
</BatchQueryDeviceDetailResponse>
```

`JSON` 格式

```
{
	"Data": {
		"Data": [
			{
				"DeviceName": "Humidity",
				"GmtActive": "2020-01-16 13:33:37",
				"ProductKey": "a1ttsqu****",
				"DeviceSecret": "sLefbFmN9SYfnWLJTePG893XNuRV****",
				"GmtCreate": "2020-01-08 14:47:08",
				"UtcCreate": "2020-01-08T06:47:08.000Z",
				"IotId": "dwnS41bhNxjslDAIF****00100",
				"Status": "OFFLINE",
				"UtcActive": "2020-01-08T06:47:08.000Z",
				"Region": "cn-shanghai",
				"Nickname": "温湿度",
				"NodeType": 0,
				"ProductName": "光照温湿度传感器"
			},
			{
				"Status": "OFFLINE",
				"GmtActive": "2020-01-17 16:23:15",
				"DeviceName": "TH_sensor",
				"Region": "cn-shanghai",
				"UtcActive": "2020-01-17T03:39:14.000Z",
				"ProductKey": "a1ttsqu****",
				"NodeType": 0,
				"DeviceSecret": "dCYdTU3gw5Z77bsHjPk6lPHPVnBT****",
				"ProductName": "光照温湿度传感器",
				"GmtCreate": "2020-01-17 11:39:14",
				"UtcCreate": "2020-01-17T03:39:14.000Z",
				"IotId": "RKYkCRstfGBh5SZXL****00100"
			}
		]
	},
	"RequestId": "D4C12DD8-4390-4877-B1DC-4049CF4868BC",
	"Success": true
}
```


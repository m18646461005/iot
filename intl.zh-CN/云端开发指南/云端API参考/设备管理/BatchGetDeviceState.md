# BatchGetDeviceState

调用该接口批量查看同一产品下指定设备的运行状态。

## 限制说明

-   该接口用于查看一个产品下多个设备的运行状态，单次最多可查询50个设备。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchGetDeviceState&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchGetDeviceState|系统规定参数。取值：BatchGetDeviceState。 |
|DeviceName.N|RepeatList|否|light|要查看运行状态的设备的名称列表。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|要查看运行状态的设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|IotId.N|RepeatList|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要查看运行状态的设备ID列表。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|DeviceStatusList|Array of DeviceStatus| |调用成功时，返回设备状态信息列表，请参见DeviceStatus包含的以下参数。 |
|DeviceStatus| | | |
|AsAddress|String|42.12\*.7\*.1\*\*|设备IP地址。 |
|DeviceId|String|dwnS41bhNxjslDAI\*\*\*\*|设备ID（旧版参数）。

 **说明：** 该参数是旧版本遗留参数，已无实际作用，不能用来标识设备。目前，有效的设备标识符为**IotId**和**ProductKey**与**DeviceName**组合。 |
|DeviceName|String|light|设备名称。 |
|IotId|String|dwnS41bhNxjslDAI\*\*\*\*000100|设备ID，物联网平台为设备颁发的唯一标识。 |
|LastOnlineTime|String|2020-01-17 16:19:11|设备最后一次上线的时间。 |
|Status|String|OFFLINE|设备状态。取值：

 -   **ONLINE**：设备在线。
-   **OFFLINE**：设备离线。
-   **UNACTIVE**：设备未激活。
-   **DISABLE**：设备已禁用。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=BatchGetDeviceState
&productKey=a1BwAGV****
&DeviceName.1=device1
&DeviceName.2=device2
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchGetDeviceStateResponse>
  <DeviceStatusList>
        <DeviceStatus>
              <Status>OFFLINE</Status>
              <DeviceId>dwnS41bhNxjslDAI****</DeviceId>
              <DeviceName>Humidity</DeviceName>
              <AsAddress>42.1**.7*.1**</AsAddress>
              <LastOnlineTime>2020-01-17 16:19:11</LastOnlineTime>
              <IotId>dwnS41bhNxjslDAI****000100</IotId>
        </DeviceStatus>
  </DeviceStatusList>
  <RequestId>3258D872-EDC5-4039-B564-C27ED7176741</RequestId>
  <Success>true</Success>
</BatchGetDeviceStateResponse>
```

`JSON` 格式

```
{
	"DeviceStatusList": {
		"DeviceStatus": [
			{
				"Status": "OFFLINE",
				"DeviceId": "dwnS41bhNxjslDAI****",
				"DeviceName": "Humidity",
				"AsAddress": "42.1**.7*.1**",
				"LastOnlineTime": "2020-01-17 16:19:11",
				"IotId": "dwnS41bhNxjslDAI****000100"
			}
		]
	},
	"RequestId": "3258D872-EDC5-4039-B564-C27ED7176741",
	"Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


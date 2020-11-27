# UpdateDeviceShadow

调用该接口修改指定设备的影子信息。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=UpdateDeviceShadow&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateDeviceShadow|系统规定参数。取值：UpdateDeviceShadow。 |
|DeviceName|String|是|device1|要修改影子信息的设备名称。 |
|ProductKey|String|是|a1T27vz\*\*\*\*|要修改影子信息的设备所隶属的产品ProductKey。 |
|ShadowMessage|String|是|\{"method":"update","state":\{"desired":\{"color":"green"\}\},"version":2\}|修改后的设备影子信息。

 影子信息参数中包含：

 -   **method**：String，指定操作类型，取值：**update**。
-   **state**：String，发送给影子的具体状态，由**desired**参数表示期望的影子状态。
-   **version**：Long，设备影子的版本，必须大于当前影子版本。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|DeltaUpdate|Boolean|否|false|是否增量更新设备影子**desired**参数。

 -   true：增量更新。
-   false：全量更新。

 默认值为false。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|6754C0E7-A35D-4CC8-A684-45EB1F0008D9|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=UpdateDeviceShadow
&ProductKey=a1T27vz****
&DeviceName=device1
&ShadowMessage={"method":"update","state":{"desired":{"color":"green"}},"version":1}
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UpdateDeviceShadowResponse>
        <RequestId>BB71E443-4447-4024-A000-EDE09922891E</RequestId>
        <Success>true</Success>
  </UpdateDeviceShadowResponse>
```

`JSON` 格式

```
{
	"RequestId": "6754C0E7-A35D-4CC8-A684-45EB1F0008D9",
	"Success": true
}
```


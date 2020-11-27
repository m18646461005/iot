# GetDeviceShadow

调用该接口查询指定设备的影子信息。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=GetDeviceShadow&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetDeviceShadow|系统规定参数。取值：GetDeviceShadow。 |
|DeviceName|String|是|device1|要查询的设备名称。 |
|ProductKey|String|是|a1T27vz\*\*\*\*|要查询的设备所隶属的产品ProductKey。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|A56E345A-0978-4993-ACBA-3EF444ED187F|阿里云为该请求生成的唯一标识符。 |
|ShadowMessage|String|\{"method":"update","state":\{"desired":\{"color":"green"\}\},"version":1\}|调用成功时，返回的设备影子信息。

 **说明：** 根据影子设备的不同状态，查询到的影子信息结构有所差别，详情请参考[设备影子开发](~~53930~~)。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=GetDeviceShadow
&ProductKey=a1T27vz****
&DeviceName=device1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetDeviceShadowResponse>
        <RequestId>BB71E443-4447-4024-A000-EDE09922891E</RequestId>
        <Success>true</Success>
        <ShadowMessage>{"method":"update","state":{"desired":{"color":"green"},"reported":"\"},"version":1}</ShadowMessage>
  </GetDeviceShadowResponse>
```

`JSON` 格式

```
{
	"ShadowMessage": {"method":"update","state":{"desired":{"color":"green"}},"version":1},
	"RequestId": "A56E345A-0978-4993-ACBA-3EF444ED187F",
	"Success": true
}
```


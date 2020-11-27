# BatchRegisterDevice

调用该接口在指定产品下批量注册多个设备（随机生成设备名）。

## 批量注册设备方式说明

批量注册设备有两种方式：

-   由系统随机生成设备名称：调用本接口。

    建议按照以下流程注册设备和查看结果。

    1. 调用本接口批量注册设备。返回成功结果，表示批量注册的申请已经提交成功。实际的注册是异步执行，会有一个过程。

    2. 调用[QueryBatchRegisterDeviceStatus](~~69483~~)查看设备注册结果。

    3. 调用[QueryPageByApplyId](~~69518~~)查看批量注册的设备信息（DeviceName、DeviceSecret、IotId）。

-   自定义设备名称：请参见[BatchRegisterDeviceWithApplyId](~~69514~~)。

## 限制说明

-   单次调用，最多可创建1,000 个设备。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchRegisterDevice&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchRegisterDevice|系统规定参数。取值：BatchRegisterDevice。 |
|Count|Integer|是|100|要注册的设备数量，取值不能大于1,000。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|要批量注册的设备所隶属的产品ProductKey。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|ApplyId|Long|1295006|调用成功时，系统返回的申请批次ID。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=BatchRegisterDevice
&ProductKey=a1BwAGV****
&Count=10
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchRegisterDeviceResponse>
  <Data>
        <ApplyId>12345678</ApplyId>
  </Data>
  <RequestId>92C67DC1-41B5-45F8-9AFD-1FB42448D405</RequestId>
  <Success>true</Success>
</BatchRegisterDeviceResponse>
```

`JSON` 格式

```
{
	"Data": {
		"ApplyId": 12345678
	},
	"RequestId": "92C67DC1-41B5-45F8-9AFD-1FB42448D405",
	"Success": true
}
```


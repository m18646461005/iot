# BatchRegisterDeviceWithApplyId

调用该接口根据申请批次ID（ApplyId）批量注册设备。

## 使用说明

批量注册设备有两种方式：

-   由系统随机生成设备名称：请调用[BatchRegisterDevice](~~69473~~)接口。
-   自定义设备名称：需本接口与**BatchCheckDeviceNames**等接口结合实现。

请按以下流程操作。

1. 调用[BatchCheckDeviceNames](~~69482~~)接口，传入要批量注册的设备的名称。物联网平台检查您提交的设备名称符合要求后，返回申请批次ID（**ApplyId**）。**ApplyId**将用于设备名称设置结果查询、批量设备注册和设备信息查询。

2. 调用[QueryBatchRegisterDeviceStatus](~~69483~~)查看名称设置结果。

3. 调用本接口批量注册设备。本接口调用返回的成功结果，仅表示批量注册的申请已经提交成功。实际的注册会有一个过程。

4. （可选）调用[QueryBatchRegisterDeviceStatus](~~69483~~)查看设备注册结果。

5. 调用[QueryPageByApplyId](~~69518~~)查看批量注册的设备信息。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchRegisterDeviceWithApplyId&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchRegisterDeviceWithApplyId|系统规定参数。取值：BatchRegisterDeviceWithApplyId。 |
|ApplyId|Long|是|1295006|要批量注册的设备的申请批次ID。申请批次ID由调用[BatchCheckDeviceNames](~~69482~~)接口生成。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|要批量注册的设备所隶属的产品ProductKey。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的数据，详情请参见以下参数。 |
|ApplyId|Long|1295006|申请批次ID。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=BatchRegisterDeviceWithApplyId
&ProductKey=alNdd3i****
&ApplyId=1234567
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchRegisterDeviceWithApplyIdResponse>
  <Data>
        <ApplyId>1234567</ApplyId>
  </Data>
  <RequestId>82C16DC1-41B5-45F8-9AFD-1FB42448D405</RequestId>
  <Success>true</Success>
</BatchRegisterDeviceWithApplyIdResponse>
```

`JSON` 格式

```
{
	"Data": {
		"ApplyId": 1234567
	},
	"RequestId": "82C16DC1-41B5-45F8-9AFD-1FB42448D405",
	"Success": true
}
```


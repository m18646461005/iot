# CancelOTAStrategyByJob

调用该接口取消动态升级策略。

## 限制说明

-   只支持取消动态升级批次所关联的动态升级策略。该接口对静态升级批次无效。

    该接口执行成功后，会将动态升级批次的状态（**JobStatus**）设置为已取消（CANCELED）。

-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CancelOTAStrategyByJob&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CancelOTAStrategyByJob|系统规定参数。取值：CancelOTAStrategyByJob。 |
|JobId|String|是|HvKuBpuk3rdk6E92CP\*\*\*\*0200|升级批次ID。

 您调用[CreateOTADynamicUpgradeJob](~~147887~~)创建批次返回的**JobId**。您也可以在物联网平台控制台固件的**固件详情**页查看。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|291438BA-6E10-4C4C-B761-243B9A0D324F|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=CancelOTAStrategyByJob
&JobId=HvKuBpuk3rdk6E92CP****0200
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CancelOTAStrategyByJobResponse>
    <RequestId>A01829CE-75A1-4920-B775-921146A1AB79</RequestId>
    <Success>true</Success>
</CancelOTAStrategyByJobResponse>
```

`JSON` 格式

```
{
  "RequestId": "291438BA-6E10-4C4C-B761-243B9A0D324F",
  "Success": true
}
```


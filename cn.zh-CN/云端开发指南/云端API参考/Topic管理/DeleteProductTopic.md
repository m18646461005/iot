# DeleteProductTopic

调用该接口删除指定的自定义Topic类。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=DeleteProductTopic&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteProductTopic|系统规定参数。取值：DeleteProductTopic。 |
|TopicId|String|是|798\*\*\*\*|要删除的Topic类的ID。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|FCC27691-9151-4B93-9622-9C90F30542EC|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=DeleteProductTopic
&TopicId=798****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteProductTopicResponse>
      <RequestId>FCC27691-9151-4B93-9622-9C90F30542EC</RequestId>
      <Success>true</Success>
</DeleteProductTopicResponse>
```

`JSON` 格式

```
{
    "RequestId":"FCC27691-9151-4B93-9622-9C90F30542EC",
    "Success":true
}
```


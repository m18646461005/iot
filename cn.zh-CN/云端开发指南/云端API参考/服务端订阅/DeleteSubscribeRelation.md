# DeleteSubscribeRelation

调用该接口删除MNS或AMQP服务端订阅。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=DeleteSubscribeRelation&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteSubscribeRelation|系统规定参数。取值：DeleteSubscribeRelation。 |
|ProductKey|String|是|a1fyXVF\*\*\*\*|该订阅中的产品的ProductKey。 |
|Type|String|是|AMQP|订阅类型。取值：

 -   **MNS**
-   **AMQP** |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=DeleteSubscribeRelation
&ProductKey=a1Zkii7****
&Type=AMQP
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteSubscribeRelationResponse>
       <RequestId>73B9DF43-7780-47DE-8BED-077729D28BD2</RequestId>
       <Success>true</Success>
</DeleteSubscribeRelationResponse>
```

`JSON` 格式

```
{
  "RequestId": "73B9DF43-7780-47DE-8BED-077729D28BD2",
  "Success": true
}
```


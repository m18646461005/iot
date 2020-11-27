# UpdateRuleAction

调用该接口修改指定的规则动作。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=UpdateRuleAction&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateRuleAction|系统规定参数。取值：UpdateRuleAction。 |
|ActionId|Long|是|1000003|要修改的规则动作ID。调用[CreateRuleAction](~~69586~~)成功创建规则动作后返回的**ActionId**参数值，您也可以调用[ListRuleActions](~~69517~~)从返回结果中查看对应规则动作的**Id**参数值。 |
|Configuration|String|是|\{"topic":"/a1iYSOl\*\*\*\*/device5/user/get","topicType":1\}|该规则动作的配置信息。不同规则动作类型所需配置内容不同。具体要求，请参见[CreateRuleAction](~~69586~~)的请求参数补充说明中的各规则动作类型的Configuration描述。 |
|Type|String|是|REPUBLISH|规则动作类型，取值：

 -   **DATAHUB**：流转规则处理后的Topic数据至阿里云DataHub，进行流式数据处理。
-   **ONS**：流转规则处理后的Topic数据至阿里云消息队列RocketMQ，进行消息分发。
-   **MNS**：流转规则处理后的Topic数据至阿里云消息服务中，进行消息传输。
-   **FC**：流转规则处理后的Topic数据至阿里云函数计算服务，进行事件计算。
-   **REPUBLISH**：流转规则处理后的Topic数据至另一个物联网平台 Topic。
-   **AMQP**：数据流转到AMQP消费组。
-   **OTS**：流转规则处理后的Topic数据至阿里云表格存储，进行NoSQL数据存储。

 **说明：**

-   数据格式为二进制的规则（即规则的**DataType**参数是**BINARY**）不支持转发数据至OTS（表格存储）。
-   服务地域不同，规则引擎所支持的数据转发目标云产品不同。具体请参见规则引擎相关[地域和可用区](~~85669~~)。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|21D327AF-A7DE-4E59-B5D1-ACAC8C024555|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=UpdateRuleAction
&ActionId=10003
&Type=REPUBLISH
&Configuration={"topic":"/a1iYSOl****/device5/user/get","topicType":1}
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UpdateRuleActionResponse>
      <RequestId>9A2F243E-17FE-4874-QBB5-D02A25155AC8</RequestId>
      <Success>true</Success>
</UpdateRuleActionResponse>
```

`JSON` 格式

```
{
    "RequestId": "21D327AF-A7DE-4E59-B5D1-ACAC8C024555",
    "Success": true
}
```


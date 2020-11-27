# GetRuleAction

调用该接口查询指定规则动作的详细信息。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=GetRuleAction&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetRuleAction|系统规定参数。取值：GetRuleAction。 |
|ActionId|Long|是|100001|要查询的规则动作ID。调用[CreateRuleAction](~~69586~~)成功创建规则动作后返回的**ActionId**参数值，您也可以调用[ListRuleActions](~~69517~~)从返回结果中查看对应规则动作的**Id**参数值。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|F2D0755D-F350-40FE-9A6D-491859DB5E5F|阿里云为该请求生成的唯一标识符。 |
|RuleActionInfo|Struct| |调用成功时，返回的规则动作详细信息。详情参见以下参数。 |
|Configuration|String|\{\\"topic\\":\\"/sys/a1zSA28\*\*\*\*/device/thing/service/property/set\\",\\"topicType\\":0,\\"uid\\":\\"1231579\*\*\*\*\*\*\*\\"\}|该规则动作的配置信息。 |
|ErrorActionFlag|Boolean|false|该规则动作是否为转发错误操作数据的转发动作，即转发流转到其他云产品失败且重试失败的数据。

 -   **true**：该规则动作转发错误操作数据。
-   **false**：该规则动作不转发错误操作数据，而是正常转发操作。 |
|Id|Long|100001|规则动作ID。 |
|RuleId|Long|152323|该规则动作对应的规则ID。 |
|Type|String|REPUBLISH|规则动作类，取值：

 -   **REPUBLISH**：转发到另一个topic。
-   **OTS**：存储到表格存储。
-   **MNS**：发送消息到消息服务。
-   **FC**：发送数据到函数计算。
-   **RDS**：存储数据到云数据库中。
-   **AMQP**：数据流转到AMQP消费组。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=GetRuleAction
&ActionId=1000001
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetRuleActionResponse>
      <RuleActionInfo>
            <Type>REPUBLISH</Type>
            <RuleId>152323</RuleId>
            <Id>100001</Id>
            <Configuration>
                  <topic>/sys/a1zSA28****/device/thing/service/property/set</topic>
                  <topicType>0</topicType>
                  <uid>1231579*******</uid>
            </Configuration>
            <ErrorActionFlag>false</ErrorActionFlag>
      </RuleActionInfo>
      <RequestId>F2D0755D-F350-40FE-9A6D-491859DB5E5F</RequestId>
      <Success>true</Success>
</GetRuleActionResponse>
```

`JSON` 格式

```
{
  "RuleActionInfo": {
    "Type": "REPUBLISH", 
    "RuleId": 152323, 
    "Id": 100001, 
    "Configuration": "{\"topic\":\"/sys/a1zSA28***/device/thing/service/property/set\",\"topicType\":0,\"uid\":\"1231579*******\"}", 
    "ErrorActionFlag": false
  }, 
  "RequestId": "F2D0755D-F350-40FE-9A6D-491859DB5E5F", 
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


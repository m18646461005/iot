# GetRule

调用该接口查询指定规则的详细信息。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=GetRule&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetRule|系统规定参数。取值：GetRule。 |
|RuleId|Long|是|100000|要查询的规则ID。可在物联网平台控制台**规则引擎**\>**云产品流转**页查看规则ID，或调用[ListRule](~~69486~~)从返回结果中查看。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|58D4CEC0-3E95-4DBE-AFC1-809D1400E52F|阿里云为该请求生成的唯一标识符。 |
|RuleInfo|Struct| |调用成功时，返回的规则详细信息。详情参见以下RuleInfo。 |
|CreateUserId|Long|100000000000000|创建该规则的用户ID。 |
|Created|String|Thu Feb 28 14:14:33 CST 2019|该规则创建时的CST时间。 |
|DataType|String|JSON|该规则的数据类型，取值：**JSON**或**BINARY**。 |
|Id|Long|100000|规则ID。 |
|Modified|String|Thu Feb 28 14:20:58 CST 2019|该规则最近一次被修改时的CST时间。 |
|Name|String|iotrules|规则名称。 |
|ProductKey|String|a1KiV\*\*\*\*\*\*|应用该规则的产品ProductKey。 |
|RuleDesc|String|rule1Desc|规则的描述信息。 |
|Select|String|deviceName\(\) as deviceName|该规则SQL语句中的**Select**内容。 |
|ShortTopic|String|+/user/pm25data|该规则所处理消息来源的具体Topic（不包含ProductKey类目），格式为：`${deviceName}/topicShortName`。其中，$\{deviceName\}是具体设备的名称，topicShortName是Topic余下部分。

 **说明：** 若Topic包含通配符`+`或`#`，请参见[Topic通配符说明](~~73731~~)。 |
|Status|String|STOP|该规则的运行状态。取值：

 -   **RUNNING**：运行中
-   **STOP**：停止 |
|Topic|String|/a1QsMlL44pp/+/user/pm25data|该规则所处理消息来源的完整Topic，格式为：`${productKey}/${deviceName}/topicShortName`。

 **说明：** 若Topic包含通配符`+`或`#`，请参见[Topic通配符说明](~~73731~~)。 |
|TopicType|Integer|1|若您设置了规则SQL语句，则返回：

 -   **0**：表示基础通信Topic或物模型通信Topic。
-   **1**：表示自定义Topic。
-   **2**：表示设备状态Topic。

 若未设置过规则SQL语句，则返回**-1**。 |
|UtcCreated|String|2019-02-28T06:14:33.000Z|规则创建时的UTC时间。 |
|UtcModified|String|2019-02-28T06:20:58.000Z|规则最近一次更新时的UTC时间。 |
|Where|String|Temperature\>35|该规则SQL语句中的**Where**查询条件。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=GetRule
&RuleId=100000
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetRuleResponse>
  <RequestId>85648524-E5EE-418E-BD16-FAFBB4FF3645</RequestId>
  <Success>true</Success>
  <RuleInfo>
        <DataType>JSON</DataType>
        <ShortTopic>+/user/pm25data</ShortTopic>
        <ProductKey>a1QsMl****</ProductKey>
        <UtcModified>2019-12-23T03:34:45.000Z</UtcModified>
        <CreateUserId>198426864326****</CreateUserId>
        <UtcCreated>2019-12-23T02:32:06.000Z</UtcCreated>
        <Name>Ruff_rule1</Name>
        <Status>RUNNING</Status>
        <Select>deviceName() as deviceName , timestamp('yyyy-MM-dd HH:mm:ss') as time, pm25, pm10</Select>
        <Created>Mon Dec 23 10:32:06 CST 2019</Created>
        <Modified>Mon Dec 23 11:34:45 CST 2019</Modified>
        <TopicType>1</TopicType>
        <Topic>/a1QsMlL****/+/user/pm25data</Topic>
        <Id>425367</Id>
  </RuleInfo>
</GetRuleResponse>
```

`JSON` 格式

```
{
	"RequestId": "85648524-E5EE-418E-BD16-FAFBB4FF3645",
	"Success": true,
	"RuleInfo": {
		"DataType": "JSON",
		"ShortTopic": "+/user/pm25data",
		"ProductKey": "a1QsMl****",
		"UtcModified": "2019-12-23T03:34:45.000Z",
		"CreateUserId": "198426864326****",
		"UtcCreated": "2019-12-23T02:32:06.000Z",
		"Name": "Ruff_rule1",
		"Status": "RUNNING",
		"Select": "deviceName() as deviceName , timestamp('yyyy-MM-dd HH:mm:ss') as time, pm25, pm10",
		"Created": "Mon Dec 23 10:32:06 CST 2019",
		"Modified": "Mon Dec 23 11:34:45 CST 2019",
		"TopicType": 1,
		"Topic": "/a1QsMlL****/+/user/pm25data",
		"Id": 425367
	}
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


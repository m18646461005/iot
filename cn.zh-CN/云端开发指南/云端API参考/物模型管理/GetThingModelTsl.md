# GetThingModelTsl

调用该接口查询指定产品的物模型TSL。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为20。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=GetThingModelTsl&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetThingModelTsl|系统规定参数。取值：GetThingModelTsl。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|产品的ProductKey。

 可以在物联网平台控制台产品页查看，或调用[QueryProductList](~~69271~~)查看ProductKey的取值。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ResourceGroupId|String|否|rg-acfm4l5tcwd\*\*\*\*|资源组ID。

 **说明：** 目前不传入此参数。 |
|ModelVersion|String|否|v1.0.0|要查询的物模型版本号。

 不传入此参数，则将返回未发布上线的草稿版物模型TSL。 |
|Simple|Boolean|否|true|是否获取精简版物模型信息。

 -   **true**：获取精简版物模型TSL。

精简版物模型TSL中仅包含属性、服务、事件及入参和出参的标识符（**identifier**）和数据类型（**dataType**），可供设备端开发人员参考。

-   **false**：获取完整的物模型TSL。

完整物模型TSL中包含属性、服务和事件定义的所有参数和取值，可供云端应用开发人员参考。


 不传入此参数，则默认为false，获取完整的物模型信息。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的物模型信息。 |
|TslStr|String|\{\\"schema\\":\\"https://iotx-tsl.oss-ap-southeast-1.aliyuncs.com/schema.json\\",\\"profile\\":\{\\"productKey\\":\\"a14TeWI\*\*\*\*\\"\},\\"properties\\":\[\{\\"identifier\\":\\"Humidity\\"\}\]\}|物模型的TSL字符串。 |
|TslUri|String|https://iotx-pop-dsl.oss-cn-shanghai.aliyuncs.com/thing/a14TeWI\*\*\*\*/model.json?Expires=1581947119&OSSAccessKeyId=LTAIuFOwFSR9\*\*\*\*&Signature=5i389hacjdj3t%2FnrHmQpEUfnxw\*\*\*\*|物模型数据在对象存储（OSS）上的存储地址URI。返回的URI有效期为60分钟。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=GetThingModelTsl
&ProductKey=a1bPo9p****
&ModelVersion=v1.0.0
&Simple=false
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetThingModelTslResponse>
  <Data>
        <TslUri>https://iotx-pop-dsl.oss-cn-shanghai.aliyuncs.com/thing/a14TeWI****/model.json?Expires=1581947119&amp;OSSAccessKeyId=LTAIuFOwFSR9****&amp;Signature=5i389hacjdj3t%2FnrHmQpEUfnx****</TslUri>
        <TslStr>{"schema":"https://iotx-tsl.oss-ap-southeast-1.aliyuncs.com/schema.json","profile":{"productKey":"a14TeWIjbCO"},"properties":[{"identifier":"Humidity","name":"湿度","accessMode":"rw","required":false,"dataType":{"type":"int","specs":{"min":"55","max":"60","unit":"%","step":"1"}}},{"identifier":"Temperature","name":"温度","accessMode":"rw","required":false,"dataType":{"type":"float","specs":{"min":"26","max":"28","unit":"°C","step":"0.01"}}}],"events":[{"identifier":"post","name":"post","type":"info","required":true,"desc":"属性上报","method":"thing.event.property.post","outputData":[{"identifier":"Humidity","name":"湿度","dataType":{"type":"int","specs":{"min":"55","max":"60","unit":"%","step":"1"}}},{"identifier":"Temperature","name":"温度","dataType":{"type":"float","specs":{"min":"26","max":"28","unit":"°C","step":"0.01"}}}]}],"services":[{"identifier":"set","name":"set","required":true,"callType":"async","desc":"属性设置","method":"thing.service.property.set","inputData":[{"identifier":"Humidity","name":"湿度","dataType":{"type":"int","specs":{"min":"55","max":"60","unit":"%","step":"1"}}},{"identifier":"Temperature","name":"温度","dataType":{"type":"float","specs":{"min":"26","max":"28","unit":"°C","step":"0.01"}}}],"outputData":[]},{"identifier":"get","name":"get","required":true,"callType":"async","desc":"属性获取","method":"thing.service.property.get","inputData":["Humidity","Temperature"],"outputData":[{"identifier":"Humidity","name":"湿度","dataType":{"type":"int","specs":{"min":"55","max":"60","unit":"%","step":"1"}}},{"identifier":"Temperature","name":"温度","dataType":{"type":"float","specs":{"min":"26","max":"28","unit":"°C","step":"0.01"}}}]}]}</TslStr>
  </Data>
  <RequestId>C4371E68-F6DB-4D7B-8AD0-D38336E1DF94</RequestId>
  <Success>true</Success>
</GetThingModelTslResponse>
```

`JSON` 格式

```
{
	"Data": {
		"TslUri": "https://iotx-pop-dsl.oss-cn-shanghai.aliyuncs.com/thing/a14TeWI****/model.json?Expires=1581947119&OSSAccessKeyId=LTAIuFOwFSR9****&Signature=5i389hacjdj3t%2FnrHmQpEUfnx****",
		"TslStr": "{\"schema\":\"https://iotx-tsl.oss-ap-southeast-1.aliyuncs.com/schema.json\",\"profile\":{\"productKey\":\"a14TeWIjbCO\"},\"properties\":[{\"identifier\":\"Humidity\",\"name\":\"湿度\",\"accessMode\":\"rw\",\"required\":false,\"dataType\":{\"type\":\"int\",\"specs\":{\"min\":\"55\",\"max\":\"60\",\"unit\":\"%\",\"step\":\"1\"}}},{\"identifier\":\"Temperature\",\"name\":\"温度\",\"accessMode\":\"rw\",\"required\":false,\"dataType\":{\"type\":\"float\",\"specs\":{\"min\":\"26\",\"max\":\"28\",\"unit\":\"°C\",\"step\":\"0.01\"}}}],\"events\":[{\"identifier\":\"post\",\"name\":\"post\",\"type\":\"info\",\"required\":true,\"desc\":\"属性上报\",\"method\":\"thing.event.property.post\",\"outputData\":[{\"identifier\":\"Humidity\",\"name\":\"湿度\",\"dataType\":{\"type\":\"int\",\"specs\":{\"min\":\"55\",\"max\":\"60\",\"unit\":\"%\",\"step\":\"1\"}}},{\"identifier\":\"Temperature\",\"name\":\"温度\",\"dataType\":{\"type\":\"float\",\"specs\":{\"min\":\"26\",\"max\":\"28\",\"unit\":\"°C\",\"step\":\"0.01\"}}}]}],\"services\":[{\"identifier\":\"set\",\"name\":\"set\",\"required\":true,\"callType\":\"async\",\"desc\":\"属性设置\",\"method\":\"thing.service.property.set\",\"inputData\":[{\"identifier\":\"Humidity\",\"name\":\"湿度\",\"dataType\":{\"type\":\"int\",\"specs\":{\"min\":\"55\",\"max\":\"60\",\"unit\":\"%\",\"step\":\"1\"}}},{\"identifier\":\"Temperature\",\"name\":\"温度\",\"dataType\":{\"type\":\"float\",\"specs\":{\"min\":\"26\",\"max\":\"28\",\"unit\":\"°C\",\"step\":\"0.01\"}}}],\"outputData\":[]},{\"identifier\":\"get\",\"name\":\"get\",\"required\":true,\"callType\":\"async\",\"desc\":\"属性获取\",\"method\":\"thing.service.property.get\",\"inputData\":[\"Humidity\",\"Temperature\"],\"outputData\":[{\"identifier\":\"Humidity\",\"name\":\"湿度\",\"dataType\":{\"type\":\"int\",\"specs\":{\"min\":\"55\",\"max\":\"60\",\"unit\":\"%\",\"step\":\"1\"}}},{\"identifier\":\"Temperature\",\"name\":\"温度\",\"dataType\":{\"type\":\"float\",\"specs\":{\"min\":\"26\",\"max\":\"28\",\"unit\":\"°C\",\"step\":\"0.01\"}}}]}]}"
	},
	"RequestId": "C4371E68-F6DB-4D7B-8AD0-D38336E1DF94",
	"Success": true
}
```


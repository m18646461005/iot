# UpdateProductTopic

调用该接口更新指定的产品自定义Topic类。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=UpdateProductTopic&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateProductTopic|系统规定参数。取值：UpdateProductTopic。 |
|Operation|String|是|PUB|设备对该Topic类的操作权限，取值：

 -   **SUB**：订阅。
-   **PUB**：发布。
-   **ALL**：发布和订阅。 |
|TopicId|String|是|821\*\*\*\*|要修改的Topic类的ID。 |
|TopicShortName|String|是|resubmit|设置Topic类的自定义类目名称。Topic类默认包含\_productKey\_和\_deviceName\_两级类目，类目间以正斜线（/）分隔，其格式为：`productKey/deviceName/topicShortName`。

 **说明：** 每级类目的名称只能包含字母、数字和下划线（\_），且不能为空。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|Desc|String|否|resubmit a test topic|Topic类的描述信息。长度限制为100字符（一个汉字占一个字符）。 |

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
https://iot.cn-shanghai.aliyuncs.com/?Action=UpdateProductTopic
&TopicId=821****
&TopicShortName=resubmit
&Operation=PUB
&Desc=resubmit a test topic
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UpdateProductTopicResponse>
      <RequestId>FCC27691-9151-4B93-9622-9C90F30542EC</RequestId>
      <Success>true</Success>
</UpdateProductTopicResponse>
```

`JSON` 格式

```
{
    "RequestId":"FCC27691-9151-4B93-9622-9C90F30542EC",
    "Success":true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


# SetDeviceGroupTags

调用该接口添加、更新、或删除分组标签。

## 限制说明

-   单个分组最多可有100个标签。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=SetDeviceGroupTags&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetDeviceGroupTags|系统规定参数。取值：SetDeviceGroupTags。 |
|GroupId|String|是|W16X8Tvdosec\*\*\*\*|分组ID，分组的全局唯一标识符。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|TagString|String|否|\[\{"tagKey":"h1","tagValue":"rr"\},\{"tagKey":"7h","tagValue":"rr"\}\]|JSON格式的标签数据。TagString由标签的**tagKey**和**tagValue**组成，**tagKey**和**tagValue**均不能为空。

 -   **tagKey**：标签键。可包含英文大小写字母，数字和点号（.），长度在2-30字符之间。
-   **tagValue**：标签值。可包含中文、英文字母、数字、下划线（\_）和短划线（-）。长度不可超过128个字符。一个中文汉字算2字符。

 多个标签以英文逗号间隔。如`[{"tagKey":"h1","tagValue":"rr"},{"tagKey":"7h","tagValue":"rr"}]`。

 若更新已有标签，新的标签value值将覆盖原来的值。

 若要删除某个标签，则不传入该标签的key和value即可。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|12CFDAF1-99D9-42E0-8C2F-F281DA5E8953|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=SetDeviceGroupTags
&GroupId=W16X8Tvdosec****
&TagString=[{"tagKey":"h1","tagValue":"rr"},{"tagKey":"7h","tagValue":"rr"}]
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SetDeviceGroupTagsResponse>
      <RequestId>12CFDAF1-99D9-42E0-8C2F-F281DA5E8953</RequestId>
      <Success>true</Success>
</SetDeviceGroupTagsResponse>
```

`JSON` 格式

```
{
    "RequestId":"12CFDAF1-99D9-42E0-8C2F-F281DA5E8953",
    "Success":true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


# CreateProductTags

调用该接口为指定产品创建标签。

## 限制说明

-   单次调用该接口最多能为指定产品创建10个标签。
-   单个产品的标签总数不超过100个。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateProductTags&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateProductTags|系统规定参数。取值：CreateProductTags。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|产品的ProductKey。ProductKey是物联网平台为新建产品颁发的产品Key，作为其全局唯一标识符。您可以在物联网平台控制台查看或调用[QueryProductList](~~69271~~)查看当前账号下所有产品的信息。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ProductTag.N.TagKey|String|否|room|产品标签键（Key）。可包含英文大小写字母，数字和点号（.），长度不可超过30个字符。 |
|ProductTag.N.TagValue|String|否|TagValue|产品标签值（Value）。可包含中文、英文字母、数字、下划线（\_）和连接号（-）。长度不可超过128字符。一个中文汉字算2字符。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|InvalidProductTags|Array of ProductTag| |调用失败时，返回不合法的产品标签列表。 |
|ProductTag| | | |
|TagKey|String|room|标签键。 |
|TagValue|String|123$|标签值。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/&Action=CreateProductTags
&ProductKey=a1h7knJ****
&ProductTag.1.TagKey=first
&ProductTag.1.TagValue=value1
&ProductTag.2.TagKey=second
&ProductTag.2.TagValue=value2
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateProductTagsResponse>
      <RequestId>57b144cf-09fc-4916-a272-a62902d5b207</RequestId>
      <Success>true</Success>
</CreateProductTagsResponse>
```

`JSON` 格式

```
{
  "RequestId": "354A4F9B-6B01-4498-8084-867F59720BA5",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


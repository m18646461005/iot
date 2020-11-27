# DeleteProductTags

调用该接口删除产品标签。

## 限制说明

-   单次调用该接口最多可删除10个标签。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=DeleteProductTags&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteProductTags|系统规定参数。取值：DeleteProductTags。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|产品的ProductKey。ProductKey是物联网平台为新建产品颁发的产品Key，作为其全局唯一标识符。您可以在物联网平台控制台查看或调用[QueryProductList](~~69271~~)查看当前账号下所有产品的信息。 |
|ProductTagKey.N|RepeatList|是|room|要删除的标签键列表。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=DeleteProductTags
&ProductKey=a1h7knJdld1
&ProductTagKey.1=first
&ProductTagKey.2=second
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteProductTagsResponse>
  <RequestId>E7E8456E-EDD7-41D3-83B1-62FF4F5ED6BD</RequestId>
  <Success>true</Success>
</DeleteProductTagsResponse>
```

`JSON` 格式

```
{
  "RequestId": "E7E8456E-EDD7-41D3-83B1-62FF4F5ED6BD",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


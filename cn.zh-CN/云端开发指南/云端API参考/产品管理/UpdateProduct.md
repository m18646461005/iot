# UpdateProduct

调用该接口修改指定产品的信息。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=UpdateProduct&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateProduct|系统规定参数。取值：UpdateProduct。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|要更新的产品的ProductKey。ProductKey是物联网平台为新建产品颁发的产品Key，作为其全局唯一标识符。您可以在物联网平台控制台查看或调用[QueryProductList](~~69271~~)查看当前账号下所有产品的信息。 |
|ProductName|String|是|路灯|修改后的产品名称。产品名应满足以下限制：长度为4-30字符，可以包含中文、英文字母、数字和下划线（\_）。一个中文字符占两位。

 **说明：** 产品名在当前账号下应具有唯一性。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|Description|String|否|第二代路灯产品。|描述产品信息。长度不超过100字符。一个中文算一个字符。 |

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
https://iot.cn-shanghai.aliyuncs.com/?Action=UpdateProduct
&ProductKey=a1BwAGV****
&ProductName=TestProductNew
&Description=new features v2
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UpdateProductResponse>
  <RequestId>C4FDA54C-4201-487F-92E9-022F42387458</RequestId>
  <Success>true</Success>
</UpdateProductResponse>
```

`JSON` 格式

```
{
      "RequestId":"C4FDA54C-4201-487F-92E9-022F42387458",
      "Success":true
  }
```


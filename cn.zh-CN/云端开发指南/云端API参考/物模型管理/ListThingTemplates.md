# ListThingTemplates

调用该接口获取物联网平台预定义的标准产品品类列表。

## 使用说明

物联网平台提供已定义了物模型的产品品类供您使用，例如路灯照明、车辆定位卡、水浸检测等。

您调用[CreateProduct](~~69123~~)接口创建产品时，可以传入参数CategoryKey指定品类，创建的产品将引用该品类的标准物模型。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=ListThingTemplates&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListThingTemplates|系统规定参数。取值：ListThingTemplates。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ResourceGroupId|String|否|rg-acfm4l5tcwd\*\*\*\*|资源组ID。

 **说明：** 目前不传入该参数 。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Array of CategoryInfo| |调用成功时，返回的标准品类列表。 |
|CategoryKey|String|lighting|品类的标识符。 |
|CategoryName|String|路灯照明|品类的名称。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=ListThingTemplates
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListThingTemplatesResponse>
  <RequestId>57b144cf-09fc-4916-a272-a62902d5b207</RequestId>
  <Success>true</Success>
  <Data>
        <CategoryName>智能后视镜</CategoryName>
        <CategoryKey>SmartRearviewMirror</CategoryKey>
  </Data>
  <Data>
        <CategoryName>智能车机</CategoryName>
        <CategoryKey>SmartTox</CategoryKey>
  </Data>
</ListThingTemplatesResponse>
```

`JSON` 格式

```
{
  "RequestId":"57b144cf-09fc-4916-a272-a62902d5b207",
  "Success":true,
  "Data": [
    {
      "CategoryName": "智能后视镜",
      "CategoryKey": "SmartRearviewMirror"
    },
    {
      "CategoryName": "智能车机",
      "CategoryKey": "SmartTox"
    }
  ]
}
```


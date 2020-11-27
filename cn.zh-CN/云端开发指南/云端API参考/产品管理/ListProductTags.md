# ListProductTags

调用该接口查询指定产品的所有标签。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=ListProductTags&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListProductTags|系统规定参数。取值：ListProductTags。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|产品的ProductKey。ProductKey是物联网平台为新建产品颁发的产品Key，作为其全局唯一标识符。您可以在物联网平台控制台查看或调用[QueryProductList](~~69271~~)查看当前账号下所有产品的信息。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Array of ProductTag| |调用成功时，返回产品标签信息列表，具体信息见一下ProductTag包含的参数。 |
|ProductTag| | | |
|TagKey|String|room|标签键。 |
|TagValue|String|102|标签值。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=ListProductTags
&ProductKey=a1h7knJ****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListProductTagsResponse>
      <Data>
            <ProductTag>
                  <TagValue>alterTable</TagValue>
                  <TagKey>binary</TagKey>
            </ProductTag>
            <ProductTag>
                  <TagValue>json2</TagValue>
                  <TagKey>extt</TagKey>
            </ProductTag>
            <ProductTag>
                  <TagValue>1234</TagValue>
                  <TagKey>Lock</TagKey>
            </ProductTag>
            <ProductTag>
                  <TagValue>support</TagValue>
                  <TagKey>Lockk</TagKey>
            </ProductTag>
            <ProductTag>
                  <TagValue>reen</TagValue>
                  <TagKey>Reen</TagKey>
            </ProductTag>
            <ProductTag>
                  <TagValue>try</TagValue>
                  <TagKey>Reenn</TagKey>
            </ProductTag>
            <ProductTag>
                  <TagValue>DropTable</TagValue>
                  <TagKey>roc</TagKey>
            </ProductTag>
      </Data>
      <RequestId>7FBE60F8-4AB5-4A8C-AFCB-F4F38851F01F</RequestId>
      <Success>true</Success>
</ListProductTagsResponse>
```

`JSON` 格式

```
{
  "Data": {
    "ProductTag": [
      {
        "TagValue": "alterTable",
        "TagKey": "binary"
      },
      {
        "TagValue": "json2",
        "TagKey": "extt"
      },
      {
        "TagValue": "1234",
        "TagKey": "Lock"
      },
      {
        "TagValue": "support",
        "TagKey": "Lockk"
      },
      {
        "TagValue": "reen",
        "TagKey": "Reen"
      },
      {
        "TagValue": "try",
        "TagKey": "Reenn"
      },
      {
        "TagValue": "DropTable",
        "TagKey": "roc"
      }
    ]
  },
  "RequestId": "7FBE60F8-4AB5-4A8C-AFCB-F4F38851F01F",
  "Success": true
}
```


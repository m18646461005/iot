# ListProductByTags

调用该接口根据标签分页查询产品列表。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=ListProductByTags&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListProductByTags|系统规定参数。取值：ListProductByTags。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|CurrentPage|Integer|否|1|指定显示返回结果中的第几页。 |
|PageSize|Integer|否|10|指定返回结果中每页显示的记录数量。最大值是50。 |
|ProductTag.N.TagKey|String|否|room|产品标签键。 |
|ProductTag.N.TagValue|String|否|102|产品标签值。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

**说明：** 支持按照TagKey和TagValue组合来搜索。支持只按照TagKey来搜索。传入多个ProductTag是或的关系。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|ProductInfos|Array of ProductInfo| |调用成功时，返回产品信息列表（**ProductInfo**）。

 **说明：** 返回的产品信息按照产品创建时间倒序排列。 |
|ProductInfo| | | |
|CreateTime|Long|1545355537000|产品创建时间。 |
|Description|String|This is a test product.|产品描述。 |
|NodeType|Integer|0|产品的节点类型，取值：

 -   **0**：设备。设备不能挂载子设备。可以直连物联网平台，也可以作为网关的子设备连接物联网平台。
-   **1**：网关。网关可以挂载子设备，具有子设备管理模块，维持子设备的拓扑关系，和将拓扑关系同步到物联网平台。 |
|ProductKey|String|a1BwAGV\*\*\*\*|产品的ProductKey。ProductKey是物联网平台为新建产品颁发的产品Key，作为其全局唯一标识符。 |
|ProductName|String|路灯|产品名称。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=ListProductByTags
&CurrentPage=1
&PageSize=10
&ProductTag.1.TagKey=Reen
&ProductTag.1.TagValue=reen
&ProductTag.2.TagKey=Lock
&ProductTag.2.TagValue=1234
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListProductByTagsResponse>
  <RequestId>09AA366E-81EC-4CF0-B49E-61BCD7C95338</RequestId>
  <Success>true</Success>
  <ProductInfos>
        <ProductInfo>
              <ProductKey>a1T27vzfrCj</ProductKey>
              <NodeType>0</NodeType>
              <CreateTime>1581595942000</CreateTime>
              <ProductName>路灯</ProductName>
        </ProductInfo>
        <ProductInfo>
              <ProductKey>a1POX0c3iug</ProductKey>
              <NodeType>0</NodeType>
              <CreateTime>1580898565000</CreateTime>
              <ProductName>TSL测试</ProductName>
        </ProductInfo>
  </ProductInfos>
</ListProductByTagsResponse>
```

`JSON` 格式

```
{
	"RequestId": "09AA366E-81EC-4CF0-B49E-61BCD7C95338",
	"Success": true,
	"ProductInfos": {
		"ProductInfo": [
			{
				"ProductKey": "a1T27vzfrCj",
				"NodeType": 0,
				"CreateTime": 1581595942000,
				"ProductName": "路灯"
			},
			{
				"ProductKey": "a1POX0c3iug",
				"NodeType": 0,
				"CreateTime": 1580898565000,
				"ProductName": "TSL测试"
			}
		]
	}
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


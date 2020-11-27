# QueryDeviceByTags

调用该接口通过标签查询设备。

## 限制说明

-   一次调用，最多可输入10个标签。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceByTags&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceByTags|系统规定参数。取值：QueryDeviceByTags。 |
|Tag.N.TagKey|String|是|room|设备标签的Key。 |
|Tag.N.TagValue|String|是|101|设备标签的值。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|CurrentPage|Integer|否|1|指定从返回结果中的第几页开始显示。默认值是1。 |
|PageSize|Integer|否|10|指定返回结果中每页显示的设备记录数量，最大值是50。默认值是10。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Array of SimpleDeviceInfo| |调用成功时，返回的设备信息列表（**SimpleDeviceInfo**）。 |
|SimpleDeviceInfo| | | |
|DeviceName|String|light1|设备名称。 |
|IotId|String|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|物联网平台为该设备颁发的ID，作为该设备的唯一标识符。 |
|ProductKey|String|a1BwAGV\*\*\*\*|设备所属产品的ProductKey。 |
|ProductName|String|lamp|产品名称。 |
|ErrorMessage|String|系统异常|调用失败时返回的出错信息。 |
|Page|Integer|1|当前页面号。 |
|PageCount|Integer|1|总页数。 |
|PageSize|Integer|10|每页显示的记录数。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|Total|Integer|1|总记录数。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceByTags
&CurrentPage=1
&PageSize=10
&Tag.1.TagKey=room
&Tag.1.TagValue=101
&Tag.2.TagKey=city
&Tag.2.TagValue=hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceByTags>
  <PageCount>1</PageCount>
  <Data>
        <SimpleDeviceInfo>
              <DeviceName>1102jichu02</DeviceName>
              <ProductKey>a1SM5S1****</ProductKey>
              <IotId>GookTiUcwqRbHosp9Ta10****3a00</IotId>
              <ProductName>TEST</ProductName>
        </SimpleDeviceInfo>
  </Data>
  <PageSize>10</PageSize>
  <Page>1</Page>
  <RequestId>2B5091E4-32D5-4884-A5B2-2E8E713D84AF</RequestId>
  <Success>true</Success>
  <Total>1</Total>
</QueryDeviceByTags>
```

`JSON` 格式

```
{
    "PageCount": 1,
    "Data": {
        "SimpleDeviceInfo": [
            {
                "DeviceName": "1102jichu02",
                "ProductKey": "a1SM5S1****",
                "IotId": "GookTiUcwqRbHosp9Ta10****3a00",
                "ProductName": "TEST"
            }
        ]
    },
    "PageSize": 10,
    "Page": 1,
    "RequestId": "2B5091E4-32D5-4884-A5B2-2E8E713D84AF",
    "Success": true,
    "Total": 1
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


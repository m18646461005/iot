# QueryProductTopic

调用该接口查询指定产品的自定义Topic类。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为3。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryProductTopic&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryProductTopic|系统规定参数。取值：QueryProductTopic。 |
|ProductKey|String|是|HMyB\*\*\*\*\*\*\*|要查询Topic类的产品Key。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Array of ProductTopicInfo| |调用成功时，返回的Topic类信息列表。详情参见以下ProductTopicInfo。 |
|ProductTopicInfo| | | |
|Desc|String|topicDesc|Topic类的描述信息。 |
|Id|String|821\*\*\*\*|Topic类的ID。 |
|Operation|String|1|设备对该Topic类的操作权限，取值：

 -   **0**：发布
-   **1**：订阅
-   **2**：发布和订阅 |
|ProductKey|String|HMyB\*\*\*|产品Key。 |
|TopicShortName|String|/HMyB\*\*\*/$\{deviceName\}/user/get|Topic类中除\_productKey\_和\_deviceName\_以外的类目。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|B953EAFF-CFF6-4FF8-BC94-8B89F018E4DD|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryProductTopic
&ProductKey=HMyB*******
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryProductTopicResponse>
      <Data>
            <Id>10000</Id>
            <Operation>0</Operation>
            <ProductKey>HMyB***</ProductKey>
            <TopicShortName>/HMyB***/${deviceName}/user/update</TopicShortName>
      </Data>
      <Data>
            <Id>10001</Id>
            <Operation>2</Operation>
            <ProductKey>HMyB***</ProductKey>
            <TopicShortName>/HMyB***/${deviceName}/user/update/error</TopicShortName>
      </Data>
      <Data>
            <Id>10002</Id>
            <Operation>1</Operation>
            <ProductKey>HMyB***</ProductKey>
            <TopicShortName>/HMyB***/${deviceName}/user/get</TopicShortName>
      </Data>
      <RequestId>B953EAFF-CFF6-4FF8-BC94-8B89F018E4DD</RequestId>
      <Success>true</Success>
</QueryProductTopicResponse>
```

`JSON` 格式

```
{
    "Data": [{
        "Id": "10000",
        "Operation": "0",
        "ProductKey": "HMyB***",
        "TopicShortName": "/HMyB***/${deviceName}/user/update"
    },
    {
        "Id": "10001",
        "Operation": "2",
        "ProductKey": "HMyB***",
        "TopicShortName": "/HMyB***/${deviceName}/user/update/error"
    },
    {
        "Id": "10002",
        "Operation": "1",
        "ProductKey": "HMyB***",
        "TopicShortName": "/HMyB***/${deviceName}/user/get"
    }],
    "RequestId": "B953EAFF-CFF6-4FF8-BC94-8B89F018E4DD",
    "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


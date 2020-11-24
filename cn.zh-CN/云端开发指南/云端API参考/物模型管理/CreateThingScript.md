# CreateThingScript

调用该接口为指定产品提交数据解析脚本。

## 使用说明

-   数据解析脚本用于将设备上报的自定义格式数据转换为JSON结构体。脚本类型支持JavaScript、Python 2.7、PHP 7.2，更多信息，请参见[提交数据解析脚本](~~149963~~)。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateThingScript&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateThingScript|系统规定参数。取值：CreateThingScript。 |
|ProductKey|String|是|a1Q5XoY\*\*\*\*|产品**ProductKey**。

 可以在物联网平台控制台产品页查看，或调用[QueryProductList](~~69271~~)查看**ProductKey**的取值。 |
|ScriptContent|String|是|"function protocolToRawData\(jsonObj\) \{return rawdata; \}function rawDataToProtocol\(rawData\) \{return jsonObj; \}"|脚本内容。不允许为空。

 脚本示例的更多信息，请参见[什么是数据解析](~~68702~~)。 |
|ScriptType|String|是|JavaScript|脚本类型。取值：

 -   JavaScript
-   Python\_27：表示Python 2.7
-   PHP\_72：表示PHP 7.2 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数；您购买的企业实例需传入此参数。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|BB71E443-4447-4024-A000-EDE09922891E|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=CreateThingScript
&ProductKey=a1Q5XoY****
&ScriptContent="function protocolToRawData(jsonObj) {return rawdata; }function rawDataToProtocol(rawData) {return jsonObj; }"
&ScriptType=JavaScript
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateThingScriptResponse>
    <RequestId>BB71E443-4447-4024-A000-EDE09922891E</RequestId>
    <Success>true</Success>
</CreateThingScriptResponse>
```

`JSON` 格式

```
{
      "RequestId":"BB71E443-4447-4024-A000-EDE09922891E",
      "Success":true
  }
```


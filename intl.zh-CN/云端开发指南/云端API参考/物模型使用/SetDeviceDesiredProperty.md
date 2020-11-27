# SetDeviceDesiredProperty

调用该接口为指定设备批量设置期望属性值。

## 限制说明

-   只读属性不支持设置期望属性值。
-   一次调用最多可设置10个期望属性值。
-   设备创建后，期望属性值的版本（**Version**）为**0**。首次设置期望属性值时，如果指定**Version**参数，则需指定**Version**值为**0**。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=SetDeviceDesiredProperty&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetDeviceDesiredProperty|系统规定参数。取值：SetDeviceDesiredProperty。 |
|Items|String|是|\{"Temperature":35\}|要设置的期望属性值，组成为属性的**Key:Value**，数据格式为 JSON String，例如**\{"Temperature":35\}**。最多可输入10个期望属性值。

 -   **Key**取值为属性的标识符（**identifier**）。可在控制台中，设备所属产品的**功能定义**中查看；或调用[QueryThingModel](~~150321~~)，从返回的物模型数据中查看。

**说明：** 指定属性必须是读写型。如果您指定了一个只读型的属性，设置将会失败。并且， 一次调用中，不能传入重复的属性标识符。

-   **Value**取值为要设置的期望属性值。取值需符合您为该属性定义的数据类型和取值范围。

**说明：** 若属性值设置为null，则表示清空期望属性值。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要设置期望属性值的设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |
|DeviceName|String|否|light|要设置期望属性值的设备名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|要设置期望属性值的设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|Versions|String|否|\{"Temperature":2\}|当前期望属性值版本，组成为Key:Value，数据格式为 JSON String，例如\{"Temperature":2\}。

 -   **Key**取值为属性的标识符（identifier）。可在控制台中，设备所属产品的功能定义中查看属性的identifier。

**说明：** 一次调用中，key的取值（即属性的identifier）不能重复。

-   **Value**取值为当前期望属性值的版本号。

首次设置期望属性值时，指定该参数值为0。首次设置期望属性值后，期望值版本号为1。以后每次设置期望值后，物联网平台自动将期望值版本加1（即第二次设置期望属性值时，指定该参数值为1。设置成功后，版本号自动变为2；第三次设置时，指定该参数值为2。设置成功后，版本号自动变为3；以此类推）。

**说明：** 如果传入的版本号与当前版本不符，服务器将拒绝此次请求。若您不确定当前期望值的版本号，可以不传入版本号，但仍需传入有效的JSON，即传入\{\}。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的数据。详情请参见以下参数。 |
|MessageId|String|300511751|云端下发给设备的设置期望属性值的消息ID。 |
|Versions|String|\{\\"Temperature\\":2\}|本次设置期望属性值后，期望属性值的当前版本号。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=SetDeviceDesiredProperty
&ProductKey=a1BwAGV****
&DeviceName=device1
&Items=%7B%22LightAdjustLevel%22%3A1%7D
&Versions=%7B%22LightAdjustLevel%22%3A10%7D
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SetDeviceDesiredPropertyResponse>
  <Data>
        <MessageId>300511751</MessageId>
        <Versions>{"LightAdjustLevel":2}</Versions>
  </Data>
  <RequestId>AADE79D2-B328-4FC6-A3E0-34BB23BCA440</RequestId>
  <Success>true</Success>
</SetDeviceDesiredPropertyResponse>
```

`JSON` 格式

```
{
    "Data": {
        "MessageId": "300511751",
        "Versions": "{\"LightAdjustLeve\":2}"
    },
    "RequestId": "AADE79D2-B328-4FC6-A3E0-34BB23BCA440",
    "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


# SetDevicesProperty

调用该接口批量设置设备属性值。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=SetDevicesProperty&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetDevicesProperty|系统规定参数。取值：SetDevicesProperty。 |
|DeviceName.N|RepeatList|是|light|要设置属性值的设备名称列表。最多支持传入100个设备名称。 |
|Items|String|是|\{"Switch":1,"Color":"blue"\}|要设置的属性信息，数据格式为JSON。

 每个属性信息由**属性标识符key:属性值value**构成，多个属性用英文逗号隔开。

 例如，设置智能灯的如下两个属性：

 -   标识符为**Switch**的开关属性，数据类型为**Bool**，设置值为**1**（开）；
-   标识符为**Color**的灯颜色属性，数据类型为**String**，设置值为**blue**。

 那么，**Items=\{"Switch":1,"Color":"blue"\}**。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|要设置属性值的设备所隶属的产品**ProductKey**。 |
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
https://iot.cn-shanghai.aliyuncs.com/?Action=SetDevicesProperty
&DeviceName.1=1102andriod02
&DeviceName.2=1102android01
&Items=%7B%20%20%20%20%20%22Data%22%3A%221372060916%22%2C%20%20%20%20%20%22Status%22%3A1%20%7D
&ProductKey=a1hWjHD****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SetDevicesPropertyResponse>
  <RequestId>2E19BDAF-0FD0-4608-9F41-82D230CFEE38</RequestId>
  <Success>true</Success>
</SetDevicesPropertyResponse>
```

`JSON` 格式

```
{
  "RequestId": "2E19BDAF-0FD0-4608-9F41-82D230CFEE38",
  "Success": true
}
```


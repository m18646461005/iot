# RegisterDevice

调用该接口在指定产品下注册设备。

## 接口说明

注册设备指在物联网平台产品下添加设备。在指定产品下成功注册设备后，阿里云物联网平台为设备颁发全局唯一的设备ID（IotId），用来标识该设备。在进行与设备相关的操作时，您可能需要提供目标设备的IotId。您也可以使用ProductKey和DeviceName组合来标识一个设备。其中ProductKey是新建产品时物联网平台为产品颁发的产品Key，DeviceName是注册设备时由您指定或由系统随机生成的设备名称。IotId的优先级高于ProductKey和DeviceName组合。

-   如果您希望在一个产品下批量注册多个设备，并且随机生成设备名，您可以调用[BatchRegisterDevice](~~69473~~)接口。
-   如果您希望在一个产品下批量注册多个设备，并且为每个设备单独命名，您需要先调用[BatchCheckDeviceNames](~~69482~~)接口为每个设备命名，并生成申请批次ID（ApplyId），再调用[BatchRegisterDeviceWithApplyId](~~69514~~)接口批量注册设备。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为30。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=RegisterDevice&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RegisterDevice|系统规定参数。取值：RegisterDevice。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|待注册设备所隶属的产品的ProductKey。ProductKey是物联网平台为新建产品颁发的产品Key，作为其全局唯一标识符。

 您可以在物联网平台控制台查看或调用[QueryProductList](~~69271~~)查看当前账号下所有产品的信息。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|DeviceName|String|否|light|为待注册的设备命名。设备名称长度为4-32个字符，可以包含英文字母、数字和特殊字符：短划线（-）、下划线（\_）、at符号（@）、点号（.）、和英文冒号（:）。

 DeviceName通常与ProductKey组合使用，用作设备标识。

 **说明：** 如果不传入该参数，则由系统随机生成设备名称。 |
|DevEui|String|否|e8SDdgeIlk3nED\*\*\*\*|LoRaWAN设备的DevEUI。

 创建LoRaWAN设备时，该参数必传。 |
|PinCode|String|否|DIe80dfeg\*\*\*\*\*|LoRaWAN设备的PIN Code，用于校验DevEUI的合法性。

 创建LoRaWAN设备时，该参数必传。 |
|Nickname|String|否|园区灯|为待注册的设备设置备注名称。备注名称长度为4-64个字符，可包含中文汉字、英文字母、数字和下划线（\_）。一个中文汉字算2字符。

 **说明：** 如果不传入该参数，系统不会为设备生成备注名称。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回注册的设备信息。 |
|DevEui|String|e8SDdgeIlk3nED\*\*\*\*|LoRaWAN设备的DevEUI。仅LoRaWAN设备才会返回该参数。 |
|DeviceName|String|light|设备名称。

 **说明：** 请妥善保管，勿泄露。 |
|DeviceSecret|String|mz2Canp4GB7qRVf1OYPNtRqB2anu\*\*\*\*|设备密钥。

 **说明：** 请妥善保管，勿泄露。 |
|IotId|String|1O4YPNtRqB2anumz2Canp4GB7q\*\*\*\*|物联网平台为该设备颁发的设备ID，作为该设备的唯一标识符。

 **说明：** 请妥善保管，勿泄露。 |
|JoinEui|String|Ede4tde8erth\*\*\*\*|LoRaWAN设备的入网凭证 JoinEUI。仅LoRaWAN设备才会返回该参数。 |
|Nickname|String|园区灯|设备的备注名称。

 若您没有为该设备设置备注名称，则该参数返回为空。 |
|ProductKey|String|a1BwAGV\*\*\*\*|设备所属产品的ProductKey。 |
|ErrorMessage|String|系统异常|调用失败时，返回的错误信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=RegisterDevice
&ProductKey=a1rYuVF****
&DeviceName=device1
&Nickname=detectors_in_beijing
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RegisterDeviceResponse>
  <RequestId>57b144cf-09fc-4916-a272-a62902d5b207</RequestId>
  <Success>true</Success>
  <Data>
        <DeviceName>device1</DeviceName>
        <ProductKey>a1rYuVF****</ProductKey>
        <DeviceSecret>tXHf4ezGEHcwdyMwoCDHGBmk9avi****</DeviceSecret>
        <IotId>CqXL5h5ysRTA4NxjABjj0010fa****</IotId>
        <Nickname>detectors_in_beijing</Nickname>
  </Data>
</RegisterDeviceResponse>
```

`JSON` 格式

```
{
    "RequestId": "57b144cf-09fc-4916-a272-a62902d5b207", 
    "Success": true, 
    "Data": {
        "DeviceName": "device1", 
        "ProductKey": "a1rYuVF****", 
        "DeviceSecret": "tXHf4ezGEHcwdyMwoCDHGBmk9avi****", 
        "IotId": "CqXL5h5ysRTA4NxjABjj0010fa****", 
        "Nickname": "detectors_in_beijing"
    }
}
```


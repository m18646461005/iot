# QueryOTAFirmware

调用该接口查询指定固件的详细信息。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为20。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryOTAFirmware&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryOTAFirmware|系统规定参数。取值：QueryOTAFirmware。 |
|FirmwareId|String|是|s8SSHiKjpBfrM3BSN0z803\*\*\*\*|固件ID，固件的唯一标识符。

 固件ID是调用[CreateOTAFirmware](~~147311~~)创建固件时，返回的参数之一。

 可以调用[ListOTAFirmware](~~147450~~)，从返回参数中查看。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|FirmwareInfo|Struct| |调用成功时，返回的固件信息。详情见以下**FirmwareInfo**包含的参数。 |
|DestVersion|String|4.0.0|当前固件版本号。 |
|FirmwareDesc|String|modified-WiFi-module|固件描述信息。 |
|FirmwareId|String|UfuxnwygsuSkVE0VCN\*\*\*\*0100|固件ID，固件的唯一标识符。 |
|FirmwareName|String|t3q5rkNm|固件名称。 |
|FirmwareSign|String|3d04ab6462633508606e5f3daac8\*\*\*\*|固件内容的签名值。 |
|FirmwareSize|Integer|924|固件大小，单位：MB。 |
|FirmwareUrl|String|https://ota-pre.iot-thing.cn-shanghai.aliyuncs.com/ota/572ef2fd12ca4791a5b21a9eb948\*\*\*\*/5E962CF83DB1495E8337E9C8A4D1\*\*\*\*.bin?Expires=1577587360&OSSAccessKeyId=cS8uRRy54Rsz\*\*\*\*&Signature=farzC8%2FVMN4HYdEtXvdiC2OevH\*\*\*\*|OSS存储固件的URL。 |
|ModuleName|String|WifiConfigModify|固件模块名称。

 固件模块用于区分同产品下设备的不同模块的升级。 |
|ProductKey|String|a19mzPZ\*\*\*\*|固件所属产品的ProductKey。 |
|ProductName|String|MyProduct|固件所属产品的名称。 |
|SignMethod|String|MD5|固件签名方式。 |
|SrcVersion|String|1.0.0|待升级固件版本号。

 **说明：** 仅差分升级的固件返回该参数。 |
|Status|Integer|2|固件状态。

 -   **0**：未验证。
-   **1**：已验证。
-   **2**：验证中。
-   **3**：验证失败。 |
|Type|Integer|0|固件类型。

 -   **0**：整包固件。
-   **1**：差分固件。 |
|UtcCreate|String|2019-12-28T02:42:22.000Z|固件创建时的时间，UTC格式。 |
|UtcModified|String|2019-12-28T02:42:41.000Z|固件最后一次修改时的时间，UTC格式。 |
|VerifyProgress|Integer|0|固件的验证进度。

 -   **0**：未验证。
-   **100**：已完成验证。
-   0至100之间的数值N：表示N%的设备已完成升级。固件验证状态请根据返回参数**Status**判断。 |
|RequestId|String|A01829CE-75A1-4920-B775-921146A1AB79|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。**true**表示调用成功，**false**表示调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryOTAFirmware
&FirmwareId=s8SSHiKjpBfrM3BSN0z803****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryOTAFirmwareResponse>
    <RequestId>A01829CE-75A1-4920-B775-921146A1AB79</RequestId>
    <FirmwareInfo>
        <SrcVersion></SrcVersion>
        <FirmwareSign>3d04ab6462633508606e5f3daac8****</FirmwareSign>
        <ProductKey>a19mzPZ****</ProductKey>
        <Type>0</Type>
        <UtcModified>2019-12-28T02:42:41.000Z</UtcModified>
        <SignMethod>MD5</SignMethod>
        <UtcCreate>2019-12-28T02:42:41.000Z</UtcCreate>
        <FirmwareSize>924</FirmwareSize>
        <Status>0</Status>
        <FirmwareId>yLYuCqfqQNQ1JOqkDa****0100</FirmwareId>
        <FirmwareDesc>modified-WiFi-module</FirmwareDesc>
        <FirmwareUrl><![CDATA[https://ota-pre.iot-thing.cn-shanghai.aliyuncs.com/ota/572ef2fd12ca4791a5b21a9eb948****/5E962CF83DB1495E8337E9C8A4D1****.bin?Expires=1577587360&OSSAccessKeyId=cS8uRRy54Rsz****&Signature=farzC8%2FVMN4HYdEtXvdiC2OevH****]]></FirmwareUrl>
        <DestVersion>4.0.0</DestVersion>
        <ProductName>MyProduct</ProductName>
        <FirmwareName>t3q5rkNm</FirmwareName>
        <ModuleName>WifiConfigModify</ModuleName>
        <VerifyProgress>0</VerifyProgress>
    </FirmwareInfo>
    <Success>true</Success>
</QueryOTAFirmwareResponse>
```

`JSON` 格式

```
{
  "RequestId": "A01829CE-75A1-4920-B775-921146A1AB79",
  "FirmwareInfo": {
    "SrcVersion": "",
    "FirmwareSign": "3d04ab6462633508606e5f3daac8****",
    "ProductKey": "a19mzPZ****",
    "Type": 0,
    "UtcModified": "2019-12-28T02:42:41.000Z",
    "SignMethod": "MD5",
    "UtcCreate": "2019-12-28T02:42:22.000Z",
    "FirmwareSize": 924,
    "Status": 2,
    "FirmwareId": "UfuxnwygsuSkVE0VCN****0100",
    "FirmwareDesc": "modified-WiFi-module",
    "FirmwareUrl": "https://ota-pre.iot-thing.cn-shanghai.aliyuncs.com/ota/572ef2fd12ca4791a5b21a9eb948****/5E962CF83DB1495E8337E9C8A4D1****.bin?Expires=1577587360&OSSAccessKeyId=cS8uRRy54Rsz****&Signature=farzC8%2FVMN4HYdEtXvdiC2OevH****",
    "DestVersion": "4.0.0",
    "ProductName": "MyProduct",
    "FirmwareName": "t3q5rkNm",
    "ModuleName": "WifiConfigModify",
    "VerifyProgress": 0
  },
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


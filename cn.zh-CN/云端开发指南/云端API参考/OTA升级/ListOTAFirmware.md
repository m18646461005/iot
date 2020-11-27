# ListOTAFirmware

调用该接口查询固件列表。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=ListOTAFirmware&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListOTAFirmware|系统规定参数。取值：ListOTAFirmware。 |
|CurrentPage|Integer|是|1|指定从返回结果中的第几页开始显示。页数从1开始排序。 |
|PageSize|Integer|是|10|指定返回结果中每页显示的固件数量。最大限制为100。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ProductKey|String|否|a19mzPZ\*\*\*\*|固件所属产品的ProductKey。

 传入该参数，则查询指定产品下的固件列表；不传入此参数，则返回当前阿里云账号下的所有固件列表。 |
|DestVersion|String|否|4.0.0|固件版本号。传入该参数，则查询版本号为指定版本号的固件。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|CurrentPage|Integer|1|当前页码。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|FirmwareInfo|Array of SimpleFirmwareInfo| |调用成功时，返回的固件列表。详情参见以下SimpleFirmwareInfo。 |
|SimpleFirmwareInfo| | | |
|DestVersion|String|4.0.0|当前固件版本号。 |
|FirmwareDesc|String|firmwareDesc|固件描述信息。 |
|FirmwareId|String|UfuxnwygsuSkVE0VCN\*\*\*\*0100|固件ID，固件的唯一标识符。 |
|FirmwareName|String|t3q5rkNm|固件名称。 |
|FirmwareSign|String|3d04ab6462633508606e5f3daac8\*\*\*\*|固件内容的签名值。 |
|FirmwareSize|Integer|924|固件大小，单位：字节。 |
|FirmwareUrl|String|https://iotx-ota-pre.oss-cn-shanghai.aliyuncs.com/ota/572ef2fd12ca4791a5b21a9eb948\*\*\*\*/5E962CF83DB1495E8337E9C8A4D1\*\*\*\*.bin|OSS存储固件的URL。 |
|ModuleName|String|module1234|升级固件的模块名称。 |
|ProductKey|String|a19mzPZ\*\*\*\*|固件所属产品的ProductKey。 |
|ProductName|String|MyProduct|固件所属产品的名称。 |
|SignMethod|String|MD5|固件签名方式。 |
|SrcVersion|String|V1.0.0|待升级固件版本号。

 **说明：** 整包固件返回的该参数为空。 |
|Status|Integer|0|固件状态。

 -   **0**：未验证。
-   **1**：已验证。
-   **2**：验证中。
-   **3**：验证失败。 |
|Type|Integer|0|固件类型。

 -   **0**：整包固件。
-   **1**：差分固件。 |
|UtcCreate|String|2019-12-28T02:42:22.000Z|固件创建时的时间，UTC格式。 |
|UtcModified|String|2019-12-28T02:42:22.000Z|固件最后一次修改时的时间，UTC格式。 |
|PageCount|Integer|1|总页数。 |
|PageSize|Integer|10|每页显示的固件数量。 |
|RequestId|String|A01829CE-75A1-4920-B775-921146A1AB79|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|Total|Integer|1|固件数量总计。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=ListOTAFirmware
&CurrentPage=1
&PageSize=10
&ProductKey=a19mzPZ****
&DestVersion=4.0.0
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListOTAFirmwareResponse>
  <PageCount>1</PageCount>
  <PageSize>10</PageSize>
  <RequestId>A01829CE-75A1-4920-B775-921146A1AB79</RequestId>
  <FirmwareInfo>
        <SimpleFirmwareInfo>
              <SrcVersion>1.0.0</SrcVersion>
              <FirmwareSign>3d04ab6462633508606e5f3daac8****</FirmwareSign>
              <ProductKey>a19mzPZ****</ProductKey>
              <Type>0</Type>
              <UtcModified>2019-12-28T02:42:22.000Z</UtcModified>
              <SignMethod>MD5</SignMethod>
              <UtcCreate>2019-12-28T02:42:22.000Z</UtcCreate>
              <FirmwareSize>924</FirmwareSize>
              <Status>0</Status>
              <FirmwareId>UfuxnwygsuSkVE0VCN****0100</FirmwareId>
              <FirmwareDesc>firmwareDesc</FirmwareDesc>
              <FirmwareUrl>https://iotx-ota-pre.oss-cn-shanghai.aliyuncs.com/ota/572ef2fd12ca4791a5b21a9eb948****/5E962CF83DB1495E8337E9C8A4D1****.bin</FirmwareUrl>
              <DestVersion>4.0.0</DestVersion>
              <ProductName>MyProduct</ProductName>
              <FirmwareName>t3q5rkNm</FirmwareName>
              <ModuleName>module1234</ModuleName>
        </SimpleFirmwareInfo>
  </FirmwareInfo>
  <CurrentPage>1</CurrentPage>
  <Success>true</Success>
  <Total>1</Total>
</ListOTAFirmwareResponse>
```

`JSON` 格式

```
{
  "PageCount": 1,
  "PageSize": 10,
  "RequestId": "A01829CE-75A1-4920-B775-921146A1AB79",
  "FirmwareInfo": {
    "SimpleFirmwareInfo": [{
      "SrcVersion": "1.0.0",
      "FirmwareSign": "3d04ab6462633508606e5f3daac8****",
      "ProductKey": "a19mzPZ****",
      "Type": 0,
      "UtcModified": "2019-12-28T02:42:22.000Z",
      "SignMethod": "MD5",
      "UtcCreate": "2019-12-28T02:42:22.000Z",
      "FirmwareSize": 924,
      "Status": 0,
      "FirmwareId": "UfuxnwygsuSkVE0VCN****0100",
      "FirmwareDesc": "firmwareDesc",
      "FirmwareUrl": "https://iotx-ota-pre.oss-cn-shanghai.aliyuncs.com/ota/572ef2fd12ca4791a5b21a9eb948****/5E962CF83DB1495E8337E9C8A4D1****.bin",
      "DestVersion": "4.0.0",
      "ProductName": "MyProduct",
      "FirmwareName": "t3q5rkNm",
      "ModuleName": "module1234"
    }]
  },
  "CurrentPage": 1,
  "Success": true,
  "Total": 1
}
```


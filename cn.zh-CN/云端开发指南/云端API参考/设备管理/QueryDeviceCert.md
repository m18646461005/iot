# QueryDeviceCert

调用该接口查询设备的X.509证书。

## 限制说明

-   仅支持地域为华东2（上海），且认证方式为X.509证书的设备。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceCert&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceCert|系统规定参数。取值：QueryDeviceCert。 |
|DeviceName|String|是|light|设备名称。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|设备所属产品的ProductKey。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|DeviceCertInfo|Struct| |返回的证书信息列表。 |
|CertSN|String|636217374433\*\*\*\*|X.509证书ID。 |
|Certificate|String|tXHf4ezGEHcwdyMwoCDHGBmk9avi\*\*\*\*|X.509证书。 |
|PrivateKey|String|CqXL5h5ysRTA4NxjABjj0010fa\*\*\*\*|X.509证书密钥。 |
|Status|Integer|2|证书生成状态。

 -   **0**：生成中。
-   **1**：生成失败。
-   **2**：生成成功。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceCert
&ProductKey=alRedOt****
&DeviceName=device1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceCertResponse>
  <RequestId>57b144cf-09fc-4916-a272-a62902d5b207</RequestId>
  <Success>true</Success>
  <DeviceCertInfo>
        <Status>2</Status>
        <Certificate>tXHf4ezGEHcwdyMwoCDHGBmk9avi****</Certificate>
        <PrivateKey>CqXL5h5ysRTA4NxjABjj0010fa****</PrivateKey>
        <CertSN>636217374433****</CertSN>
  </DeviceCertInfo>
</QueryDeviceCertResponse>
```

`JSON` 格式

```
{
    "RequestId":"57b144cf-09fc-4916-a272-a62902d5b207",
    "Success": true,
    "DeviceCertInfo": {
        "Status": 2,
        "Certificate": "tXHf4ezGEHcwdyMwoCDHGBmk9avi****",
        "PrivateKey": "CqXL5h5ysRTA4NxjABjj0010fa****",
        "CertSN": "636217374433****"
    }
}
```


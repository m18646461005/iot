# RRpc

调用该接口向指定设备发送请求消息，并同步返回响应。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为1000。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=RRpc&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RRpc|系统规定参数。取值：RRpc。 |
|DeviceName|String|是|device1|要接收消息的设备名称。 |
|ProductKey|String|是|aldfeSe\*\*\*\*|要发送消息的产品Key。 |
|RequestBase64Byte|String|是|dGhpcyBpcyBhbiBleGFtcGxl|要发送的消息内容经过Base64编码得到的字符串格式数据，例如`dGhpcyBpcyBhbiBleGFtcGxl`。 |
|Timeout|Integer|是|1000|等待设备回复消息的时间，单位是毫秒，取值范围是1,000 ~8,000。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|Topic|String|否|/a1uZfYb\*\*\*\*/A\_Vol\*\*\*\*/user/update|使用自定义的RRPC相关Topic。需要设备端配合使用，请参见设备端开发[自定义Topic](~~90570~~)。

 不传入此参数，则使用系统默认的RRPC Topic。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|MessageId|Long|889455942124347392|成功发送请求消息后，云端生成的消息ID，用于标识该消息。 |
|PayloadBase64Byte|String|d29ybGQgaGVsbG8=|设备返回结果Base64编码后的值。 |
|RequestId|String|41C4265E-F05D-4E2E-AB09-E031F501AF7F|阿里云为该请求生成的唯一标识符。 |
|RrpcCode|String|SUCCESS|调用成功时，生成的调用返回码，标识请求状态。取值：

 -   **UNKNOWN**：系统异常
-   **SUCCESS**：成功
-   **TIMEOUT**：设备响应超时
-   **OFFLINE**：设备离线
-   **HALFCONN**：设备离线（设备连接断开，但是断开时间未超过一个心跳周期） |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=RRpc
&ProductKey=aldfeSe****
&DeviceName=device1
&RequestBase64Byte=dGhpcyBpcyBhbiBleGFtcGxl
&TimeOut=1000
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<?xml version='1.0' encoding='UTF-8'?>
  <RRpcResponse>
      <RequestId>41C4265E-F05D-4E2E-AB09-E031F501AF7F<RequestId/>
      <Success>true</Success>
      <RrpcCode>SUCCESS</RrpcCode>
      <PayloadBase64Byte>d29ybGQgaGVsbG8=</PayloadBase64Byte>
      <MessageId>889455942124347392</MessageId>
  </RRpcResponse>
```

`JSON` 格式

```
{
      "RrpcCode":"SUCCESS",
      "PayloadBase64Byte":"d29ybGQgaGVsbG8=",
      "MessageId":889455942124347392,
      "RequestId":"41C4265E-F05D-4E2E-AB09-E031F501AF7F",
      "Success":true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


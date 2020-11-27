# DeleteDevice

调用该接口删除指定设备。

## 限制说明

-   设备删除后，设备ID（IotId）将失效，与设备关联的其他信息也一并删除，您将无法执行与该设备关联的任何操作。
-   传入请求参数时，需传入IotId或ProductKey与DeviceName组合，用于指定设备。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=DeleteDevice&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteDevice|系统规定参数。取值：DeleteDevice。 |
|IotInstanceId|String|否|iot-cn-0pp1n8t\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|IotId|String|否|MpEKNuEUJzIORNANAWJX0010929900\*\*\*\*\*|要删除的设备ID。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。IotId作为设备唯一标识符，与**ProductKey**和**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |
|ProductKey|String|否|a1FlqIQ\*\*\*\*|要删除的设备所隶属的产品**ProductKey**。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|light|指定要删除的设备的名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.prod.NullProductKey|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|入参产品ID没有赋值。|调用失败时，返回的出错信息。 |
|RequestId|String|57b144cf-09fc-4916-a272-a62902d5b207|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|false|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=DeleteDevice
&ProductKey=a1rYuVF****
&DeviceName=device1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteDeviceResponse>
  <RequestId>57b144cf-09fc-4916-a272-a62902d5b207</RequestId>
  <Success>true</Success>
</DeleteDeviceResponse>
```

`JSON` 格式

```
{
  "RequestId":"57b144cf-09fc-4916-a272-a62902d5b207",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


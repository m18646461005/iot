# BatchAddThingTopo

调用该接口批量添加设备拓扑关系。

## 限制说明

-   单次调用最多可为一个网关添加10个子设备。
-   接口调用者必须是网关的所有者（Owner）。
-   单个阿里云账号调用该接口的QPS限流为5。子账号共享主账号配额。
-   如果传入的子设备已存在拓扑关系，则会将子设备原有的网关替换为当前网关。
-   任意一个子设备与网关的拓扑关系建立失败时，系统回滚，传入的所有子设备与当前网关建立拓扑关系失败。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=BatchAddThingTopo&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchAddThingTopo|系统规定参数。取值：BatchAddThingTopo。 |
|GwDeviceName|String|是|gateway|网关设备的名称。 |
|GwProductKey|String|是|a1vL7cp\*\*\*\*|网关设备所属的产品的ProductKey。 |
|TopoAddItem.N.DeviceName|String|是|light|要接入网关的子设备名称。 |
|TopoAddItem.N.ProductKey|String|是|a1BwAGV\*\*\*\*|要接入网关的子设备所属的产品ProductKey。 |
|TopoAddItem.N.Sign|String|是|C1C1606D61884C5F16C9EA6622E5\*\*\*\*|添加拓扑关系的签名。

 根据签名计算方式**SignMethod\(deviceSecret,content\)**，计算出的结果作为Sign的取值。

 其中，**content**是将所有提交给服务器的子设备参数（Sign、SignMethod除外），按照英文字母升序，依次排序拼接（无拼接符号）的结果。

 例如，如果传入的设备参数为**ClientId=868575026974305、DeviceName=868575026974305、ProductKey=a1PB5fp1234、SignMethod=hmacmd5，且deviceSecret=1234**，那么签名计算为`hmacmd5(1234, clientId868575026974305deviceName868575026974305productKeya1PB5fpX1234)`；签名计算结果为`C1C1606D61884C5F16C9EA6622E5****`。 |
|TopoAddItem.N.SignMethod|String|是|hmacMd5|签名方法。支持**hmacSha1**、**hmacSha256**、**hmacMd5**和**Sha256**（大小写不敏感）。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|TopoAddItem.N.Timestamp|String|否|1579335899000|UTC时间戳。非必选。如果传入该参数，则需包含到签名计算中。 |
|TopoAddItem.N.ClientId|String|否|a1BwAGV\*\*\*\*device1|设备端ID，可使用设备的SN码或MAC地址。非必选参数。如果传入该参数，则需包含到签名计算中。 |

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
https://iot.cn-shanghai.aliyuncs.com/?Action=BatchAddThingTopo
&GwProductKey=a1duisa****
&GwDeviceName=tydhnay16shc6
&TopoAddItem.1.ProductKey=a1rYuVF****
&TopoAddItem.1.DeviceName=SR8FiTu1R9tlUR2V1bmi
&TopoAddItem.1.Sign=dgj1609rD6IUGFCRkJKKdNKAE67h8****
&TopoAddItem.1.SignMethod=hmacMd5
&TopoAddItem.2.ProductKey=a1yrZMH****
&TopoAddItem.2.DeviceName=RkQ8CFtNpDok4BEunymt
&TopoAddItem.2.Sign=C1C1606D61884C5F16C9EA6622E5****
&TopoAddItem.2.SignMethod=hmacMd5
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<BatchAddThingTopoResponse>
  <RequestId>2E19BDAF-0FD0-4608-9F41-82D230CFEE38</RequestId>
  <Success>true</Success>
</BatchAddThingTopoResponse>
```

`JSON` 格式

```
{
  "RequestId": "2E19BDAF-0FD0-4608-9F41-82D230CFEE38",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


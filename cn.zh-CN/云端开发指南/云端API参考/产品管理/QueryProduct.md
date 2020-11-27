# QueryProduct

调用该接口查询指定产品的详细信息。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryProduct&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryProduct|系统规定参数。取值：QueryProduct。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|要查询的产品的ProductKey。ProductKey是物联网平台为新建产品颁发的产品Key，作为其全局唯一标识符。您可以在物联网平台控制台查看或调用[QueryProductList](~~69271~~)查看当前账号下所有产品的信息。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的产品信息详情。 |
|AliyunCommodityCode|String|iothub\_senior|产品版本，决定是否使用物模型功能。

 取值：

 -   **iothub**：不使用物模型。
-   **iothub\_senior**：使用物模型。 |
|AuthType|String|secret|产品下的设备接入物联网平台的认证方式。

 -   **secret**：设备密钥。
-   **id2**：ID²。
-   **x509**：X.509证书。 |
|CategoryKey|String|Lighting|产品所属品类的标识符。

 产品使用了物联网平台预定义的标准品类物模型会返回此参数。

 该参数为使用物模型的产品（AliyunCommodityCode=iothub\_senior）的特有参数。 |
|CategoryName|String|路灯照明|产品所属品类的名称。

 产品使用了物联网平台预定义的标准品类物模型会返回此参数。

 该参数为使用物模型的产品（AliyunCommodityCode=iothub\_senior）的特有参数。 |
|DataFormat|Integer|1|设备与云端之间的数据通信协议类型。该参数为使用物模型的产品（AliyunCommodityCode=iothub\_senior）的特有参数。

 取值：

 -   **0**：透传模式。使用自定义的串口数据格式。该模式下，设备可以上报原始数据（如二进制数据流）。阿里云物联网平台会运行您配置在云端的数据解析脚本，将原始数据转换成Alink JSON标准数据格式。
-   **1**：Alink JSON。阿里云物联网平台定义的设备与云端的数据交换协议，采用 JSON 格式。 |
|Description|String|智能路灯|产品描述。 |
|DeviceCount|Integer|0|该产品下的设备数量。 |
|GmtCreate|Long|1581595942000|该产品的创建时间。毫秒级时间戳。 |
|Id2|Boolean|false|该产品是否使用ID²认证。取值：

 -   **true**：使用ID²认证。
-   **false**：不使用ID²认证。 |
|NetType|Integer|3|产品下设备的联网方式。取值：

 -   **3**：Wi-Fi
-   **6**：Cellular（2G/3G/4G/5G）蜂窝网
-   **7**：Ethernet以太网。
-   **8**：其他 |
|NodeType|Integer|0|产品的节点类型。该参数为使用物模型的产品（AliyunCommodityCode=iothub\_senior）的特有参数。取值：

 -   **0**：设备。设备不能挂载子设备，可以直连IoT Hub，也可以作为网关的子设备连接IoT Hub。
-   **1**：网关。网关可以挂载子设备，具有子设备管理模块，维持子设备的拓扑关系，并且可以将拓扑关系同步到云端。 |
|Owner|Boolean|true|调用者是否是产品的拥有者。

 -   **true**：是。
-   **false**：不是。 |
|ProductKey|String|a1T27vz\*\*\*\*|产品的ProductKey。创建产品时，物联网平台为该产品颁发的全局唯一标识。 |
|ProductName|String|路灯|产品名称。 |
|ProductSecret|String|U5tW7i44uilc\*\*\*\*|产品密钥。 |
|ProductStatus|String|DEVELOPMENT\_STATUS|产品的状态。

 -   **DEVELOPMENT\_STATUS**：开发中。
-   **RELEASE\_STATUS**：产品已发布。 |
|ProtocolType|String|modbus|子设备接入网关的协议类型。

 此参数为使用物模型的产品（AliyunCommodityCode=iothub\_senior），且产品节点类型为要接入网关的设备的特有参数。取值：

 -   **modbus**：Modbus协议
-   **opc-ua**：OPC UA协议
-   **customize**：自定义协议
-   **ble**：BLE协议
-   **zigbee**：ZigBee协议 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E4F94B97-1D64-4080-BFD2-67461667AA43|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：表示调用成功。
-   **false**：表示调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryProduct
&ProductKey=a1BwAGV****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryProductResponse>
  <Data>
        <Owner>true</Owner>
        <CategoryName>路灯照明</CategoryName>
        <DataFormat>1</DataFormat>
        <ProductKey>a1BwAGV****</ProductKey>
        <ProductStatus>DEVELOPMENT_STATUS</ProductStatus>
        <GmtCreate>1581595942000</GmtCreate>
        <ProductSecret>U5tW7i44uilc****</ProductSecret>
        <NodeType>0</NodeType>
        <ProductName>路灯</ProductName>
        <DeviceCount>0</DeviceCount>
        <NetType>3</NetType>
        <AuthType>secret</AuthType>
        <CategoryKey>Lighting</CategoryKey>
        <Id2>false</Id2>
        <AliyunCommodityCode>iothub_senior</AliyunCommodityCode>
  </Data>
  <RequestId>DA5A3C45-D457-48ED-9A20-AEDEA8503401</RequestId>
  <Success>true</Success>
</QueryProductResponse>
```

`JSON` 格式

```
{
	"Data": {
		"Owner": true,
		"CategoryName": "路灯照明",
		"DataFormat": 1,
		"ProductKey": "a1BwAGV****",
		"ProductStatus": "DEVELOPMENT_STATUS",
		"GmtCreate": 1581595942000,
		"ProductSecret": "U5tW7i44uilc****",
		"NodeType": 0,
		"ProductName": "路灯",
		"DeviceCount": 0,
		"NetType": 3,
		"AuthType": "secret",
		"CategoryKey": "Lighting",
		"Id2": false,
		"AliyunCommodityCode": "iothub_senior"
	},
	"RequestId": "DA5A3C45-D457-48ED-9A20-AEDEA8503401",
	"Success": true
}
```


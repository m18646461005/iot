# CreateProduct

调用该接口新建产品。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=CreateProduct&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateProduct|系统规定参数。取值：CreateProduct。 |
|NodeType|Integer|是|0|产品的节点类型，取值：

 **0**：设备。设备不能挂载子设备。可以直连物联网平台，也可以作为网关的子设备连接物联网平台。

 **1**：网关。网关可以挂载子设备，具有子设备管理模块，维持子设备的拓扑关系，和将拓扑关系同步到物联网平台。 |
|ProductName|String|是|Light|为新建产品命名。产品名应满足以下限制：由4-30位中文、英文字母、数字和下划线（\_）组成（一个中文字符占两位）。

 **说明：** 产品名在当前账号下应保持唯一。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|DataFormat|Integer|否|1|数据格式。

 可选值：

 -   **0**：透传/自定义格式（CUSTOM\_FORMAT）
-   **1**：Alink协议（ALINK\_FORMAT） |
|Description|String|否|Product test|为新建产品添加描述信息。描述信息应在100字符以内。 |
|AliyunCommodityCode|String|否|iothub\_senior|产品版本类型。 目前仅支持创建使用物模型的产品，输入**iothub\_senior**。 |
|Id2|Boolean|否|false|是否使用ID²认证。

 可选值：

 -   **true**：开通ID²认证。
-   **false**：不开通ID²认证。

 不传入此参数，则默认为**false**，不开通ID²认证。

 **说明：** 仅华东2（上海）地域支持ID²认证方式。如果此参数值设置为**true**，但传入的**AuthType**参数值不是**id2**，系统将以**AuthType**参数值为准。 |
|CategoryId|Long|否|1|多余参数，请忽略。 |
|ProtocolType|String|否|modbus|设备接入网关的协议类型。

 使用物模型的产品（AliyunCommodityCode=iothub\_senior），且产品下的设备需通过网关接入物联网平台，需传入此参数。

 可选值：

 -   **modbus**：Modbus协议
-   **opc-ua**：OPC UA协议
-   **customize**：自定义协议
-   **ble**：BLE协议
-   **zigbee**：ZigBee协议 |
|NetType|String|否|WIFI|连网方式。

 使用物模型的产品（AliyunCommodityCode=iothub\_senior），且产品下的设备为网关或不接入网关的设备时，需传入此参数。

 可选值：

 -   **WIFI**： Wi-Fi
-   **CELLULAR**：蜂窝网
-   **ETHERNET**：以太网
-   **LORA**：LoRaWAN
-   **OTHER**：其他

 若不传入此参数，则默认为Wi-Fi。 |
|JoinPermissionId|String|否|8\*\*\*|LoRaWAN入网凭证ID。连网方式NetType选择为LORA时，该参数必需。

 请调用[QueryLoRaJoinPermissions](~~109293~~)

 查询您账号下的LoRaWAN入网凭证的**JoinPermissionId**。

 如果您还没有LoRaWAN入网凭证，请访问[物联网络管理平台](https://linkwan.console.aliyun.com/join-permission-authorization)创建。 |
|ResourceGroupId|String|否|rg-acfmxazb4ph\*\*\*\*|产品所属资源组ID。传入此参数，则将新建产品划归到某个资源组。

 可在[资源管理控制台](https://resourcemanager.console.aliyun.com/resource-groups)查看资源组ID。 |
|AuthType|String|否|secret|产品下的设备接入物联网平台的认证方式。

 -   **secret**：使用设备密钥进行设备身份认证。更多信息，请参见[MQTT-TCP连接通信](~~73742~~)。
-   **id2**：使用物联网设备身份认证ID²。

**说明：** 仅华东2（上海）地域支持ID²认证方式。连网方式NetType为LORA的产品不支持ID²认证方式。 选择使用ID²认证，需购买ID²服务。更多信息，请参见[使用ID²认证](~~141661~~)。

-   **x509**：使用设备X.509证书进行设备身份认证。

**说明：** 仅华东2（上海）地域支持X.509证书。连网方式NetType为LORA的产品不支持X.509证书。使用X.509证书的设备端配置说明，请参见[使用X.509证书认证](~~140588~~)。


 若不传入此参数，默认值为**secret**。 |
|CategoryKey|String|否|Lighting|产品品类的标识符。如果传入此参数，创建的产品将使用指定品类的物模型；不传入，则不使用任何品类的标准物模型。

 调用[ListThingTemplates](~~150316~~)，从返回结果中查看物联网平台预定义的品类信息，获取CategoryKey的取值。 |
|PublishAuto|Boolean|否|false|是否在产品创建后自动发布物模型。

 -   **true**：发布。
-   **false**：不发布。

 不传入此参数，取默认值为**true**。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的新建产品信息。 |
|AliyunCommodityCode|String|iothub\_senior|产品类型。

 -   iothub\_senior：使用物模型。
-   iothub：不使用物模型。 |
|AuthType|String|secret|产品下的设备接入物联网平台的认证方式。

 -   secret：使用设备密钥进行设备身份认证。
-   id2：使用物联网设备身份认证ID²。
-   x509：使用设备X.509证书进行设备身份认证。 |
|DataFormat|Integer|1|产品类型数据格式。

 -   0：透传/自定义格式（CUSTOM\_FORMAT）。
-   1：Alink协议（ALINK\_FORMAT）。

 **说明：** 此参数为使用物模型的产品（AliyunCommodityCode=iothub\_senior）特有参数。 |
|Description|String|Product test|产品描述信息。 |
|Id2|Boolean|false|是否使用ID²认证。

 -   true：开通ID²认证。
-   false：不开通ID²认证。 |
|NodeType|Integer|0|产品的节点类型，取值：

 -   0：设备。设备不能挂载子设备。可以直连物联网平台，也可以作为网关的子设备连接物联网平台。
-   1：网关。网关可以挂载子设备，具有子设备管理模块，维持子设备的拓扑关系，和将拓扑关系同步到物联网平台。

 **说明：** 此参数为使用物模型的产品（AliyunCommodityCode=iothub\_senior）特有参数。 |
|ProductKey|String|a1FlqIQ\*\*\*\*|物联网平台为新建产品颁发的产品Key，作为该产品的全局唯一标识。

 **说明：** 请妥善保管新建产品的ProductKey。在其他操作中会用到该信息。 |
|ProductName|String|Test|产品的名称。 |
|ProductSecret|String|U5tW7i44uilc\*\*\*\*|产品密钥。 |
|ProtocolType|String|modbus|设备接入网关协议类型。

 **说明：** 此参数为使用物模型的产品（AliyunCommodityCode=iothub\_senior）特有参数。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|ProductKey|String|a1FlqIQ\*\*\*\*|产品的ProductKey，物联网平台为产品颁发的唯一标识符。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https:/iot.cn-shanghai.aliyuncs.com/?Action=CreateProduct
&AliyunCommodityCode=iothub_senior
&AuthType=secret
&DataFormat=1
&Description=Product test
&NodeType=0
&ResourceGroupId=rg-acfmxazb4ph****
&ProductName=Test
&ProtocolType=modbus
&CategoryKey=Lighting
&PublishAuto=false
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateProductResponse>
      <Data>
            <Description>Product test</Description>
            <DataFormat>1</DataFormat>
            <ProtocolType>modbus</ProtocolType>
            <ProductKey>a1FlqIQ****</ProductKey>
            <ProductSecret>U5tW7i44uilc****</ProductSecret>
            <NodeType>0</NodeType>
            <ProductName>Test</ProductName>
            <AliyunCommodityCode>iothub_senior</AliyunCommodityCode>
            <AuthType>secret</AuthType>
            <ResourceGroupId>rg-acfmxazb4ph****</ResourceGroupId>
      </Data>
      <ProductKey>a1FlqIQ****</ProductKey>
      <RequestId>E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565</RequestId>
      <Success>true</Success>
</CreateProductResponse>
```

`JSON` 格式

```
{
  "Data": {
    "Description": "Product test",
    "DataFormat": 1,
    "ProtocolType": "modbus",
    "ProductKey": "a1FlqIQ****",
    "ProductSecret": "U5tW7i44uilc****",
    "NodeType": 0,
    "ProductName": "Test",
    "AliyunCommodityCode": "iothub_senior",
    "AuthType": "secret",
    "ResourceGroupId": "rg-acfmxazb4ph****"
  },
  "ProductKey": "a1FlqIQ****",
  "RequestId": "E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


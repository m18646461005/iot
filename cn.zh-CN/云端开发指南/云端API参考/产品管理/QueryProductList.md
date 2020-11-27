# QueryProductList

调用该接口查看所有产品列表。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryProductList&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryProductList|系统规定参数。取值：QueryProductList。 |
|CurrentPage|Integer|是|1|指定显示返回结果中的第几页。 |
|PageSize|Integer|是|2|指定返回结果中每页显示的产品数量，最大值是200。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|AliyunCommodityCode|String|否|iothub\_senior|指定要查看的产品类型，取值：

 -   **iothub\_senior**：使用物模型版产品。
-   **iothub**：不使用物模型版产品。

 **说明：** 如果不传入该参数，则返回所有产品的列表。 |
|ResourceGroupId|String|否|rg-acfmxazb4ph\*\*\*\*|产品所属资源组ID。 可在[资源管理控制台](https://resourcemanager.console.aliyun.com/resource-groups)查看资源组信息。

 若不传入此参数，则查询账号下所有资源组中的产品。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的产品信息。具体信息请参见以下参数。 |
|CurrentPage|Integer|1|当前页号。 |
|List|Array of ProductInfo| |产品信息列表。

 **说明：** 返回的产品信息按照产品创建时间倒序排列。 |
|ProductInfo| | | |
|AuthType|String|secret|产品下的设备接入物联网平台的认证方式。

 -   secret：设备密钥。
-   id2：ID²。
-   x509：X.509证书。 |
|DataFormat|Integer|1|设备与云端之间的数据通信协议类型。该参数为使用物模型的产品（AliyunCommodityCode=iothub\_senior）的特有参数。

 取值：

 -   **0**：透传模式。使用自定义的串口数据格式。该模式下，设备可以上报原始数据（如二进制数据流）。阿里云物联网平台会运行您配置在云端的数据解析脚本，将原始数据转换成Alink JSON标准数据格式。
-   **1**：Alink JSON。阿里云物联网平台定义的设备与云端的数据交换协议，采用 JSON 格式。 |
|Description|String|This is a test product.|产品描述。 |
|DeviceCount|Integer|128|产品下的设备数量。 |
|GmtCreate|Long|1581595942000|该产品的创建时间。毫秒值时间戳。 |
|NodeType|Integer|0|产品的节点类型。该参数为使用物模型的产品（AliyunCommodityCode=iothub\_senior）的特有参数。取值：

 -   **0**：设备。设备不能挂载子设备，可以直连IoT Hub，也可以作为网关的子设备连接IoT Hub。
-   **1**：网关。网关可以挂载子设备，具有子设备管理模块，维持子设备的拓扑关系，并且可以将拓扑关系同步到云端。 |
|ProductKey|String|a1T27vz\*\*\*\*|产品的ProductKey。创建产品时，物联网平台为该产品颁发的全局唯一标识。 |
|ProductName|String|路灯|产品名称。 |
|PageCount|Integer|92|总页数。 |
|PageSize|Integer|2|每页显示的产品数。 |
|Total|Integer|184|产品总数。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|4B4ECF2C-6222-42EC-A4B5-C12202E71CEA|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：表示调用成功。
-   **false**：表示调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryProductList
&CurrentPage=1
&PageSize=2
&ResourceGroupId=rg-acfmxazb4ph****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryProductListResponse>
  <Data>
        <PageCount>92</PageCount>
        <PageSize>2</PageSize>
        <List>
              <ProductInfo>
                    <DataFormat>1</DataFormat>
                    <ProductKey>a1A0D4t****</ProductKey>
                    <NodeType>0</NodeType>
                    <ProductName>路灯产品</ProductName>
                    <DeviceCount>1</DeviceCount>
                    <GmtCreate>1569233025000</GmtCreate>
                    <AuthType>secret</AuthType>
              </ProductInfo>
              <ProductInfo>
                    <DataFormat>1</DataFormat>
                    <ProductKey>a1dEvuQ****</ProductKey>
                    <NodeType>0</NodeType>
                    <ProductName>子设备custom</ProductName>
                    <DeviceCount>0</DeviceCount>
                    <GmtCreate>1568690432000</GmtCreate>
                    <AuthType>secret</AuthType>
              </ProductInfo>
        </List>
        <CurrentPage>1</CurrentPage>
        <Total>184</Total>
  </Data>
  <RequestId>4B4ECF2C-6222-42EC-A4B5-C12202E71CEA</RequestId>
  <Success>true</Success>
</QueryProductListResponse>
```

`JSON` 格式

```
{
  "Data": {
    "PageCount": 92, 
    "PageSize": 2, 
    "List": {
      "ProductInfo": [
        {
          "DataFormat": 1, 
          "ProductKey": "a1A0D4t****", 
          "NodeType": 0, 
          "ProductName": "路灯产品", 
          "DeviceCount": 1, 
          "GmtCreate": 1569233025000, 
          "AuthType": "secret"
        }, 
        {
          "DataFormat": 1, 
          "ProductKey": "a1dEvuQ****", 
          "NodeType": 0, 
          "ProductName": "子设备custom", 
          "DeviceCount": 0, 
          "GmtCreate": 1568690432000,
          "AuthType": "secret"
        }
      ]
    }, 
    "CurrentPage": 1, 
    "Total": 184
  }, 
  "RequestId": "4B4ECF2C-6222-42EC-A4B5-C12202E71CEA", 
  "Success": true
}
```


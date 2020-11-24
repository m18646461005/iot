# ListOTAModuleVersionsByDevice

调用该接口查询设备上报过的OTA模块版本列表。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=ListOTAModuleVersionsByDevice&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListOTAModuleVersionsByDevice|系统规定参数。取值：ListOTAModuleVersionsByDevice。 |
|CurrentPage|Integer|是|1|指定从返回结果中的第几页开始显示。默认值是1。 |
|PageSize|Integer|是|10|指定返回结果中每页显示的模块版本数量。数量限制：每页最多可显示200条。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数；您购买的企业实例需传入此参数。 |
|ProductKey|String|否|aluctKe\*\*\*\*|要查询设备所属的产品**ProductKey**。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|newdevice|指定要查询设备的名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要查询的设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|CurrentPage|Integer|1|当前页面号。 |
|Data|Array of SimpleOTAModuleInfo| |调用成功时，返回的设备上报的模块版本信息。更多信息，请参见以下**SimpleOTAModuleInfo**。 |
|SimpleOTAModuleInfo| | | |
|DeviceName|String|newDevice|设备名称。 |
|IotId|String|QjIFT\*\*\*000101|设备ID。 |
|ModuleName|String|barcodeScanner|模块名称。 |
|ModuleVersion|String|1.0|设备上报的模块版本。 |
|ProductKey|String|aluctKe\*\*\*\*|设备所属产品的**ProductKey**。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|PageCount|Integer|1|返回的总页数。 |
|PageSize|Integer|10|每页显示的模块版本数量。 |
|RequestId|String|291438BA-6E10-4C4C-B761-243B9A0D324F|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|Total|Integer|10|设备上报的模块版本总数。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=ListOTAModuleVersionsByDevice
&CurrentPage=1
&PageSize=10
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListOTAModuleVersionsByDeviceResponse>
  <requestId>67AF7881-704C-40CC-B296-72F91380A117</requestId>
  <success>true</success>
  <code></code>
  <errorMessage></errorMessage>
  <PageSize>10</PageSize>
  <PageCount>1</PageCount>
  <CurrentPage>1</CurrentPage>
  <Total>1</Total>
  <Data>
        <SimpleOTAModuleInfo>
              <IotId>QjIFT***000101</IotId>
              <ModuleVersion>1.6940.1</ModuleVersion>
              <ModuleName>default</ModuleName>
              <ProductKey>a14***S</ProductKey>
              <DeviceName>newDevice</DeviceName>
        </SimpleOTAModuleInfo>
  </Data>
</ListOTAModuleVersionsByDeviceResponse>
```

`JSON` 格式

```
{
    "requestId": "67AF7881-704C-40CC-B296-72F91380A117",
    "success": true,
    "code": "",
    "errorMessage": null,
    "PageSize": 10,
    "PageCount": 1,
    "CurrentPage": 1,
    "Total": 1,
    "Data": {
        "SimpleOTAModuleInfo": [
            {
                "IotId": "QjIFT***000101",
                "ModuleVersion": "1.6940.1",
                "ModuleName": "default",
                "ProductKey": "a14***S",
                "DeviceName": "newDevice"
            }
        ]
    }
}
```


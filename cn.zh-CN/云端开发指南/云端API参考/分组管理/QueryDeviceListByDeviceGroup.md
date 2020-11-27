# QueryDeviceListByDeviceGroup

调用该接口查询分组中的设备列表。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为5。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceListByDeviceGroup&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceListByDeviceGroup|系统规定参数。取值：QueryDeviceListByDeviceGroup。 |
|GroupId|String|是|7DIgqIl1Ijnh\*\*\*\*|分组ID，分组的全局唯一标识符。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|PageSize|Integer|否|10|指定返回结果中，每页显示的设备数量。 |
|CurrentPage|Integer|否|1|指定显示查询结果中的第几页。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Array of SimpleDeviceInfo| |调用成功时，返回的设备列表信息数据。详情请参见以下SimpleDeviceInfo。 |
|SimpleDeviceInfo| | | |
|DeviceName|String|ios\_1207\_08|设备名称。 |
|IotId|String|TfmUAeJjQQhCPH84UVNn0010c6\*\*\*\*|物联网平台为该设备颁发的ID，作为该设备的唯一标识符。 |
|ProductKey|String|a1hWjHD\*\*\*\*|设备所属的产品Key。 |
|ProductName|String|WIFIdevice|设备所属的产品名称。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|Page|Integer|1|当前页码。 |
|PageCount|Integer|1|总页数。 |
|PageSize|Integer|10|每页所显示的设备数量。 |
|RequestId|String|B1A921D9-1061-4D45-9F12-EA6B0FDEDE30|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|Total|Integer|3|设备总数。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceListByDeviceGroup
&GroupId=7DIgqIl1Ijnh****
&CurrentPage=1
&PageSize=10
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceListByDeviceGroupResponse>
      <PageCount>1</PageCount>
      <Data>
            <SimpleDeviceInfo>
                  <DeviceName>ios_1207_08</DeviceName>
                  <ProductKey>a1hWjHD****</ProductKey>
                  <ProductName>WIFIdevice</ProductName>
                  <IotId>TfmUAeJjQQhCPH84UVNn0010c6****</IotId>
            </SimpleDeviceInfo>
            <SimpleDeviceInfo>
                  <DeviceName>ios_1207_07</DeviceName>
                  <ProductKey>a1hWjHD****</ProductKey>
                  <ProductName>WIFIgateway</ProductName>
                  <IotId>wVPeAksaboXBlRgvZNHQ001031****</IotId>
            </SimpleDeviceInfo>
            <SimpleDeviceInfo>
                  <DeviceName>E1IPK25iL4CTOwnuI2yt</DeviceName>
                  <ProductKey>a1mV8bK****</ProductKey>
                  <ProductName>yanlv</ProductName>
                  <IotId>E1IPK25iL4CTOwnuI2yt001059****</IotId>
            </SimpleDeviceInfo>
      </Data>
      <PageSize>10</PageSize>
      <Page>1</Page>
      <RequestId>B1A921D9-1061-4D45-9F12-EA6B0FDEDE30</RequestId>
      <Success>true</Success>
      <Total>3</Total>
</QueryDeviceListByDeviceGroupResponse>
```

`JSON` 格式

```
{
  "PageCount": 1,
  "Data": {
    "SimpleDeviceInfo": [
      {
        "DeviceName": "ios_1207_08",
        "ProductKey": "a1hWjHD****",
        "ProductName": "WIFIdevice",
        "IotId": "TfmUAeJjQQhCPH84UVNn0010c6****"
      },
      {
        "DeviceName": "ios_1207_07",
        "ProductKey": "a1hWjHD****",
        "ProductName": "WIFIgateway",
        "IotId": "wVPeAksaboXBlRgvZNHQ001031****"
      },
      {
        "DeviceName": "E1IPK25iL4CTOwnuI2yt",
        "ProductKey": "a1mV8bK****",
        "ProductName": "yanlv",
        "IotId": "E1IPK25iL4CTOwnuI2yt001059****"
      }
    ]
  },
  "PageSize": 10,
  "Page": 1,
  "RequestId": "B1A921D9-1061-4D45-9F12-EA6B0FDEDE30",
  "Success": true,
  "Total": 3
}
```


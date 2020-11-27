# QueryDevice

调用该接口查询指定产品下的所有设备列表。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDevice&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDevice|系统规定参数。取值：QueryDevice。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|要查询的设备所属产品的ProductKey。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|PageSize|Integer|否|10|指定返回结果中每页显示的记录数量，最大值是50。默认值是10。 |
|CurrentPage|Integer|否|1|指定显示返回结果中的第几页的内容。默认值是 1。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Array of DeviceInfo| |调用成功时，返回设备信息列表（**DeviceId**）。

 **说明：** 返回的设备信息按照设备创建时间倒序排列。 |
|DeviceInfo| | | |
|DeviceId|String|dwnS41bhNxjslDAI\*\*\*\*|设备ID（旧版参数）。

 **说明：** 该参数是旧版本遗留参数，已无实际作用，不能用来标识设备。目前，有效的设备标识符为**IotId**和**ProductKey**与**DeviceName**组合。 |
|DeviceName|String|light|设备名称。 |
|DeviceSecret|String|sLefbFmN9SYfnWLJTePG893XNuRV\*\*\*\*|设备密钥。 |
|DeviceStatus|String|ONLINE|设备状态。取值：

 -   **ONLINE**：设备在线。
-   **OFFLINE**：设备离线。
-   **UNACTIVE**：设备未激活。
-   **DISABLE**：设备已禁用。 |
|DeviceType|String|Lighting|设备所属产品的品类。

 **说明：** 目前不返回此参数。 |
|GmtCreate|String|Wed, 20-Feb-2019 02:16:09 GMT|设备创建时间，GMT格式。 |
|GmtModified|String|Wed, 20-Feb-2019 02:16:09 GMT|设备信息最后一次更新时的时间，GMT格式。 |
|IotId|String|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。 |
|Nickname|String|智能灯设备|设备的备注名称。 |
|ProductKey|String|a1BwAGV\*\*\*\*|设备所隶属的产品ProductKey。 |
|UtcCreate|String|2019-02-20T02:16:09.000Z|设备创建时间，UTC格式。 |
|UtcModified|String|2019-02-20T02:16:09.000Z|设备信息最后一次更新时的时间，UTC格式。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|Page|Integer|1|当前页面号。 |
|PageCount|Integer|1|总页数。 |
|PageSize|Integer|10|每页显示的设备数。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|Total|Integer|2|设备总数。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDevice
&ProductKey=aldafD****
&PageSize=10
&CurrentPage=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceResponse>
  <PageCount>1</PageCount>
  <Data>
        <DeviceInfo>
              <DeviceId>Av8NGHGtwPrH9BYG****</DeviceId>
              <DeviceName>Av8NGHGtwPrH9BYGLMBi</DeviceName>
              <ProductKey>a1dafDE****</ProductKey>
              <DeviceSecret>d7GYhf5hfcPHDe1bXSd3n9MjO1G3****</DeviceSecret>
              <UtcModified>2019-02-20T02:16:09.000Z</UtcModified>
              <GmtCreate>Wed, 20-Feb-2019 02:16:09 GMT</GmtCreate>
              <UtcCreate>2019-02-20T02:16:09.000Z</UtcCreate>
              <GmtModified>Wed, 20-Feb-2019 02:16:09 GMT</GmtModified>
              <IotId>Av8NGHGtwPrH9BYGLMBi00****</IotId>
              <DeviceStatus>UNACTIVE</DeviceStatus>
              <Nickname>SensorInShanghai</Nickname>
        </DeviceInfo>
        <DeviceInfo>
              <DeviceId>zNIcSmWQ9BPJlmkj****</DeviceId>
              <DeviceName>zNIcSmWQ9BPJlmkjn3H1</DeviceName>
              <ProductKey>a1dafDE****</ProductKey>
              <DeviceSecret>C27XXmC18yLIEDXvUj6FSlvgO7ag****</DeviceSecret>
              <UtcModified>2019-02-20T02:16:09.000Z</UtcModified>
              <GmtCreate>Wed, 20-Feb-2019 02:16:09 GMT</GmtCreate>
              <UtcCreate>2019-02-20T02:16:09.000Z</UtcCreate>
              <GmtModified>Wed, 20-Feb-2019 02:16:09 GMT</GmtModified>
              <IotId>zNIcSmWQ9BPJlmkjn3H100****</IotId>
              <DeviceStatus>UNACTIVE</DeviceStatus>
              <Nickname>DriverInShanghai</Nickname>
        </DeviceInfo>
  </Data>
  <Page>1</Page>
  <PageSize>10</PageSize>
  <RequestId>CD9E5F99-A095-4A05-9256-D924EA3075E8</RequestId>
  <Success>true</Success>
  <Total>2</Total>
</QueryDeviceResponse>
```

`JSON` 格式

```
{
  "PageCount": 1, 
  "Data": {
    "DeviceInfo": [
      {
        "DeviceId": "Av8NGHGtwPrH9BYG****", 
        "DeviceName": "Av8NGHGtwPrH9BYGLMBi", 
        "ProductKey": "a1dafDE****", 
        "DeviceSecret": "d7GYhf5hfcPHDe1bXSd3n9MjO1G3****", 
        "UtcModified": "2019-02-20T02:16:09.000Z", 
        "GmtCreate": "Wed, 20-Feb-2019 02:16:09 GMT", 
        "UtcCreate": "2019-02-20T02:16:09.000Z", 
        "GmtModified": "Wed, 20-Feb-2019 02:16:09 GMT", 
        "IotId": "Av8NGHGtwPrH9BYGLMBi00****", 
        "DeviceStatus": "UNACTIVE", 
        "Nickname": "SensorInShanghai"
      }, 
      {
        "DeviceId": "zNIcSmWQ9BPJlmkj****", 
        "DeviceName": "zNIcSmWQ9BPJlmkjn3H1", 
        "ProductKey": "a1dafDE****", 
        "DeviceSecret": "C27XXmC18yLIEDXvUj6FSlvgO7ag****", 
        "UtcModified": "2019-02-20T02:16:09.000Z", 
        "GmtCreate": "Wed, 20-Feb-2019 02:16:09 GMT", 
        "UtcCreate": "2019-02-20T02:16:09.000Z", 
        "GmtModified": "Wed, 20-Feb-2019 02:16:09 GMT", 
        "IotId": "zNIcSmWQ9BPJlmkjn3H100****", 
        "DeviceStatus": "UNACTIVE", 
        "Nickname": "DriverInShanghai"
      }
    ]
  }, 
  "Page": 1, 
  "PageSize": 10, 
  "RequestId": "CD9E5F99-A095-4A05-9256-D924EA3075E8", 
  "Success": true, 
  "Total": 2
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


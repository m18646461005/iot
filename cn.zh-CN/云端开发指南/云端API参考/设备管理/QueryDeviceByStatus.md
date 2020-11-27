# QueryDeviceByStatus

调用该接口根据设备状态查询设备列表。

## 限制说明

-   设备状态变更后，新的状态数据会在变更后10秒内生效。变更数据生效后，才能根据新状态查询；变更数据生效前，根据原状态仍能查询到该设备。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceByStatus&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceByStatus|系统规定参数。取值：QueryDeviceByStatus。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|设备所属的产品ProductKey。 |
|Status|Integer|否|1|设备状态。 可选值：

 -   **0**：未激活
-   **1**：在线
-   **3**：离线
-   **8**：已禁用 |
|CurrentPage|Integer|否|1|指定从返回结果中的第几页开始显示。 |
|PageSize|Integer|否|10|指定返回结果中每页显示的记录数量，最大值是50。 |
|BizTenantId|String|否|wdpznyrgac\*\*\*\*|租户ID。 |
|ResourceGroupId|String|否|rg-acfm4l5tcwd\*\*\*|设备所属资源组ID。资源组ID可在控制台上查看。

 **说明：** 传入此参数，则只查询指定资源组内指定状态的设备；不传入，则查询账号下指定状态的全部设备。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Array of SimpleDeviceInfo| |调用成功时，返回的设备信息列表（**SimpleDeviceInfo**）。 |
|SimpleDeviceInfo| | | |
|DeviceName|String|light|设备名称。 |
|DeviceSecret|String|sLefbFmN9SYfnWLJTePG893XNuRV\*\*\*\*|设备密钥。 |
|GmtCreate|String|Wed, 20-Feb-2019 02:16:09 GMT|设备创建时的时间，GMT格式。 |
|GmtModified|String|Wed, 20-Feb-2019 02:16:09 GMT|设备信息最后一次修改时的时间，GMT格式。 |
|IotId|String|Av8NGHGtwPrH9BYGLMBi00\*\*\*\*|设备ID。 |
|Nickname|String|SensorInShanghai|设备的备注名称。 |
|ProductKey|String|a1BwAGV\*\*\*\*|设备所属产品的ProductKey。 |
|Status|String|ONLINE|设备状态。 取值：

 -   **UNACTIVE**：未激活。
-   **ONLINE**：在线。
-   **OFFLINE**：离线。
-   **DISABLE**：已禁用。 |
|UtcCreate|String|2019-02-20T02:16:09.000Z|设备创建时的时间，UTC格式。 |
|UtcModified|String|2019-02-20T02:16:09.000Z|设备信息最后一次修改时的时间，UTC格式。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|Page|Integer|1|当前页码。 |
|PageCount|Integer|1|总页数。 |
|PageSize|Integer|10|每页显示的设备数。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|Total|Integer|2|查询到的设备总数。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceByStatus
&ProductKey=aldafD****
&Status=0
&PageSize=10
&CurrentPage=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceByStatusResponse>
      <RequestId>CD9E5F99-A095-4A05-9256-D924EA3075E8</RequestId>
      <Success>true</Success>
      <CurrentPage>1</CurrentPage>
      <PageSize>10</PageSize>
      <TotalPageCount>1</TotalPageCount>
      <TotalCount>2</TotalCount>
      <Data>
            <SimpleDeviceInfo>
                  <IotId>Av8NGHGtwPrH9BYGLMBi00****</IotId>
                  <DeviceName>Av8NGHGtwPrH9BYGLMBi</DeviceName>
                  <ProductKey>a1dafDE****</ProductKey>
                  <DeviceSecret>d7GYhf5hfcPHDe1bXSd3n9MjO1G3****</DeviceSecret>
                  <UtcModified>2019-02-20T02:16:09.000Z</UtcModified>
                  <GmtCreate>Wed, 20-Feb-2019 02:16:09 GMT</GmtCreate>
                  <UtcCreate>2019-02-20T02:16:09.000Z</UtcCreate>
                  <GmtModified>Wed, 20-Feb-2019 02:16:09 GMT</GmtModified>
                  <Status>UNACTIVE</Status>
                  <Nickname>SensorInShanghai</Nickname>
            </SimpleDeviceInfo>
            <SimpleDeviceInfo>
                  <IotId>zNIcSmWQ9BPJlmkjn3H100****</IotId>
                  <DeviceName>zNIcSmWQ9BPJlmkjn3H1</DeviceName>
                  <ProductKey>a1dafDE****</ProductKey>
                  <DeviceSecret>C27XXmC18yLIEDXvUj6FSlvgO7ag****</DeviceSecret>
                  <UtcModified>2019-02-20T02:16:09.000Z</UtcModified>
                  <GmtCreate>Wed, 20-Feb-2019 02:16:09 GMT</GmtCreate>
                  <UtcCreate>2019-02-20T02:16:09.000Z</UtcCreate>
                  <GmtModified>Wed, 20-Feb-2019 02:16:09 GMT</GmtModified>
                  <DeviceStatus>UNACTIVE</DeviceStatus>
                  <Nickname>DriverInShanghai</Nickname>
            </SimpleDeviceInfo>
      </Data>
</QueryDeviceByStatusResponse>
```

`JSON` 格式

```
{
  "RequestId": "CD9E5F99-A095-4A05-9256-D924EA3075E8", 
  "Success": true,  
  "CurrentPage": 1, 
  "PageSize": 10, 
  "TotalPageCount": 1,
  "TotalCount": 2,
  "Data": {
    "SimpleDeviceInfo": [
      {
        "IotId": "Av8NGHGtwPrH9BYGLMBi00****", 
        "DeviceName": "Av8NGHGtwPrH9BYGLMBi", 
        "ProductKey": "a1dafDE****", 
        "DeviceSecret": "d7GYhf5hfcPHDe1bXSd3n9MjO1G3****", 
        "UtcModified": "2019-02-20T02:16:09.000Z", 
        "GmtCreate": "Wed, 20-Feb-2019 02:16:09 GMT", 
        "UtcCreate": "2019-02-20T02:16:09.000Z", 
        "GmtModified": "Wed, 20-Feb-2019 02:16:09 GMT", 
        "Status": "UNACTIVE", 
        "Nickname": "SensorInShanghai"
      }, 
      {
        "IotId": "zNIcSmWQ9BPJlmkjn3H100****", 
        "DeviceName": "zNIcSmWQ9BPJlmkjn3H1", 
        "ProductKey": "a1dafDE****", 
        "DeviceSecret": "C27XXmC18yLIEDXvUj6FSlvgO7ag****", 
        "UtcModified": "2019-02-20T02:16:09.000Z", 
        "GmtCreate": "Wed, 20-Feb-2019 02:16:09 GMT", 
        "UtcCreate": "2019-02-20T02:16:09.000Z", 
        "GmtModified": "Wed, 20-Feb-2019 02:16:09 GMT", 
        "DeviceStatus": "UNACTIVE", 
        "Nickname": "DriverInShanghai"
      }
    ]
  }  
}
```


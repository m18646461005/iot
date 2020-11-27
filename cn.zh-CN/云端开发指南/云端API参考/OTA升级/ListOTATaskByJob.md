# ListOTATaskByJob

调用该接口查询指定升级批次下的设备升级作业列表。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=ListOTATaskByJob&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListOTATaskByJob|系统规定参数。取值：ListOTATaskByJob。 |
|JobId|String|是|7glPHmaDYLAYMD1HHutT02\*\*\*\*|升级批次ID，升级批次的唯一标识符。您调用[CreateOTAVerifyJob](~~147480~~)、[CreateOTAStaticUpgradeJob](~~147496~~)或[CreateOTADynamicUpgradeJob](~~147887~~)返回的**JobId**。您也可以在物联网平台控制台上固件的**固件详情**页查看。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|PageSize|Integer|否|10|指定返回结果中，每页显示的设备升级作业数量。最大限制：100。 |
|TaskStatus|String|否|FAILED|传入此参数，则查询指定升级状态下的设备升级作业。

 -   **QUEUED**：待推送。
-   **NOTIFIED**：已推送。
-   **IN\_PROGRESS**：升级中。
-   **SUCCEEDED**：升级成功。
-   **FAILED**：升级失败。
-   **CANCELED**：已取消。

 不传入此参数，则查询指定升级批次下的全部设备升级作业。 |
|CurrentPage|Integer|否|1|指定从返回结果中的第几页开始显示。页数从1开始排序。 |
|DeviceNames.N|RepeatList|否|device1|指定查询的设备名称列表。

 **说明：**

-   最多传入设备名称50个。
-   如果传入该参数，则无需传入**PageSize**和**CurrentPage**。如果您同时传入**DeviceNames.N**、**PageSize**和**CurrentPage**，则以**DeviceNames.N**为准。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|CurrentPage|Integer|1|当前页码。 |
|Data|Array of SimpleOTATaskInfo| |调用成功时，返回的设备升级作业信息。更多信息，请参见**SimpleOTATaskInfo**下的参数。 |
|SimpleOTATaskInfo| | | |
|DestVersion|String|1.0.1|升级的目标固件版本。 |
|DeviceName|String|testDevice2|设备名称。 |
|FirmwareId|String|q3j9OYBjUAZMv1hlMgdo03\*\*\*\*|固件ID。 |
|IotId|String|nadRdeffljdEndlfadgadfse\*\*\*\*|设备ID。 |
|JobId|String|7glPHmaDYLAYMD1HHutT02\*\*\*\*|升级批次ID。 |
|ProductKey|String|a1GUfrM\*\*\*\*|设备所属产品的ProductKey。 |
|ProductName|String|MyProduct|设备所属产品的名称。 |
|Progress|String|0.00|当前的升级进度。 |
|SrcVersion|String|1.0.0|设备的原固件版本。 |
|TaskDesc|String|report version is not conform|升级作业描述信息。当设备升级超时、升级作业被取消等场景下，该参数承载具体的错误信息。 |
|TaskId|String|y3tOmCDNgpR8F9jnVEzC01\*\*\*\*|设备升级作业ID。 |
|TaskStatus|String|FAILED|设备升级状态。

 -   **QUEUED**：待推送。
-   **NOTIFIED**：已推送。
-   **IN\_PROGRESS**：升级中。
-   **SUCCEEDED**：升级成功。
-   **FAILED**：升级失败。
-   **CANCELED**：已取消。 |
|UtcCreate|String|2019-11-04T03:38:22.000Z|升级作业创建时的时间，UTC格式。 |
|UtcModified|String|2019-11-04T03:38:22.000Z|升级作业最后一次修改时的时间，UTC格式。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|PageCount|Integer|1|总页数。 |
|PageSize|Integer|10|每页显示的设备升级作业数量。 |
|RequestId|String|A59D3BE1-E9A3-43F3-9B50-B7C8DE165D9B|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|Total|Integer|2|设备升级作业数量总计。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=ListOTATaskByJob
&JobId=7glPHmaDYLAYMD1HHutT02****
&PageSize=10
&CurrentPage=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListOTATaskByJobResponse>
    <PageCount>1</PageCount>
    <Data>
        <SimpleOTATaskInfo>
            <SrcVersion>1.0.0</SrcVersion>
            <DeviceName>testDevice1</DeviceName>
            <FirmwareId>q3j9OYBjUAZMv1hlMgdo03****</FirmwareId>
            <IotId>SR8FiTu1R9tlUR2V1bmi00105****</IotId>
            <ProductKey>a1GUfrM****</ProductKey>
            <JobId>7glPHmaDYLAYMD1HHutT02****</JobId>
            <TaskDesc>report version is not conform</TaskDesc>
            <DestVersion>1.0.1</DestVersion>
            <UtcCreate>2019-11-04T03:38:15.000Z</UtcCreate>
            <UtcModified>2019-11-04T03:38:15.000Z</UtcModified>
            <TaskStatus>FAILED</TaskStatus>
            <ProductName>MyProduct</ProductName>
            <TaskId>y3tOmCDNgpR8F9jnVEzC01****</TaskId>
            <Progress>0.00</Progress>
        </SimpleOTATaskInfo>
        <SimpleOTATaskInfo>
            <SrcVersion>1.0.0</SrcVersion>
            <DeviceName>testDevice2</DeviceName>
            <FirmwareId>q3j9OYBjUAZMv1hlMgdo03****</FirmwareId>
            <IotId>nadRdeffljdEndlfadgadfse****</IotId>
            <ProductKey>a1GUfrM****</ProductKey>
            <JobId>7glPHmaDYLAYMD1HHutT02****</JobId>
            <TaskDesc></TaskDesc>
            <DestVersion>1.0.1</DestVersion>
            <UtcCreate>2019-11-04T03:38:22.000Z</UtcCreate>
            <UtcModified>2019-11-04T03:38:22.000Z</UtcModified>
            <TaskStatus>SUCCEEDED</TaskStatus>
            <ProductName>MyProduct</ProductName>
            <TaskId>ZS9sNBb1ahsu6khqr9II01****</TaskId>
            <Progress>100.00</Progress>
        </SimpleOTATaskInfo>
    </Data>
    <PageSize>10</PageSize>
    <RequestId>A01829CE-75A1-4920-B775-921146A1AB79</RequestId>
    <Success>true</Success>
    <CurrentPage>1</CurrentPage>
    <Total>2</Total>
</ListOTATaskByJobResponse>
```

`JSON` 格式

```
{
  "PageCount": 1,
  "Data": {
    "SimpleOTATaskInfo": [{
      "SrcVersion": "1.0.0",
      "DeviceName": "testDevice1",
      "FirmwareId": "q3j9OYBjUAZMv1hlMgdo03****",
      "IotId": "SR8FiTu1R9tlUR2V1bmi00105****",
      "ProductKey": "a1GUfrM****",
      "JobId": "7glPHmaDYLAYMD1HHutT02****",
      "TaskDesc": "report version is not conform",
      "DestVersion": "1.0.1",
      "UtcCreate": "2019-11-04T03:38:15.000Z",
      "UtcModified": "2019-11-04T03:38:15.000Z",
      "TaskStatus": "FAILED",
      "ProductName": "MyProduct",
      "TaskId": "y3tOmCDNgpR8F9jnVEzC01****",
      "Progress": "0.00"
    }, {
      "SrcVersion": "1.0.0",
      "DeviceName": "testDevice2",
      "FirmwareId": "q3j9OYBjUAZMv1hlMgdo03****",
      "IotId": "nadRdeffljdEndlfadgadfse****",
      "ProductKey": "a1GUfrM****",
      "JobId": "7glPHmaDYLAYMD1HHutT02****",
      "TaskDesc": "",
      "DestVersion": "1.0.1",
      "UtcCreate": "2019-11-04T03:38:22.000Z",
      "UtcModified": "2019-11-04T03:38:22.000Z",
      "TaskStatus": "SUCCEEDED",
      "ProductName": "MyProduct",
      "TaskId": "ZS9sNBb1ahsu6khqr9II01****",
      "Progress": "100.00"
    }]
  },
  "PageSize": 10,
  "RequestId": "A59D3BE1-E9A3-43F3-9B50-B7C8DE165D9B",
  "CurrentPage": 1,
  "Success": true,
  "Total": 2
}
```


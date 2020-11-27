# QueryDeviceFileList

调用该接口查询指定设备上传到物联网平台的所有文件列表。

## 限制说明

-   调用该接口返回的文件信息中，不包括文件下载地址。如需获取文件下载地址，请调用[QueryDeviceFile](~~112002~~)查询。
-   单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceFileList&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceFileList|系统规定参数。取值：QueryDeviceFileList。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|PageSize|Integer|否|10|返回结果中每页显示的文件记录数量。最大取值200，默认值是10。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|要查询的设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|light|要查询的设备名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要查询的设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |
|CurrentPage|Integer|否|1|显示返回结果中的第几页。最小取值1，默认值 1。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|CurrentPage|Integer|1|当前页码。 |
|Data|Array of FileSummary| |调用成功时，返回的文件信息列表。 |
|FileSummary| | | |
|FileId|String|xL0G67MBLBDtkR7GCfT\*\*\*\*\*\*|文件ID，文件的唯一标识符。 |
|Name|String|testFile2.txt|文件名称。 |
|Size|String|1024000|文件大小，单位：KB。 |
|UtcCreatedOn|String|2019-03-21T08:45:42.000Z|文件创建时间。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|PageCount|Integer|1|总页数。 |
|PageSize|Integer|10|每页显示的文件个数。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |
|Total|Integer|2|文件总数。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceFileList
&ProductKey=a1BwAGV****
&DeviceName=deviceName1
&PageSize=10
&CurrentPage=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceFileListResponse>
  <PageCount>1</PageCount>
  <Data>
        <FileStoreSummary>
              <Name>testFile2.txt</Name>
              <FileId>xL0G67MBLBDtkR7GCfT******</FileId>
              <UtcCreatedOn>2019-03-21T08:45:42.000Z</UtcCreatedOn>
              <Size>102400</Size>
        </FileStoreSummary>
        <FileStoreSummary>
              <Name>testFile3.txt</Name>
              <FileId>6UCo1SqbqnQEoh9aKqD******</FileId>
              <UtcCreatedOn>2019-03-21T08:45:42.000Z</UtcCreatedOn>
              <Size>102400</Size>
        </FileStoreSummary>
        <FileStoreSummary>
              <Name>testFile1.txt</Name>
              <FileId>IhXXww3Eeu6uzSOSCyu******</FileId>
              <UtcCreatedOn>2019-03-21T08:45:40.000Z</UtcCreatedOn>
              <Size>102400</Size>
        </FileStoreSummary>
  </Data>
  <PageSize>10</PageSize>
  <RequestId>7C7BA526-826D-46AA-A45E-55D21E6D1583</RequestId>
  <CurrentPage>1</CurrentPage>
  <Success>true</Success>
  <Total>3</Total>
</QueryDeviceFileListResponse>
```

`JSON` 格式

```
{
  "PageCount": 1, 
  "Data": {
    "FileStoreSummary": [
      {
        "Name": "testFile2.txt", 
        "FileId": "xL0G67MBLBDtkR7GCfT******", 
        "UtcCreatedOn": "2019-03-21T08:45:42.000Z", 
        "Size": "102400"
      }, 
      {
        "Name": "testFile3.txt", 
        "FileId": "6UCo1SqbqnQEoh9aKqD******", 
        "UtcCreatedOn": "2019-03-21T08:45:42.000Z", 
        "Size": "102400"
      }, 
      {
        "Name": "testFile1.txt", 
        "FileId": "IhXXww3Eeu6uzSOSCyu******", 
        "UtcCreatedOn": "2019-03-21T08:45:40.000Z", 
        "Size": "102400"
      }
    ]
  }, 
  "PageSize": 10, 
  "RequestId": "7C7BA526-826D-46AA-A45E-55D21E6D1583", 
  "CurrentPage": 1, 
  "Success": true, 
  "Total": 3
}
```


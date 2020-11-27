# QueryDeviceFile

调用该接口查询指定设备上传到物联网平台的指定文件信息。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryDeviceFile&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryDeviceFile|系统规定参数。取值：QueryDeviceFile。 |
|FileId|String|是|xL0G67MBLBDtkR7GCfT\*\*\*\*\*\*|文件标识符。您可以调用[QueryDeviceFileList](~~112001~~)，从返回结果中查看文件ID。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ProductKey|String|否|a1BwAGV\*\*\*\*|要查询的设备所隶属的产品ProductKey。

 **说明：** 如果传入该参数，需同时传入**DeviceName**。 |
|DeviceName|String|否|light|要查询的设备名称。

 **说明：** 如果传入该参数，需同时传入**ProductKey**。 |
|IotId|String|否|Q7uOhVRdZRRlDnTLv\*\*\*\*00100|要查询的设备ID。物联网平台为该设备颁发的ID，设备的唯一标识符。

 **说明：** 如果传入该参数，则无需传入**ProductKey**和**DeviceName**。**IotId**作为设备唯一标识符，和**ProductKey**与**DeviceName**组合是一一对应的关系。如果您同时传入**IotId**和**ProductKey**与**DeviceName**组合，则以**IotId**为准。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的文件信息。 |
|DownloadUrl|String|http://iotx-file-store.oss-cn-shanghai.aliyuncs.com/device\_file/A849E4E5CFF64804A18D9384AC9D\*\*\*\*/aGEKIpp5NAGxdP2oo90000\*\*\*\*/testFile3.txt?Expires=1553162075&OSSAccessKeyId=LTAIYLScbHiV\*\*\*\*&Signature=%2F88xdEFPukJ\*\*\*\*%2F8\*\*\*\*%2Bdv3io%3D|文件下载URL。 |
|FileId|String|6UCo1SqbqnQEoh9aKqDQ01\*\*\*\*|文件标识符。 |
|Name|String|testFile3.txt|文件名称。 |
|Size|String|102400|文件大小，单位：KB。 |
|UtcCreatedOn|String|2019-03-21T08:45:42.000Z|文件创建时间。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDeviceFile
&ProductKey=a1BwAGV****
&DeviceName=deviceName1
&FileId=6UCo1SqbqnQEoh9aKqD******
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryDeviceFileResponse>
  <RequestId>93C5276D-5C8A-40D9-BFD6-4BD5B8C1A08F</RequestId>
  <Data>
        <Name>testFile3.txt</Name>
        <DownloadUrl>http://iotx-file-store.oss-cn-shanghai.aliyuncs.com/device_file/A849E4E5CFF64804A18D9384AC9D****/aGEKIpp5NAGxdP2oo90000****/testFile3.txt?Expires=1553162075&amp;OSSAccessKeyId=LTAIYLScbHiV****&amp;Signature=%2F88xdEFPukJ****%2F8****%2Bdv3io%3D</DownloadUrl>
        <FileId>6UCo1SqbqnQEoh9aKqDQ01****</FileId>
        <UtcCreatedOn>2019-03-21T08:45:42.000Z</UtcCreatedOn>
        <Size>102400</Size>
  </Data>
  <Success>true</Success>
</QueryDeviceFileResponse>
```

`JSON` 格式

```
{
  "RequestId": "93C5276D-5C8A-40D9-BFD6-4BD5B8C1A08F",
  "Data": {
    "Name": "testFile3.txt",
    "DownloadUrl": "http://iotx-file-store.oss-cn-shanghai.aliyuncs.com/device_file/A849E4E5CFF64804A18D9384AC9D****/aGEKIpp5NAGxdP2oo90000****/testFile3.txt?Expires=1553162075&OSSAccessKeyId=LTAIYLScbHiV****&Signature=%2F88xdEFPukJ****%2F8****%2Bdv3io%3D",
    "FileId": "6UCo1SqbqnQEoh9aKqDQ01****",
    "UtcCreatedOn": "2019-03-21T08:45:42.000Z",
    "Size": "102400"
  },
  "Success": true
}
```


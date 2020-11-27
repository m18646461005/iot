# ListThingModelVersion

调用该接口获取指定产品的物模型版本列表。

## 使用说明

物模型已实现版本化管理，您导入物模型（[ImportThingModelTsl](~~150320~~)）、复制其他产品物模型（[CopyThingModel](~~150322~~)）或编辑更新物模型后，需调用[PublishThingModel](~~150311~~)将物模型发布后才能被使用。一个产品的物模型每发布一次，生成一个版本。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为10。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=ListThingModelVersion&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListThingModelVersion|系统规定参数。取值：ListThingModelVersion。 |
|ProductKey|String|是|a1BwAGV\*\*\*\*|产品的ProductKey。

 可以在物联网平台控制台产品页查看，或调用[QueryProductList](~~69271~~)查看ProductKey的取值。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |
|ResourceGroupId|String|否|rg-acfm4l5tcwd\*\*\*\*|资源组ID。

 **说明：** 目前不传入此参数。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|Data|Struct| |调用成功时，返回的数据。 |
|ModelVersions|Array of ModelVersion| |物模型版本列表。按照物模型发布时间倒序排列。第一个为当前使用的版本。 |
|Description|String|增加一个light属性|物模型版本的描述。 |
|GmtCreate|Long|1579235657535|该版本物模型发布时的时间戳，格式为GMT毫秒值。 |
|ModelVersion|String|V1.0.0|物模型版本号。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=ListThingModelVersion
&ProductKey=a1rYuVF****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListThingModelVersionResponse>
  <Data>
        <ModelVersions>
              <ModelVersion>V3.0.0</ModelVersion>
              <GmtCreate>1579235682421</GmtCreate>
              <Description>new properties</Description>
        </ModelVersions>
        <ModelVersions>
              <ModelVersion>V2.0.0</ModelVersion>
              <GmtCreate>1579235657535</GmtCreate>
              <Description>new properties</Description>
        </ModelVersions>
        <ModelVersions>
              <ModelVersion>V1.0.0</ModelVersion>
              <GmtCreate>1579235637994</GmtCreate>
              <Description>Lighting</Description>
        </ModelVersions>
  </Data>
  <RequestId>9BA34AE5-2D94-4BDE-BD78-E7D3FC7985BC</RequestId>
  <Success>true</Success>
</ListThingModelVersionResponse>
```

`JSON` 格式

```
{
  "Data": {
    "ModelVersions": [
      {
        "ModelVersion": "V3.0.0",
        "GmtCreate": 1579235682421,
        "Description": "new properties"
      },
      {
        "ModelVersion": "V2.0.0",
        "GmtCreate": 1579235657535,
        "Description": "new properties"
      },
      {
        "ModelVersion": "V1.0.0",
        "GmtCreate": 1579235637994,
        "Description": "Lighting"
      }
    ]
  },
  "RequestId": "9BA34AE5-2D94-4BDE-BD78-E7D3FC7985BC",
  "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Iot)查看更多错误码。


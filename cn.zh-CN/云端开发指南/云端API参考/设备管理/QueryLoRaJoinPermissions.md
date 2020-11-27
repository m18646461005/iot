# QueryLoRaJoinPermissions

调用该接口查询LoRaWAN入网凭证列表。

## 限制说明

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为50。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=QueryLoRaJoinPermissions&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryLoRaJoinPermissions|系统规定参数。取值：QueryLoRaJoinPermissions。 |
|IotInstanceId|String|否|iot\_instc\_pu\*\*\*\*\_c\*-v64\*\*\*\*\*\*\*\*|实例ID。公共实例不传此参数，企业版实例需传入。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|iot.system.SystemException|调用失败时，返回的错误码。更多信息，请参见[错误码](~~87387~~)。 |
|ErrorMessage|String|系统异常|调用失败时，返回的出错信息。 |
|JoinPermissions|Array of JoinPermission| |调用成功时，返回的入网凭证数据（**JoinPermission**）。 |
|JoinPermission| | | |
|ClassMode|String|A|入网凭证采用的通信模式。取值：

 -   **A**：终端设备允许双向通信。
-   **B**：终端设备会在预设时间中开放接收窗口。
-   **C**：终端设备持续开放接收窗口，只在传输时关闭。 |
|Enabled|Boolean|true|入网凭证的启停用状态。取值：

 -   **true**：启用。
-   **false**：停用。 |
|JoinPermissionId|String|80\*\*\*|入网凭证ID，入网凭证的唯一标识。 |
|JoinPermissionName|String|ForTest|入网凭证名称。 |
|JoinPermissionType|String|LOCAL|入网凭证的类型。取值：

 -   **LOCAL**：专用凭证。
-   **ROAMING**：漫游凭证。 |
|OwnerAliyunPk|String|1375364789\*\*\*\*|入网凭证创建者的阿里云账号ID。 |
|ProductKey|String|a1BwAGV\*\*\*\*|使用该凭证的设备所属产品的ProductKey。 |
|RequestId|String|E55E50B7-40EE-4B6B-8BBE-D3ED55CCF565|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|true|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryLoRaJoinPermissions
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryLoRaJoinPermissions>
  <RequestId>1C1BD4E7-2FD3-4535-9D97-DE51803192AD</RequestId>
  <Success>true</Success>
  <JoinPermissions>
        <JoinPermission>
              <Enabled>true</Enabled>
              <JoinPermissionType>LOCAL</JoinPermissionType>
              <JoinPermissionId>50***</JoinPermissionId>
              <OwnerAliyunPk>198426864326****</OwnerAliyunPk>
              <ClassMode>A</ClassMode>
              <JoinPermissionName>给开发者B使用</JoinPermissionName>
        </JoinPermission>
  </JoinPermissions>
</QueryLoRaJoinPermissions>
```

`JSON` 格式

```
{
	"RequestId": "1C1BD4E7-2FD3-4535-9D97-DE51803192AD",
	"Success": true,
	"JoinPermissions": {
		"JoinPermission": [
			{
				"Enabled": true,
				"JoinPermissionType": "LOCAL",
				"JoinPermissionId": "50***",
				"OwnerAliyunPk": "198426864326****",
				"ClassMode": "A",
				"JoinPermissionName": "给开发者B使用"
			}
		]
	}
}
```


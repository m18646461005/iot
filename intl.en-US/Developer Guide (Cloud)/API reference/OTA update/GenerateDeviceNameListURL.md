# GenerateDeviceNameListURL

Generates the URL and details of a device list file to be uploaded to Object Storage Service \(OSS\). If you create a static update batch, you can specify devices to be updated in a device list file.

## Requirements

-   A device list file includes the names of devices. Separate multiple device names with line feeds or commas \(,\). A device list file must be in the CSV format. The maximum size of a device list file is 5 MB.
-   Each device list file can contain a maximum of 10,000 names for the devices of a product that is related to an update package. If the number of device names in a device list file exceeds the limit, an error occurs when you use the file to create a static update batch.

## Description

This operation can be used with other operations to upload a device list file. Procedure:

1. Call this operation to generate the information of a device list file to be uploaded to OSS.

The response parameters of this operation include:

The following request parameters of the OSS [PostObject](~~31988~~) operation that is used to upload the device list file: **Key**, **AccessKeyId**, **Signature**, and **Policy**.

2. Use an [OSS SDK](~~52834~~) to call the [PostObject](~~31988~~) operation to upload the device list file within 1 minute after a response is returned from this operation. For more information about sample code, see the "Usage of response parameters" section.

**Note:** The parameter information that is returned by this operation is valid for 1 minute. You must upload the device list file within 1 minute.

3. After the device list file is uploaded, call the IoT Platform [CreateOTAStaticUpgradeJob](~~147496~~) operation to create a static update batch within 60 minutes.

If device list files are uploaded but you do not call the CreateOTAStaticUpgradeJob to create a static update batch, these uploaded files are automatically deleted by the system on a regular basis.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** RAM users of an Alibaba Cloud account share the quota of the account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=GenerateDeviceNameListURL&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GenerateDeviceNameListURL|The operation that you want to perform. Set the value to GenerateDeviceNameListURL. |
|IotInstanceId|String|No|iot-cn-0pp1n8t\*\*\*\*|The instance ID. This parameter is not required for public instances. However, the parameter is required for the instances that you have purchased. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this API operation. For more information, see [Common request parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|iot.system.SystemException|The error code returned if the call fails. For more information about error codes, see [Error codes](~~87387~~). |
|Data|Struct| |The file upload information that is returned when the call succeeds. For more information, see the following parameters. |
|AccessKeyId|String|cS8uRRy54Rsz\*\*\*\*|The AccessKey ID of the bucket owner.

 This OSS bucket stores the device list file. |
|FileUrl|String|https://iotx-ota.oss-cn-shanghai.aliyuncs.com/ota/65dfcda0473be29836dfde585472\*\*\*\*/ck2nfzljo00023g7kysg0\*\*\*\*.csv|The URL of the device list file that is stored in OSS.

 After the device list file is uploaded, this parameter is used to call the [CreateOTAStaticUpgradeJob](~~147496~~) operation to create a static update batch. |
|Host|String|https://iotx-ota.oss-cn-shanghai.aliyuncs.com|The endpoint of OSS. |
|Key|String|ota/65dfcda0473be29836dfde585472\*\*\*\*/ck2nfzljo00023g7kysg0\*\*\*\*.csv|The full path of the device list file. The file is uploaded by the OSS PostObject operation. |
|ObjectStorage|String|OSS|The type of object storage. Default value: OSS. |
|Policy|String|eyJleHBpcmF\*\*\*\*|The parameter that is used by OSS to verify form fields for the request. |
|Signature|String|v6lViO4FBvfquajQjg20K5hK\*\*\*\*|The signature that is calculated based on the values of the **AccessKeySecret** and **Policy** parameters. When you call an OSS operation, OSS uses the signature information to verify the POST request. |
|UtcCreate|String|2019-11-04T06:21:54.607Z|The time when the URL of the device list file was generated. The time is displayed in UTC. |
|ErrorMessage|String|A system exception occurred.|The error message returned if the call fails. |
|RequestId|String|74C2BB8D-1D6F-41F5-AE68-6B2310883F63|The globally unique ID that Alibaba Cloud generates for the request. |
|Success|Boolean|true|Indicates whether the call succeeds.

 -   **true**: The call succeeded.
-   **false**: The call failed. |

## Usage of response parameters

When you call the OSS [PostObject](~~31988~~) operation to upload the device list file to OSS, specify the required response values that are returned from the GenerateDeviceNameListURL operation.

The following sample code that is written in Java shows how to upload the device list file to OSS.

-   Add the following dependencies to the pom.xml file:

```
<dependency>
  <groupId>org.apache.httpcomponents</groupId>
  <artifactId>httpclient</artifactId>
  <version>4.5.3</version>
</dependency>

<dependency>
  <groupId>org.apache.httpcomponents</groupId>
  <artifactId>httpmime</artifactId>
  <version>4.5.10</version>
</dependency>

```

-   Sample code:

```
public static boolean postObject(String key,
                                  String host,
                                  String policy,
                                  String ossAccessKeyId,
                                  String signature,
                                  String data) throws IOException {
  CloseableHttpClient httpClient = HttpClients.createDefault();
  HttpPost uploadFile = new HttpPost(host);

  MultipartEntityBuilder builder = MultipartEntityBuilder.create();
  builder.addTextBody("key", key, ContentType.TEXT_PLAIN);
  builder.addTextBody("policy", policy, ContentType.TEXT_PLAIN);
  builder.addTextBody("AccessKeyId", ossAccessKeyId, ContentType.TEXT_PLAIN);
  builder.addTextBody("signature", signature, ContentType.TEXT_PLAIN);
  builder.addTextBody("success_action_status", "200", ContentType.TEXT_PLAIN);
  builder.addBinaryBody("file", data.getBytes());

  HttpEntity multipart = builder.build();
  uploadFile.setEntity(multipart);
  CloseableHttpResponse response = httpClient.execute(uploadFile);

  if (response.getStatusLine().getStatusCode() == 200) {
    return true;
  }

  return false;
}

```

## Examples

Sample requests

```
https://iot.cn-shanghai.aliyuncs.com/?Action=GenerateDeviceNameListURL
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GenerateDeviceNameListURLResponse>
      <Data>
            <Policy>eyJleHBpcmF****</Policy>
            <FileUrl>https://iotx-ota.oss-cn-shanghai.aliyuncs.com/ota/65dfcda0473be29836dfde585472****/ck2nfzljo00023g7kysg0****.csv</FileUrl>
            <UtcCreate>2019-11-04T06:21:54.607Z</UtcCreate>
            <AccessKeyId>cS8uRRy54Rsz****</AccessKeyId>
            <Signature>v6lViO4FBvfquajQjg20K5hK****</Signature>
            <ObjectStorage>OSS</ObjectStorage>
            <Host>https://iotx-ota.oss-cn-shanghai.aliyuncs.com</Host>
            <Key>ota/65dfcda0473be29836dfde585472****/ck2nfzljo00023g7kysg0****.csv</Key>
      </Data>
      <RequestId>74C2BB8D-1D6F-41F5-AE68-6B2310883F63</RequestId>
      <Success>true</Success>
</GenerateDeviceNameListURLResponse>
```

`JSON` format

```
{
    "Data": {
        "Policy": "eyJleHBpcmF****",
        "FileUrl": "https://iotx-ota.oss-cn-shanghai.aliyuncs.com/ota/65dfcda0473be29836dfde585472****/ck2nfzljo00023g7kysg0****.csv",
        "UtcCreate": "2019-11-04T06:21:54.607Z",
        "AccessKeyId": "cS8uRRy54Rsz****",
        "Signature": "v6lViO4FBvfquajQjg20K5hK****",
        "ObjectStorage": "OSS",
        "Host": "https://iotx-ota.oss-cn-shanghai.aliyuncs.com",
        "Key": "ota/65dfcda0473be29836dfde585472****/ck2nfzljo00023g7kysg0****.csv"
    },
    "RequestId": "74C2BB8D-1D6F-41F5-AE68-6B2310883F63",
    "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).


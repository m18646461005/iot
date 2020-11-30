# GenerateOTAUploadURL

Generates the URL and details of an update package file to be uploaded to Object Storage Service \(OSS\).

## Description

This operation can be used with other operations to create an update package. Procedure:

1. Call this API operation to generate the details of an update package file to be uploaded to OSS.

The response parameters of this API operation include:

-   The following request parameters of the OSS [PostObject](~~31988~~) operation that is used to upload the update package file: **Key**, **OSSAccessKeyId**, **Signature**, and **Policy**.
-   The following request parameter of the [CreateOTAFirmware](~~147311~~) that is used to create the update package:**FirmwareUrl**.

2. Use an [OSS SDK](~~52834~~) to call the [PostObject](~~31988~~) operation to upload the update package file. For more information about sample code, see the "Usage of response parameters" section.

**Note:** The parameter information that is returned by this operation is valid for 1 minute. You must upload the update package file within 1 minute. The maximum size of the uploaded update package file is 1,000 MB.

3. After the update package file is uploaded, call the [CreateOTAFirmware](~~147311~~) operation to create an update package.

If update package files are uploaded but you do not call the CreateOTAFirmware operation to create update packages for the files, these uploaded files are automatically deleted by the system on a regular basis.

## Limits

Each Alibaba Cloud account can run a maximum of 10 queries per second \(QPS\).

**Note:** The quota is shared between the Alibaba Cloud account and RAM users.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Iot&api=GenerateOTAUploadURL&type=RPC&version=2018-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GenerateOTAUploadURL|The operation that you want to perform. Set the value to GenerateOTAUploadURL. |
|IotInstanceId|String|No|iot-cn-0pp1n8t\*\*\*\*|The instance ID. This parameter is not required for public instances. However, the parameter is required for the instances that you have purchased. |
|FileSuffix|String|No|apk|The file name extension of the update package file. Valid values: bin, apk, tar, gz, tar.gz, zip, and gzip.

Default value: bin. |

In addition to the preceding operation-specific request parameters, you must specify common request parameters when you call this API operation. For more information, see [Common request parameters](~~30561~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|iot.system.SystemException|The error code returned if the call fails. For more information about error codes, see [Error codes](~~87387~~). |
|Data|Struct| |The file upload information that is returned when the call succeeds. For more information, see the following parameters. |
|FirmwareUrl|String|https://iotx-ota.oss-cn-shanghai.aliyuncs.com/ota/65dfcda0473be29836dfde585472\*\*\*\*/ck2nfzljo00023g7kysg0\*\*\*\*.bin|The URL of the update package file that is stored in OSS.

After the update package file is uploaded, this parameter is used to call the [CreateOTAFirmware](~~147311~~) operation to create an update package. |
|Host|String|https://iotx-ota.oss-cn-shanghai.aliyuncs.com|The endpoint of OSS. |
|Key|String|ota/65dfcda0473be29836dfde585472\*\*\*\*/ck2nfzljo00023g7kysg0\*\*\*\*.bin|The full path of the update package file. The file is uploaded by the OSS PostObject operation. |
|OSSAccessKeyId|String|cS8uRRy54Rsz\*\*\*\*|The AccessKey ID of the bucket owner.

This OSS bucket stores the update package file. |
|ObjectStorage|String|OSS|The type of object storage. Default value: OSS. |
|Policy|String|eyJleHBpcmF\*\*\*\*|The parameter that is used by OSS to verify form fields for the request. |
|Signature|String|v6lViO4FBvfquajQjg20K5hK\*\*\*\*|The signature that is calculated based on the values of the **AccessKeySecret** and **Policy** parameters. When you call an OSS operation, OSS uses the signature information to verify the POST request. |
|UtcCreate|String|2019-11-04T06:21:54.607Z|The time when the URL of the update package file to be uploaded was generated. The time is displayed in UTC. |
|ErrorMessage|String|A system exception occurred.|The error message returned if the call fails. |
|RequestId|String|74C2BB8D-1D6F-41F5-AE68-6B2310883F63|The globally unique ID that Alibaba Cloud generates for the request. |
|Success|Boolean|true|Indicates whether the call succeeds.**true**indicates that the call succeeded.**false**indicates that the call failed. |

## Usage of response parameters

When you call the OSS [PostObject](~~31988~~) operation to upload the update package file to OSS, specify the required response values that are returned from the GenerateOTAUploadURL operation.

The following sample code that is written in Java shows how to upload the update package file to OSS.

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
      builder.addTextBody("OSSAccessKeyId", ossAccessKeyId, ContentType.TEXT_PLAIN);
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
https://iot.cn-shanghai.aliyuncs.com/?Action=GenerateOTAUploadURL
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GenerateOTAUploadURLResponse>
    <Data>
        <Key>ota/65dfcda0473be29836dfde585472****/ck2nfzljo00023g7kysg0****.bin</Key>
        <Host>https://iotx-ota.oss-cn-shanghai.aliyuncs.com</Host>
        <Policy>eyJleHBpcmF****</Policy>
        <OSSAccessKeyId>cS8uRRy54Rsz****</OSSAccessKeyId>
        <ObjectStorage>OSS</ObjectStorage>
        <UtcCreate>2019-11-04T06:21:54.607Z</UtcCreate>
        <Signature>PKmRTy40QxqIUUWy325SCT/****</Signature>
        <FirmwareUrl>https://iotx-ota.oss-cn-shanghai.aliyuncs.com/ota/65dfcda0473be29836dfde585472****/ck2nfzljo00023g7kysg0****.bin</FirmwareUrl>
    </Data>
    <RequestId>B6E77674-09C4-4647-BF85-59CB72A72E4B</RequestId>
    <Success>true</Success>
</GenerateOTAUploadURLResponse>
```

`JSON` format

```
{
    "Data": {
        "Key": "ota/65dfcda0473be29836dfde585472****/ck2nfzljo00023g7kysg0****.bin",
        "Host": "https://iotx-ota.oss-cn-shanghai.aliyuncs.com",
        "Policy": "eyJleHBpcmF****",
        "OSSAccessKeyId": "cS8uRRy54Rsz****",
        "ObjectStorage": "OSS",
        "UtcCreate": "2019-11-04T06:21:54.607Z",
        "Signature": "PKmRTy40QxqIUUWy325SCT/****",
        "FirmwareUrl": "https://iotx-ota.oss-cn-shanghai.aliyuncs.com/ota/65dfcda0473be29836dfde585472****/ck2nfzljo00023g7kysg0****.bin"
    },
    "RequestId": "B6E77674-09C4-4647-BF85-59CB72A72E4B",
    "Success": true
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Iot).


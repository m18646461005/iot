---
keyword: [device, OTA, Internet of Things, IoT, IoT Platform, over-the-air \(OTA\) technology, over-the-air technology, firmware update, topic, message format]
---

# Update devices by using OTA

IoT Platform supports the over-the-air \(OTA\) feature. You can use the OTA feature to update devices. This article describes how to use the OTA feature to update devices when Message Queuing Telemetry Transport \(MQTT\) is used to connect devices to IoT Platform. It also describes topics and data formats that are used during data forwarding.

## OTA update process

The following figure shows the process of an OTA update over MQTT.

![Process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9559276061/p172098.jpg)

**Note:**

-   Optional. Before the update, a device reports the version number of the OTA module.

    -   If you perform a full update, this step is optional. If the version number is not reported, you cannot update a specified version when you configure a batch update. For more information, see [Push an update package to devices](/intl.en-US/Maintenance/OAT update/Push firmware files to devices.md).
    -   If you perform a differential update, this step is required.
    A device needs to report the version number only once during the startup before the first update.

-   In the IoT Platform console, after you start updating multiple devices, each device is in the Pending Update state.

    When the OTA service of IoT Platform receives the update progress that is reported by a device, the status of the device changes to Updating.

-   IoT Platform checks whether an OTA update succeeds on a device based on the version number that is reported by the device.
-   An offline device cannot receive an update notification from IoT Platform.

    After the status of the device changes to online, IoT Platform identifies the change and the OTA service checks whether the device requires an update. If an update is required, the OTA service sends an update notification to the device. Otherwise, no notification is sent.


## Message formats

For more information about how to use language-specific SDKs to implement OTA updates on devices, see the [Link SDK documentation](https://www.alibabacloud.com/help/product/93051.htm).

The following steps describe the process of an OTA update.

1.  Optional. A device connects to the OTA service and reports the version number.

    The format of the topic is `/ota/device/inform/${YourProductKey}/${YourDeviceName}`. Sample message:

    ```
    {
      "id": "123",
      "params": {
        "version": "1.0.1",
        "module": "MCU"
      }
    }
    ```

    |Parameter|Type|Description|
    |:--------|:---|:----------|
    |id|String|The message ID. Valid values: 0 to 4294967295. Each message ID must be unique for the device.|
    |version|String|The version of the OTA module.|
    |module|String|The name of the OTA module. **Note:**

    -   If the device reports the version of the default module, the module parameter is optional.
    -   The version of the default module indicates the version of the device. |

2.  In the IoT Platform console, add an update package, check the update package, and then start a batch update.

    For more information, see [Push an update package to devices](/intl.en-US/Maintenance/OAT update/Push firmware files to devices.md).

3.  After you start an update in the console, the device receives the URL of the update package from a topic. The message that includes the URL is sent from the OTA service of IoT Platform to the topic.

    The format of the topic is `/ota/device/upgrade/${YourProductKey}/${YourDeviceName}`. After IoT Platform sends OTA update requests to devices, the devices receive the URL of the update package from this topic.

    Sample message:

    ```
    {
      "code": "1000",
      "data": {
        "size": 432945,
        "version": "2.0.0",
        "isDiff": 1,
        "url": "https://iotx-ota-pre.oss-cn-shanghai.aliyuncs.com/nopoll_0.4.4.tar.gz?Expires=1502955804&OSSAccessKeyId=XXXXXXXXXXXXXXXXXXXX&Signature=XfgJu7P6DWWejstKJgXJEH0qAKU%3D&security-token=CAISuQJ1q6Ft5B2yfSjIpK6MGsyN1Jx5jo6mVnfBglIPTvlvt5D50Tz2IHtIf3NpAusdsv03nWxT7v4flqFyTINVAEvYZJOPKGrGR0DzDbDasumZsJbo4f%2FMQBqEaXPS2MvVfJ%2BzLrf0ceusbFbpjzJ6xaCAGxypQ12iN%2B%2Fr6%2F5gdc9FcQSkL0B8ZrFsKxBltdUROFbIKP%2BpKWSKuGfLC1dysQcO1wEP4K%2BkkMqH8Uic3h%2Boy%2BgJt8H2PpHhd9NhXuV2WMzn2%2FdtJOiTknxR7ARasaBqhelc4zqA%2FPPlWgAKvkXba7aIoo01fV4jN5JXQfAU8KLO8tRjofHWmojNzBJAAPpYSSy3Rvr7m5efQrrybY1lLO6iZy%2BVio2VSZDxshI5Z3McKARWct06MWV9ABA2TTXXOi40BOxuq%2B3JGoABXC54TOlo7%2F1wTLTsCUqzzeIiXVOK8CfNOkfTucMGHkeYeCdFkm%2FkADhXAnrnGf5a4FbmKMQph2cKsr8y8UfWLC6IzvJsClXTnbJBMeuWIqo5zIynS1pm7gf%2F9N3hVc6%2BEeIk0xfl2tycsUpbL2FoaGk6BAF8hWSWYUXsv59d5Uk%3D",
        "md5": "93230c3bde425a9d7984a594ac55ea1e",
        "sign": "93230c3bde425a9d7984a594ac55****",
        "signMethod": "Md5",
        "module": "MCU",
        "extData":{
            "key1":"value1",
            "key2":"value2"
         }
      },
      "id": "1507707025",
      "message": "success"
    }
    ```

    |Parameter|Value|Description|
    |:--------|:----|:----------|
    |id|String|The message ID. Valid values: 0 to 4294967295. Each message ID must be unique for the device.|
    |message|String|The result.|
    |code|String|The HTTP status code.|
    |version|String|The version of the update package.|
    |size|Long|The size of the update package. Unit: bytes.|
    |url|String|The endpoint of the Object Storage Service \(OSS\) bucket that stores the update package.|
    |isDiff|Long|If the update package type is differential, the message includes the isDiff parameter that is set to 1. The value 1 indicates that the update package file is a differential package. The differential package includes only the differences between the original update package and the new update package. The device must integrate the differential package with the original update package to form the new update package. If the update package type is full, this parameter is not included.|
    |sign|String|The update package signature.|
    |signMethod|String|The signature algorithm. Valid values:     -   SHA256
    -   Md5
The MD5 algorithm is available only for Android differential packages.|
    |md5|String|If the signature algorithm is MD5, IoT Platform assigns values to the sign and md5 parameters.|
    |module|String|The name of the module to which the update package belongs. **Note:** If the name of the default module is specified, IoT Platform does not send the module parameter. |
    |extData|Object|Tag list of the update batch.Format of each tag: `"key":"value"`. |

4.  After the device receives the URL, the device connects to the URL by using HTTPS and download the update package from the URL.

    **Note:** If the device fails to download the update package from the URL within 24 hours, the URL becomes invalid.

5.  During an update, a device must send the update progress to a topic in the following format: `/ota/device/progress/${YourProductKey}/${YourDeviceName}`. Sample message:

    ```
    {
      "id": "123",
      "params": {
        "step": "-1",
        "desc": "OTA update has failed. No firmware information is available.",
        "module": "MCU"
      }
    }
    ```

    |Parameter|Value|Description|
    |:--------|:----|:----------|
    |id|String|The message ID. Valid values: 0 to 4294967295. Each message ID must be unique for the device.|
    |step|String|The progress information of the OTA update.

Valid values:

    -   1 to 100: indicates a percentage of the update progress.
    -   -1: indicates that the update failed.
    -   -2: indicates that the download failed.
    -   -3: indicates that the verification failed.
    -   -4: indicates that the writing failed. |
    |desc|String|The description of the step parameter. If an exception occurs, this parameter contains the error message.|
    |module|String|The name of the module to which the update package belongs. **Note:** If the device reports the update package version of the default module, the module parameter is optional. |

6.  After the OTA update of a device is completed, the device must send the current firmware version to a topic in the following format: `/ota/device/inform/${YourProductKey}/${YourDeviceName}`. If the reported version is the same as the version that the OTA service sends to the topic, the OTA update is successful. Otherwise, the OTA update fails.

    **Note:** A successful OTA update is indicated based only on the reported firmware version. For example, a device reports an update progress of 100%. However, no firmware version is reported. In this case, the update is also treated as failed.


## Common errors

-   The signature is invalid. If the URL of an update package is invalid or changed, this issue occurs, as shown in the following figure.

    ![Data masking](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9559276061/p94070.png)

-   Access denied. This error occurs due to an expired URL. The URL is valid for 24 hours.

    ![Data masking](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9559276061/p94092.png)



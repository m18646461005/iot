---
keyword: [Internet of Things, IoT Platform, IoT, OTA, Firmware update]
---

# Overview

Over-the-Air Technology \(OTA\) is a basic feature of IoT Platform. OTA allows you to update the firmware of IoT devices worldwide. This chapter uses an example to describe the OTA update process. Sample codes are also provided for configuring OTA updates on devices.

## OTA update process for device firmware

![OTA update process](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5131404061/p178027.jpg)

1.  \(Optional\) The device reports the current firmware version to the topic: `/ota/device/inform/${YourProductKey}/${YourDeviceName}`.

    ```
    
    {
      "id": 1,
      "params": {
        "version": "1-0-0"
      }
    }
    ```

2.  The device subscribes to the topic: `/ota/device/upgrade/${YourProductKey}/${YourDeviceName}` where IoT Platform pushes OTA notifications.

    The format of update notifications:

    ```
    {
        "code":"1000",
        "data":{
            "size":11472299,
            "sign":"83254ac96e141affb8aa42cbfec9****",
            "version":"2-0-0",
            "url":"https://iotx-ota.oss-cn-shanghai.aliyuncs.com/ota/dbab6f742ae389b40db88fc2500b****/ck0q5lyav00003i7hezxe****.zip?Expires=1568951190&OSSAccessKeyId=cS8uRRy54Rsz****&Signature=nk0sogaxtyp7dYvKZnjNQ%2BZ8Q9****",
            "signMethod":"Md5",
            "md5":"83254ac96e141affb8aa42cbfec9****"
        },
        "id":1568864790381,
        "message":"success"
    }
    ```

3.  The device downloads the firmware package from the URL that is provided in the update notification and performs a local update.
4.  The device reports the update progress to the topic: `/ota/device/progress/${YourProductKey}/${YourDeviceName}`.

    The format of report messages:

    ```
    {
      "id": 1,
      "params": {
        "step":"1", 
        "desc":" xxxxxxxx "
      }   
    }
    ```

5.  The device reports the updated firmware version to the topic: `/ota/device/inform/${YourProductKey}/${YourDeviceName}`.

    The format of report messages:

    ```
    
    {
      "id": 1,
      "params": {
        "version": "2-0-0"
      }
    }
    ```


## References

[Configure OTA update for devices](/intl.en-US/Best Practices/Maintenance and Monitoring/Configure OTA updates for devices/Configure OTA update for devices.md)

[Push firmware to devices](/intl.en-US/Best Practices/Maintenance and Monitoring/Configure OTA updates for devices/Push firmware to devices.md)


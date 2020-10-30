---
keyword: [Internet of Things, IoT Platform, IoT, OTA]
---

# Push firmware to devices

In the IoT Platform console, you can create a new firmware, upload a firmware file package, complete firmware verification, and push the firmware to a specified device for update.

-   OTA update is enabled for the device. For more information, see [Configure OTA update for devices](/intl.en-US/Best Practices/Maintenance and Monitoring/Configure OTA updates for devices/Configure OTA update for devices.md).

    Only devices that have OTA enabled can report firmware versions, receive update messages from the cloud, download firmware, and perform OTA update operations.

-   You have edited new firmware files based on your requirements. For the firmware file in this example, see the appendix of [Configure OTA update for devices](/intl.en-US/Best Practices/Maintenance and Monitoring/Configure OTA updates for devices/Configure OTA update for devices.md).

## Procedure

1.  Log on to the [IoT Platform console](http://iot.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Maintenance** \> **OTA Update**.

3.  On the OTA Update page, click **Add Update Package**.

4.  In the Add Update Package dialog box that appears, enter the firmware information, and upload the firmware file. For more information, see [Push firmware files to devices](/intl.en-US/Maintenance/OAT update/Push firmware files to devices.md).

    Upload the firmware file app\_1001 which is the BIN file generated when you [Configure OTA update for devices](/intl.en-US/Best Practices/Maintenance and Monitoring/Configure OTA updates for devices/Configure OTA update for devices.md) in the previous step.

5.  Click **Verify** to verify the device firmware. For more information, see [Push firmware files to devices](/intl.en-US/Maintenance/OAT update/Push firmware files to devices.md).

    The verification is successful after the device is updated. The **Batch Update** function is available.

6.  Click **Batch Update**. Set the update object and update policy, and push the update notification to the device. For more information, see [Push firmware files to devices](/intl.en-US/Maintenance/OAT update/Push firmware files to devices.md).


## View device logs

You can view the information about the firmware update from the logs of the devices after IoT Platform pushes the firmware update notification. The logs include notification messages, process messages, downloaded firmware, update progress, and update progress.

-   The log about update notification received by the device.

    ![IoT firmware update](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0047549951/p66139.png)

-   The log about the new firmware, and the firmware package download address.

    ![IoT firmware update](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1047549951/p66142.png)

-   The log about downloading the firmware and reporting the progress.

    ![IoT firmware update](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1047549951/p66144.png)



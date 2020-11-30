---
keyword: [Internet of Things, IoT Platform, IoT, device, update, firmware update, update package, OTA, update package version]
---

# Push an update package to devices

IoT Platform provides the over-the-air \(OTA\) update and management feature. To update devices, make sure that your devices support the over-the-air \(OTA\) service. Then, you can upload an update package to the IoT Platform console and push OTA update notifications to the devices. This article describes how to add an update package, verify the update package, and push the update package to multiple devices by using the IoT Platform console.

Before you use the OTA update feature, make sure that your devices support the OTA service.

-   For more information about how to configure OTA updates by using device SDKs, see [Update devices by using OTA](/intl.en-US/Maintenance/OAT update/Update devices by using OTA.md).
-   If you use the [Link SDK for Android](https://help.aliyun.com/document_detail/96607.html) on devices and need to perform differential updates, you must integrate the algorithms to authenticate the devices and generate full update packages. For more information, see [Implement a differential firmware update on an Android device]().
-   For more information about how to configure OTA updates if your devices are installed with AliOS Things chips, see [OTA tutorial for AliOS Things](https://github.com/alibaba/AliOS-Things/wiki/OTA-Tutorial).

Take note of the following limits of OTA updates:

-   Each Alibaba Cloud account can have a maximum of 500 update packages.
-   The maximum size of an update package file is 1,000 MB. The file format can only be .bin, .tar, .gz, .tar.gz, .zip, or .gzip.
-   Take note of the following limits of update batches:

    Update batches: IoT Platform shows created update tasks as different update batches. You can go to the Update Package Details page and view the update batch of the update package on the Batch Management tab.

    -   You can use an update package to create different update batches for multiple firmware versions to be updated.
    -   You can use an update package to create only one dynamic update batch for a firmware version to be updated.
    -   You can use different update packages to create multiple dynamic update batches for a firmware version to be updated.
    -   Each device can have only one ongoing update batch. A device that has an ongoing update batch is in the To Be Pushed, Pushed, or In Upgrade state.
-   Only devices that are connected to IoT Platform by using the MQTT protocol support the OTA update feature.
-   If devices are online, these devices can immediately receive update notifications. If devices are offline, IoT Platform pushes update notifications when devices go online.

1.  Log on to the [IoT Platform console](http://iot.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Maintenance** \> **OTA Update**.

    **Note:** To provide better services, IoT Platform improves the OTA update feature and allows you to manage update package versions based on products. When you use the new OTA update feature in the console for the first time, you must associate the uploaded update packages with products. You can associate an update package with only one product. For more information about how to associate update packages with products, see the instructions in the console.

3.  Optional. If AliOS Things chips are installed on your devices, you can enable the secure update feature.

    We recommend that you enable this feature to ensure integrity and security of update packages. If you use the Secure Update feature, verify the update package and update package signatures of devices. For more information, see [OTA Tutorial for AliOS Things](https://github.com/alibaba/AliOS-Things/wiki/OTA-Tutorial).

    1.  Go to the OTA Update page, and click **Secure Update**.

    2.  In the dialog box that appears, turn on the **Secure Update** switch for the product to be updated.

        When the Secure Update feature is in the **Activated** state, click **Copy** in the Public Key column to copy the public key. You can use the public key to verify the signature of the device.

4.  Optional. Add a custom OTA module.

    An OTA module indicates the module of devices to be updated in a product. These OTA modules include the firmware, software, and driver. The default module is the firmware of a device. You can also add another module as the OTA module.

    On the **Modules** tab, click **Add Module**, set the required parameters, and then click **OK**.

    |Parameter|Description|
    |:--------|:----------|
    |Product|The product to which the module belongs.|
    |Module Name|The module name. The module name must be unique in the product. The module name cannot be modified after the module is created. The module name must be 1 to 64 characters in length, and can contain letters, digits, periods\(.\), hyphens \(-\), and underscores \(\_\).|
    |Module Alias|The module alias. The module alias must be 1 to 64 characters in length, and can contain letters, digits, periods\(.\), hyphens \(-\), and underscores \(\_\).|
    |Module Description|The module description. The module description must be 1 to 100 characters in length.|

5.  On the OTA Update page, click **Add Update Package**.

6.  Set the required parameters, upload an update package, and then click **OK**.

    |Parameter|Description|
    |:--------|:----------|
    |Types of Update Packages|    -   Full: If you select Full, you must upload a complete update package. The system pushes the complete update package to devices for update.
    -   Differential: If you select Differential, you must upload a file that contains only the differences between the destination update package version and the original update package version. IoT Platform pushes the differences to devices for update. Then, the differences are merged into the original update packages. Differential updates optimize the usage of device resources and minimize the traffic that is consumed during update package pushing. |
    |Update Package Name|The update package name. The name must be 1 to 40 characters in length, and can contain letters, digits, hyphens \(-\), underscores \(\_\), and parentheses \(\). The name must start with a letter or digit.|
    |Product|The product to which the update package belongs.|
    |Update Package Module|The OTA module to which the update package applies.You can click **Add Module**. In the dialog box that appears, set the required parameters and click OK to add a module. |
    |Update Package Version|The update package version. The name must be 1 to 64 characters in length, and can contain letters, digits, periods \(.\), hyphens \(-\), and underscores \(\_\). You must specify this parameter if you set the Types of Update Packages parameter to **Full**. |
    |Version number to be upgraded|The version number for the OTA module of the device to be updated. The drop-down list shows the OTA module versions of all devices in the current product. You can enter a version number in the field, or select a version from the drop-down list. You must specify this parameter if you set the Types of Update Packages parameter to **Differential**. |
    |Post-upgrade version number|The version number of the update package. You must specify this parameter if you set the Types of Update Packages parameter to **Differential**. |
    |Signature Algorithm|The signature algorithm. Valid values: MD5 and SHA256. If you use the Link SDK for Android and set the Types of Update Packages parameter to **Differential**, select the MD5 algorithm. |
    |Select Update Package|Select an update package to upload. The maximum size of an update package is 1,000 MB. The file format can only be .bin, .tar, .gz, .tar.gz, .zip, or .gzip.|
    |Update Package Description|The update package description. The description must be 1 to 100 characters in length.|

7.  Validate the update package on one or more devices. On the Update Packages tab, find the required update package and click **Verify** in the Actions column. In the dialog box that appears, set the required parameters, and click **OK**.

    **Note:** After you upload an update package to IoT Platform, you must validate the update package on several devices. Make sure that these devices are updated. Then, you can use the update package to create batch update tasks.

    |Parameter|Description|
    |:--------|:----------|
    |Version number to be upgraded|    -   If you perform a full update, this parameter is optional.

The drop-down list shows the versions of all devices in the current product, except for the version for the destination device. You can select one or more versions. After you select the required versions, the related devices are added to the **Device to be verified** list as candidate devices.

If you do not set this parameter, no limit is set on the version number for the OTA module of the devices to be verified.

    -   If you perform a differential update, the value of this parameter is the version number that you specify when you add the update package. |
    |Device to be verified|Select one or more devices to be verified.|
    |Device upgrade time-out \(minutes\)|The timeout period of the update. If the specified device has not been updated within this period, the update times out. The period starts from the first time the specified device submits the update progress. Valid values: 1 to 1440. Unit: minutes.|

8.  After the update package is verified, click **Batch Update**, configure the required update scope and update policy, and then click **OK** to push update notifications to devices in batches.

    |Parameter|Description|
    |:--------|:----------|
    |Version number to be upgraded|    -   If you perform a full static update, this parameter is optional. If you perform a full dynamic update, this parameter is required. If you set the Apply Update to parameter to **Selected Devices**, do not set this parameter.

The drop-down list shows the versions of all devices in the current product, except for the version for the destination device. You can select one or more versions.

If you do not set this parameter, no limit is set on the version number for the OTA module of the devices to be verified.

    -   If you perform a differential update, the value of this parameter is the version number that you specify when you add the update package. |
    |Upgrade Method|    -   Static Update: updates only the current devices that meet the conditions.
    -   Dynamic Update: constantly updates the devices that meet the conditions. Dynamic updates can be applied to the following scenarios:

        -   The devices that are subsequently activated meet the conditions.
        -   The current OTA module versions that devices submit do not meet the conditions. However, the devices subsequently submit the OTA module versions that meet the conditions.
**Note:** You can use an update package to create only one dynamic update batch. If you have created a dynamic update batch by using an update package, you must cancel this dynamic update batch before you create another one. |
    |Apply Update to|    -   All Devices: updates all eligible devices in the specified product.
    -   Selected Devices: updates only the specified devices. If you set Selected Devices, use one of the following methods to select the required devices:
        -   **Select**: Select the required devices from the Device Range drop-down list.
        -   **Upload**: Download a template file in the .csv format. Perform the steps that are provided in the template to enter the names of the required devices. Then, upload the template file. Each template file can contain a maximum of 10,000 records.
    -   Phased Update: updates the specified devices. This option appears if you select Static Update from the Update Policy drop-down list.

After you select Phased Update, specify a range for devices in the Range \(%\) field that appears. IoT Platform calculates the number of devices to be updated based on the specified range. The calculation result is rounded down. You must specify at least one device for phased update. |
    |Update Time|The time when the OTA update is performed.     -   Update: immediately performs the OTA update.
    -   Scheduled Update: performs the OTA update during a specified time range. You can specify a start time and end time. The start time must be 5 minutes to 7 days later than the current time. The end time must be 1 hour to 30 days later than the start time. The end time is optional. If you do not specify an end time, the update is not forcibly stopped.

**Note:** Scheduled updates are available if you select **Static Update** from the Update Policy drop-down list. |
    |Update Package Push Rate|The number of devices to which you want to push the download URL of the update package per minute. Valid values: 10 to 1000.|
    |Retry Interval|The interval after which a retry is performed if the update fails. Valid values:     -   Do Not Retry
    -   Retry Immediately
    -   Retry in 10 Minutes
    -   Retry in 30 Minutes
    -   Retry in 1 Hour
    -   Retry in 24 Hours |
    |Maximum Retries|The maximum number of retries after the update fails. Valid values:     -   1
    -   2
    -   5 |
    |Timeout \(Minutes\)|The timeout period of the update. If the specified device has not been updated within this period, the update times out. The period starts from the first time the specified device submits the update progress. Valid values: 1 to 1440. Unit: minutes.|
    |Override Previous Device Update Tasks|Specifies whether to overwrite the previous update task. Each device can be in only one ongoing update task at a time. The To Be Pushed, Pushed, or In Upgrade state is displayed if a device is in an ongoing update task.    -   If you select Yes, only the new update task is performed.
    -   If you select No and the device already has an update task, the previous task is implemented.
The update task that is in progress is not overwritten. |
    |Take Effect for only Devices that Newly Report Versions|This parameter is available if you set the Update Policy parameter to **Dynamic Update**.This parameter specifies whether to update only the devices that submit firmware versions later. Ensure that the submit firmware versions are used as the firmware versions to be updated

    -   If you select Yes, only the devices that subsequently submit firmware versions are updated.
    -   If you select No, the current devices that meet the conditions are updated. In addition, IoT Platform constantly checks the devices. If the devices that subsequently submit firmware versions meet the conditions, these devices are updated. |
    |Tag|Click **Add Tag**. In the dialog box that appears, enter the key and value of the tag, and click **OK**. After an update batch is created, you cannot modify the tag that is added to the update batch.The tag of an update batch is sent to devices when IoT Platform pushes update notifications to these devices. |


After you submit a batch update request, IoT Platform pushes an update notification to your devices based on your settings.

Find the required update package and click **View** in the Actions column. On the Batch Management tab, you can perform the following operations:

-   View the status of an update batch.
-   Cancel all update tasks of an update batch.

**View the status of an update batch**

On the Batch Management tab, find the required update batch and click **View** in the Actions column. On the Batch Details page, you can view devices in different update statuses on the Device List tab.

|State|Description|
|-----|-----------|
|To Be Pushed|The OTA update notification has not been pushed to the device. This state may appear due to the following three causes: 1. The device is offline. 2. The notification is scheduled to be pushed. 3. The pushing rate exceeds the limit. The following states that correspond to these three causes are displayed:

-   **To Be Pushed \(Device Offline\)**
-   **To Be Pushed \(Timing: 2020/XX/XX XX:XX:XX\)**
-   **To Be Pushed** |
|Pushed|The device has received the OTA update notification but has not submitted the progress.|
|In Upgrade|The device has received the OTA update notification and submitted the update progress.|
|Updated|The device has submitted the update progress 100% and valid version number after the update.|
|Updated Failed|OTA updates may fail due to the following causes: -   If a device receives a new update notification before the previous update is complete, the new update fails. In this case, you can update the device after the previous update is complete.
-   During the updating process, an update package may fail to be downloaded, extracted, or validated. If a failure occurs, you can initiate a new update.

If you configure a batch update and specify automatic update retries, the retries are performed after the update fails. An update may fail due to one of the following causes:

-   The device in the **To Be Pushed** or **Pushed** state submits a version that is not the current version or the destination version.
-   The device in the **In Upgrade** state submits a version that is not the destination version.
-   The device submits one of the following values when using a specified topic to submit the update progress to IoT Platform: -1, -2, -3, and -4.

During automatic retries, the update status of a device in IoT Platform remains unchanged. For example, if a retry occurs on a device that is in the **Pushed** state, the device status is still displayed as **Pushed** in IoT Platform. If a retry occurs on a device that is in the **In Upgrade** state, the device status is still displayed as **In Upgrade** in IoT Platform.

**Note:**

IoT Platform does not perform update retries if an update fails due to one of the following causes:

-   The update fails due to the `timeout` issue.
-   The update is canceled. |
|Canceled|The update for the device is canceled.|

**Cancel all update tasks of an update batch**

On the Batch Management tab, find the required update batch and click **Cancel** in the Actions column.

-   For a static update batch, only scheduled update tasks are canceled by default. You can cancel all ongoing update tasks, including those in the To Be Pushed, Pushed, and In Upgrade states.
-   For a dynamic update batch, the dynamic update policy is canceled by default. You can cancel all ongoing update tasks, including those in the To Be Pushed, Pushed, and In Upgrade states.


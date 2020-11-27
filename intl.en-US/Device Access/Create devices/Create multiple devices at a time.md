---
keyword: [Internet of Things, IoT, IoT Platform, batch, create, register, device, obtain a device certificate, DeviceName, DeviceSecret]
---

# Create multiple devices at a time

A product consists of multiple devices of the same type. After you create a product, you must create devices for the product. You can create one or more devices at a time. This topic describes how to create multiple devices at a time.

1.  Log on to the [IoT Platform console](http://iot.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Devices** \> **Devices**.

3.  On the Devices page, click **Batch Add**.

4.  Select a product. Each new device derives the features and properties of the product.

    **Note:** If the product is associated with another platform, make sure that your account has sufficient activation codes to create the device.

    ![Create multiple devices at a time](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8480646061/p134552.png)

5.  Select a method to name devices.

    -   **Auto Generate**: You do not need to name devices. After you enter the number of devices, IoT Platform generates names for all devices. Each device name consists of random letters and digits.
    -   **Batch Upload**: You must name each device. Click **Download.csv Template** to download a template, specify the DeviceName and Nickname parameters in the template, and then upload the template to the IoT Platform console.

        **Note:** You must note the following issues:

        -   Each device name must be 4 to 32 characters in length and can contain letters, digits, hyphens \(-\), underscores \(\_\), at sign \(@\), periods \(.\), and colons \(:\). The name of each device that you create for a product must be unique.
        -   The Nickname parameter specifies an alias. Each alias must be 4 to 64 characters in length and can contain letters, digits, and underscores \(\_\). This parameter is optional.
        -   Each template file can contain a maximum of 1,000 device names.
        -   The maximum size of a template file is 2 MB.
6.  Click **OK**.

    If a template file includes one or more invalid device names, an error occurs. You can click **Download Invalid Device Name List** to download a TXT file. The file includes invalid device names. Modify the invalid device names in the file based on the naming rules of devices. Then, upload the file again.

7.  After the devices are created, click **Download Activation Credential** to download the certificates of the devices. Then, you can burn the certificates on the devices.


The devices are created. You can view the information about the devices and download the certificates of the devices on the Batch Management tab of the Devices page.

-   Find the batch of the devices, and click **Details** to view the details of the devices.
-   Click **DownloadCSV** to download the certificates of the devices.

View device information. For more information, see [Manage devices](/intl.en-US/Device Access/Create devices/Manage devices.md).

The status of the created devices is **Not Activated**. Use a Link SDK to implement a device, connect the device to IoT Platform, and then activate the device. For more information, see the [Link SDK documentation](https://www.alibabacloud.com/help/product/93051.htm).

Connect the device to IoT Platform. For more information about best practices, see the following articles:

-   [Access IoT Platform by using MQTT.fx](/intl.en-US/Best Practices/Device access/Access IoT Platform by using MQTT.fx.md)
-   [Connect Android Things to IoT Platform](/intl.en-US/Best Practices/Device access/Connect Android Things to IoT Platform.md)


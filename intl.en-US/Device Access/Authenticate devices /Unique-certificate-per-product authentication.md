---
keyword: [Internet of Things, IoT, IoT Platform, device, connection authentication, device activation, unique-certificate-per-product, security authentication, dynamic registration, product certificate, ProductKey, ProductSecret, DeviceSecret, DeviceToken, ClientID]
---

# Unique-certificate-per-product authentication

If you use unique-certificate-per-product authentication, the same firmware is burned to all devices of a product. The firmware includes the same product certificate information \(ProductKey and ProductSecret\). When a device initiates an activation request, IoT Platform authenticates the device. If the authentication is successful, IoT Platform sends the information that is required for connection to the device.

**Note:** This authentication method has the risk of product certificate disclosure because all devices of a product has the same firmware. On the Product Details page, you can turn off the Dynamic Registration switch to reject authentication requests from new devices.

The following diagram shows the procedure of unique-certificate-per-product authentication.

![Procedure of unique-certificate-per-product authentication](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9554788951/p146855.png)

You can use unique-certificate-per-product authentication in the following two methods:

-   Pre-registration unique-certificate-per-product authentication

    Before you connect a device to the network, you must register the DeviceName in IoT Platform. We recommend that you use the MAC address, IMEI number, or serial number \(SN\) as the DeviceName. IoT Platform issues a DeviceSecret to the device.

    After IoT Platform authenticates the device, the device uses the ProductKey, DeviceName, and DeviceSecret to establish a connection with IoT Platform.

    Pre-registration unique-certificate-per-product authentication supports MQTT-based connections.

-   Preregistration-free unique-certificate-per-product authentication

    You do not need to pre-register a device in IoT Platform. Instead, you can use an IoT card number, etc. as the DeviceName.

    After IoT Platform authenticates the device, the device uses the ProductKey, DeviceName, ClientID, and DeviceToken to establish a connection with IoT Platform.

    Preregistration-free unique-certificate-per-product authentication supports MQTT-based connections.


1.  Create a product.

    Create a product in the [IoT Platform console](http://iot.console.aliyun.com/). For more information, see [Create a product](/intl.en-US/Device Access/Create a product.md).

2.  Enable dynamic registration.

    On the Product Details page, turn on the Dynamic Registration switch. IoT Platform sends an SMS verification code to confirm your identity.

    **Note:** If dynamic registration is disabled when devices initiate activation requests, IoT Platform rejects the requests. Activated devices are not affected.

    ![Enable dynamic registration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9554788951/p146857.png)

3.  Add a device.

    -   Pre-registration unique-certificate-per-product authentication

        Add a device to a created product. For more information, see [Create multiple devices at a time](/intl.en-US/Device Access/Create devices/Create multiple devices at a time.md) or [Create a device](/intl.en-US/Device Access/Create devices/Create a device.md).

        IoT Platform authenticates the DeviceName when a device initiates an activation request. We recommend that you use an identifier that can be obtained from the device, such as the MAC address, IMEI or SN, as the DeviceName.

        IoT Platform issues a DeviceSecret to the device. The initial state of the device is Inactive.

    -   If you use preregistration-free unique-certificate-per-product authentication, skip this step.
4.  Burn the device SDK on the production line.

    1.  Download the device SDK. For more information, see [Link SDK](https://www.alibabacloud.com/help/doc-detail/96627.htm).

    2.  Initialize the device SDK and enable dynamic registration. In the device SDK, specify the ProductKey and ProductSecret.

        For more information about how to configure device-side SDKs to use the unique-certificate-per-product method, see the documentations about authentication and connection in [Authentication and connection](https://www.alibabacloud.com/help/doc-detail/96627.htm).

    3.  Develop the device SDK based on your business needs. For example, you can develop the following features: over-the-air \(OTA\) update, sub-device connection, Thing Specification Language \(TSL\), and device shadows.

    4.  Burn the developed device SDK to the device on the production line.

5.  Connect the device to IoT Platform.

    Power on the device and connect it to IoT Platform. Then, the device carries the ProductKey, ProductSecret, and DeviceName to initiate an authentication request. For more information, see [HTTP-based dynamic device registration](/intl.en-US/Device Management/Develop devices based on Alink Protocol/Device identity registration.md).

6.  Activate the device in IoT Platform.

    -   Pre-registration unique-certificate-per-product authentication

        After IoT Platform authenticates the device, IoT Platform delivers the DeviceSecret that is issued in step 3 to the device. The device obtains the device certificate \(ProductKey, DeviceName, and DeviceSecret\) and can use the certificate to connect with IoT Platform for data communication.

        **Note:**

        -   A device certificate can be used to activate only one physical device.
        -   If physical device A is activated under the DeviceName but device B needs to use this DeviceName, you can delete device A from IoT Platform and invalidate the DeviceSecret of device A. Then, use the DeviceName to add a device to activate physical device B.
        -   To reactivate a device due to the loss of its DeviceSecret, use the [ResetThing](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/ResetThing.md) API to reset the device, and then reconnect the device to IoT Platform to activate the device. The DeviceSecret issued by the IoT Platform does not change.
    -   Preregistration-free unique-certificate-per-product authentication

        After IoT Platform authenticates the device, IoT Platform delivers the ClientID and DeviceToken to the device. Then, the device uses the ProductKey and ProductSecret, ClientID, and DeviceToken to connect with IoT Platform for data communication.

        **Note:** A maximum of five physical devices can be activated in IoT Platform with the same ProductKey, ProductSecret, and DeviceName, and each device has a unique ClientID and DeviceToken.

        A DeviceName may be used for multiple physical devices that have different ClientIDs. In this case, the following message appears on the Product Details page of the IoT Platform console: The devices of the current product have multiple ClientIDs. You can retain one physical device or clear all physical devices.

        1.  On the Product Details page, click **View** to view the security-compromised devices under the product.
        2.  On the **Devices** \> **Devices** page, find the device and click **View** to go to the Device Details page. The ClientID for the current connection is displayed. Click **Switch** or **Clear** next to the ClientID.
            -   **Switch**: Select the ClientID from the drop-down list. Check the first connection time of the device that corresponds to the ClientID, or click **Log Service** and view [IoT Platform logs](/intl.en-US/Maintenance/Log Service/IoT Platform logs.md) to determine whether it is a physical device that needs to be retained. Select the ClientID of the physical device that you want to retain, and click **OK**. The physical devices that use other ClientIDs are forbidden to connect.
            -   **Clear**: All physical devices are forbidden to connect.


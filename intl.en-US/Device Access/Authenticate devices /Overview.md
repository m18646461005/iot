---
keyword: [Internet of Things, IoT, IoT Platform, device, connection authentication, unique-certificate-per-product, unique-certificate-per-device, security authentication, device activation]
---

# Overview

A device must pass identity authentication before it can be connected to IoT Platform. IoT Platform supports device authentication by using device keys.

## Use device keys for authentication

When you create a product, set **Authentication Mode** to **Device Secret**. IoT Platform issues a ProductSecret and DeviceSecret or other device keys to each device. When a device is accessing IoT Platform, the device must use the device keys for identity authentication.

IoT Platform supports various authentication methods to meet the requirements of different scenarios.

-   Unique-certificate-per-device authentication: A device certificate is burned to each device. The device certificate includes a ProductKey, DeviceName, and DeviceSecret. For more information, see [Unique-certificate-per-device authentication](/intl.en-US/Device Access/Authenticate devices /Unique-certificate-per-device authentication.md).
-   Pre-registration unique-certificate-per-product authentication: A product certificate is burned to all devices of a product. The product certificate includes a ProductKey and ProductSecret. For more information, see [Unique-certificate-per-product authentication](/intl.en-US/Device Access/Authenticate devices /Unique-certificate-per-product authentication.md). Enable dynamic registration for the product, and use dynamic registration to obtain a DeviceSecret for a device.
-   Preregistration-free unique-certificate-per-product authentication: A product certificate is burned to all devices of a product. The product certificate includes a ProductKey and ProductSecret. For more information, see [Unique-certificate-per-product authentication](/intl.en-US/Device Access/Authenticate devices /Unique-certificate-per-product authentication.md). Enable dynamic registration for the product, and use dynamic registration to obtain a combination of ClientID and DeviceToken instead of a DeviceSecret.
-   [Sub-device authentication](/intl.en-US/Device Management/Develop devices based on Alink Protocol/Device identity registration.md): After a sub-device is connected to IoT Platform by using a gateway, you can use dynamic registration to obtain a DeviceSecret for the sub-device.

These methods have their own benefits in terms of accessibility and security. You can choose a method based on the security requirements of the device and the actual production conditions. The following table shows the comparison among these methods.

|Item|Unique-certificate-per-device authentication|Pre-registration unique-certificate-per-product authentication|Preregistration-free unique-certificate-per-product authentication|Sub-device authentication|
|----|--------------------------------------------|--------------------------------------------------------------|------------------------------------------------------------------|-------------------------|
|Information burned into the device|ProductKey, DeviceName, and DeviceSecret|ProductKey and ProductSecret|ProductKey and ProductSecret|ProductKey|
|Enable dynamic registration in IoT Platform|Not required. The dynamic registration feature is enabled by default.|Required.|Required.|Required.|
|Create a device in IoT Platform and register the DeviceName|Required. You must ensure that the specified DeviceName is unique under a product.|Required. You must ensure that the specified DeviceName is unique under a product.|Not required.|Required. You must ensure that the specified DeviceName is unique under a product.|
|Certificate burning requirement|Burn a unique device certificate to each device. You must ensure the security of each device certificate.|Burn the same product certificate to all devices of a product. You must ensure that the product certificate is safely kept.|Burn the same product certificate to all devices of a product. You must ensure that the product certificate is safely kept.|-   A gateway can obtain the ProductKeys of all sub-devices on premises.
-   Burn the ProductKey of each sub-device on the gateway. |
|Security|High|Medium|Medium|Medium|
|Upper limit for registrations|A product can have a maximum of 500,000 devices.|A product can have a maximum of 500,000 devices.|A product can have a maximum of 500,000 devices.|A maximum of 1,500 sub-devices can be registered under a gateway.|
|Other external reliance|N/A|N/A|N/A|Security of the gateway.|


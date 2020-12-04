---
keyword: [IoT Platform, IoT, Alibaba Cloud IoT Platform, Sub-device, Gateway]
---

# Overview

Sub-devices cannot directly connect to IoT Platform. Instead, they must connect to IoT Platform through a gateway. This topic describes how to connect a sub-device to IoT platform through a gateway.

Follow these steps: 1. Create a gateway and a sub-device in IoT Platform. 2. Develop a device SDK for the gateway to connect the gateway to IoT platform. The gateway can build a topological relationship between the gateway and the sub-device and reports to IoT Platform. When the gateway find that it has a topological relationship with the connected sub-device, it reports the device certificate of the sub-device, or dynamically registers the sub-device. IoT Platform authenticates the identity of the sub-device and the topological relationship between the sub-device and the gateway. After the sub-device and the gateway pass the authentication, IoT Platform establishes a logical channel for the sub-device and binds the logical channel to the physical channel of the gateway. In this way, the sub-device can connect to IoT Platform for communications through the gateway.

![Sub-device communication](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1937549951/p2876.png)

This example only describes how to connect a sub-device to IoT platform through a gateway, and does not involve communication configurations such as Thing Specification Language \(TSL\) model communication. If youwant to transmit a TSL model between the sub-device and IoT platform, configure the gateway to transmit the TSL model information for the sub-device . For more information about the configuration, see [TSL model communication](/intl.en-US/Best Practices/Communications/TSL model communication.md).

**Note:** The gateway supplier implements data transmission between the gateway and the sub-device. Alibaba Cloud does not provide corresponding code.

## References

To download the SDK demo used in this example, click [here](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/44229/intl_en/1565952427116/iotx-api-demo.zip).

To connect the sub-device to IoT Platform through the gateway, follow these steps:

-   [Create a gateway and a sub-device](/intl.en-US/Best Practices/Device management/Connect a sub-device to IoT Platform/Create a gateway and a sub-device.md)
-   [Initialize the SDKs](/intl.en-US/Best Practices/Device management/Connect a sub-device to IoT Platform/Initialize the SDKs.md)
-   [Connect the gateway to IoT Platform](/intl.en-US/Best Practices/Device management/Connect a sub-device to IoT Platform/Connect the gateway to IoT Platform.md)
-   [Connect the sub-device to IoT Platform](/intl.en-US/Best Practices/Device management/Connect a sub-device to IoT Platform/Connect the sub-device to IoT Platform.md)


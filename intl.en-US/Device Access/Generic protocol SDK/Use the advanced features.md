---
keyword: [Internet of Things, IoT Platform, IoT, communication protocol, generic protocol, bridge, bridging, dynamically register bridge devices]
---

# Use the advanced features

This article describes how to use the advanced features of the generic-protocol SDK. The advanced features allow you to specify the path of the configuration file and dynamically register the bridge devices. You can also call the data reporting interface methods to report properties, events, and update tags. These methods are encapsulated in the generic-protocol SDK.

## Specify the path of configuration files

By default, the configuration file of a bridge is the application.conf file and the configuration file of the device certificate mapping is the devices.conf file. The generic-protocol SDK allows you to specify the file paths. Before you call the bootstrap\(\) method, you can call the ConfigFactory.init\(\) method to specify the path of a configuration file. You can also create an instance and implement the corresponding interface.

Sample code:

```
ConfigFactory.init(
    ConfigFactory.getBridgeConfigManager("application-self-define.conf"),
    selfDefineDeviceConfigManager);
bridgeBootstrap.bootstrap();

private static DeviceConfigManager selfDefineDeviceConfigManager = new DeviceConfigManager() {
    @Override
    public DeviceIdentity getDeviceIdentity(String originalIdentity) {
        return devicesMap.get(originalIdentity);
    }

    @Override
    public String getOriginalIdentity(String productKey, String deviceName) {
        return null;
    }
};
```

## Dynamically register the bridge devices

When you need to deploy bridges on a large number of servers, the deployment process is complex if you specify different bridge devices for different bridge servers. You can edit the bridge configuration file application.conf to dynamically register the bridge devices. You must specify the productKey and popClientProfile parameters of each bridge device in the configuration file. Then, the generic-protocol SDK calls the related IoT Platform API operation to register the bridge devices and uses the MAC addresses of the servers as the device names.

**Note:**

-   To dynamically register the bridge devices, you only need to edit the bridge configuration file. For information about the sample code, see [Use the basic features](/intl.en-US/Device Access/Generic protocol SDK/Use the basic features.md).
-   If the bridge configuration file already includes the information of a bridge device, the bridge device is not registered again. The generic-protocol SDK calls the related IoT Platform API operation to register a bridge device only if the configuration file meets the following conditions: The deviceName and deviceSecret parameters are left empty, and all the parameters in popClientprofile are specified. If a device is already registered by using a MAC address, the device will not be registered again.
-   We recommend that you do not use the bridge configuration file of the production environment to debug the bridge servers. If you use the bridge configuration file of the production environment for debugging, the bridge servers that are specified by the MAC addresses are registered as bridges. The bridge servers are associated with all devices in the devices.conf file. We recommend that you use test devices for debugging to avoid negative impacts on the production environment.

|Parameter|Required|Description|
|:--------|:-------|:----------|
|productKey|Yes|The key of the product to which the bridge device belongs.|
|subDeviceConnectMode|No|The mode that devices use to connect with the bridge.-   If this parameter is set to 3, a large-sized bridge is returned. A maximum of 200,000 devices can connect with the bridge.
-   If this parameter is not specified, a small-sized bridge is returned. A maximum of 15,000 devices can connect with the bridge.

Large-sized bridges and small-sized bridges use different policies to disconnect devices. For more information, see [Disconnect device](/intl.en-US/Device Access/Generic protocol SDK/Use the basic features.mdsection_dx9_225_h22).|
|http2Endpoint|Yes|The endpoint of the HTTP/2 gateway. The bridge and IoT Platform establish a persistent connection over the HTTP/2 protocol. -   For the public instance, the endpoint of the HTTP/2 gateway is in the format of `https://${productKey}.iot-as-http2. ${RegionId}.aliyuncs.com:443`.

Replace $\{productKey\} with the key of the product to which your bridge device belongs.

Replace $\{RegionId\} with the ID of the region where you purchased the IoT Platform service. For more information, see [Regions and zones](https://www.alibabacloud.com/help/doc-detail/40654.htm).

For example, if the product key of a bridge device is a1abcab\*\*\*\* and the IoT Platform service is purchased in the China \(Shanghai\) region, the endpoint of the HTTP/2 gateway is `https://a1abcab****.iot-as-http2.cn-shanghai.aliyuncs.com:443`.

-   For a purchased instance, the endpoint of the HTTP /2 gateway is in the format of `https://${IotInstanceId}.http2.iothub.aliyuncs.com:443`.

Replace $\{IotInstanceId\} with the ID of the purchased instance.

For example, if the instance ID is iot-cn-g06kwb\*\*\*\*, the endpoint of the HTTP/2 gateway is `https://iot-cn-g06kwb****.http2.iothub.aliyuncs.com:443`. |
|authEndpoint|Yes|The endpoint of the device authentication server. -   For the public instance, the endpoint of the device authentication server is in the format of `https://iot-auth ${RegionId}.aliyuncs.com/auth/bridge`.

Replace $\{RegionId\} with the region ID. For more information, see [Regions and zones](https://www.alibabacloud.com/help/doc-detail/40654.htm).

For example, if the IoT Platform service is purchased in the China \(Shanghai\) region, the endpoint of the device authentication server is `https://iot-auth.cn-shanghai.aliyuncs.com/auth/bridge`.

-   For a purchased instance, the endpoint of the device authentication server is in the format of `https://${IotInstanceId}.auth.iothub.aliyuncs.com/auth/bridge`.

Replace $\{IotInstanceId\} with the ID of the purchased instance.

For example, if the instance ID is iot-cn-g06kwb\*\*\*\*, the endpoint of the device authentication server is `https://iot-cn-g06kwb****.auth.iothub.aliyuncs.com/auth/bridge`. |
|popClientProfile|Yes|If you specify this parameter, the generic-protocol SDK calls the related IoT Platform API operation to automatically create a bridge device. The following table describes the parameters of popClientProfile. |

|Parameter|Required|Description|
|:--------|:-------|:----------|
|accessKey|Yes|The AccessKey ID of your Alibaba Cloud account. To create or view an AccessKey pair, log on to the [IoT Platform console](http://iot.console.aliyun.com/), move the pointer over your profile picture, and then click **AccessKey Management**. On the Security Management page, you can create or view an AccessKey pair. |
|accessSecret|Yes|The AccessKey secret of you Alibaba Cloud account.|
|name|Yes|The ID of the region to which the bridge device belongs. For more information, see [Regions and zones](https://www.alibabacloud.com/help/doc-detail/40654.htm). |
|region|Yes|The ID of the region to which the bridge device belongs. You can set this parameter to the same value as the name parameter. |
|product|Yes|The name of the product. Set the value to Iot.|
|endpoint|Yes|The endpoint of the APIs in the specified region. The endpoint is in the format of `iot. ${RegionId}.aliyuncs.com`. Replace $\{RegionId\} with the region ID. For more information, see [Regions and zones](https://www.alibabacloud.com/help/doc-detail/40654.htm).

For example, if the region is China \(Shanghai\), the endpoint is `iot.cn-shanghai.aliyuncs.com`. |

The following example shows how to configure a small-sized bridge by dynamically registering the devices. The public instance is used in the example.

```
# The endpoint of the server.
http2Endpoint = "https://${YourProductKey}.iot-as-http2.cn-shanghai.aliyuncs.com:443"
authEndpoint = "https://iot-auth.cn-shanghai.aliyuncs.com/auth/bridge"

# The information of the bridge device.
productKey = ${YourProductKey}

popClientProfile = {
    accessKey = ${YourAliyunAccessKey}
    accessSecret = ${YourAliyunAccessSecret}
    name = cn-shanghai
    region = cn-shanghai
    product = Iot
    endpoint = iot.cn-shanghai.aliyuncs.com
}
```

## Call the methods to report Thing Specification Language \(TSL\) data

To simplify the usage of the generic-protocol SDK, the SDK provides three data reporting methods: reportProperty\(\), fireEvent\(\), and updateDeviceTag\(\). The device can use these methods to report properties, events, and update device tags.

Prerequisites and instructions:

-   Properties and events are defined in the IoT Platform console. Before you call reportProperty\(\) and fireEvent\(\) to report properties and events, log on to the [IoT Platform console](http://iot.console.aliyun.com/) and go to the Product Details page of the required product. Then, click the Define Feature tab and define properties and events. For more information, see [Add a TSL feature](/intl.en-US/Device Management/TSL/Add a TSL feature.md).
-   Tags are created and updated. Before you call the updateDeviceTag method to update a device tag, check whether the tag is displayed in the IoT Platform console. If the tag is displayed on the Device Details page of the required device, update the value of the tag. If the tag is not displayed, create a tag.

Sample code:

```
TslUplinkHandler tslUplinkHandler = new TslUplinkHandler();
// Report a property.
// The testProp property is defined.
String requestId = String.valueOf(random.nextInt(1000));
tslUplinkHandler.reportProperty(requestId, originalIdentity, "testProp", random.nextInt(100));

// Report an event.
// The testEvent event is defined.
requestId = String.valueOf(random.nextInt(1000));
HashMap<String, Object> params = new HashMap<String, Object>();
params.put("testEventParam", 123);
tslUplinkHandler.fireEvent(originalIdentity, "testEvent", ThingEventTypes.INFO, params);

// Update device tags.
// The key of the tag is set to testDeviceTag.
requestId = String.valueOf(random.nextInt(1000));
tslUplinkHandler.updateDeviceTag(requestId, originalIdentity, "testDeviceTag", String.valueOf(random.nextInt(1000)));
```

The following table describes the parameters that are used in this example.

|Parameter|Description|
|:--------|:----------|
|requestId|The ID of the request.|
|originalIdentity|The original identifier of the device.|
|testProp|The identifier of the property. In this example, a property whose identifier is testProp is defined in the IoT Platform console before the reportProperty\(\) method is called to report the value of property.|
|random.nextInt\(100\)|The property value to be reported. The value range of the property is also defined in the IoT Platform console. In this example, the value is a random integer that is generated by `random.nextInt(100)`. The value is less than 100.|
|testEvent|The identifier of the event. In this example, an event whose identifier is testEvent is created in the IoT Platform console before the fireEvent\(\) method is called to report the event.|
|ThingEventTypes.INFO|The event type. The ThingEventTypes parameter specifies the event type. For example, INFO indicates that the event type is information. In this example, the event type is set to INFO when the testEvent is defined in the IoT Platform console.

If the event type is ERROR, set this parameter to `ThingEventTypes.ERROR`. |
|params|The output parameters of the event. The identifier, data type, and value range of the output parameters are also defined in the IoT Platform console. In this example, the identifier of the output parameter is testEventParam, and the value is 123.|
|testDeviceTag|The key of the tag. The data type is string. In this example, the key is testDeviceTag. Set the key of the tag as instructed based on your business requirements. For more information, see [Device tags](/intl.en-US/Device Management/Tags.md).|
|String.valueOf\(random.nextInt\(1000\)\)|The value of the tag. The data type is string. In this example, the value is a random integer that is generated by `String.valueOf(random.nextInt(1000))`. The value is less than 1000. Set the value of the tag as instructed based on your business requirements. For more information, see [Device tags](/intl.en-US/Device Management/Tags.md).|


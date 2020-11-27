---
keyword: [Internet of Things, IoT Platform, IoT, communication protocol, generic protocol, bridge, bridging]
---

# Use the basic features

Your device can connect to and communicate with Alibaba Cloud IoT Platform by using the bridging service that is supported by the generic-protocol SDK. This article describes how to configure the generic-protocol SDK to implement the basic features. These features include device connection and disconnection, and upstream and downstream message transmission.

For more information, visit [Generic-protocol SDK demo](https://github.com/aliyun/alibabacloud-iot-bridge-core-demo) in GitHub.

## Process

The following figure shows the overall process to connect a device to IoT Platform by using the generic-protocol SDK.

![Bridge](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2577929951/p45089.png)

## Deploy a development environment

Deploy a development environment to use the SDK for Java and add the following Maven dependency to your project to import the generic-protocol SDK.

```
<dependency>
  <groupId>com.aliyun.openservices</groupId>
  <artifactId>iot-as-bridge-sdk-core</artifactId>
  <version>2.1.3</version>
</dependency>
```

## Initialize SDK and specify bridge information

-   Initialize the SDK.

    Create a BridgeBootstrap object and call the bootstrap\(\) method. After the generic-protocol SDK is initialized, the SDK reads the bridge information and sends a connection request to IoT Platform for the bridge.

    When you call the bootstrap\(\) method, you can register the DownlinkChannelHandler callback with the generic-protocol SDK to receive messages from IoT Platform.

    Sample code:

    ```
    BridgeBootstrap bridgeBootstrap = new BridgeBootstrap();
    bridgeBootstrap.bootstrap(new DownlinkChannelHandler() {
        @Override
        public boolean pushToDevice(Session session, String topic, byte[] payload) {
            // Receive messages from IoT Platform.
            String content = new String(bytes);
            log.info("Get DownLink message, session:{}, {}, {}", session, topic, content);
            return true;
        }
    
        @Override
        public boolean broadcast(String topic, byte[] payload) {
            return false;
        }
    });
    ```

-   Specify the bridge information.

    By default, a bridge is configured in a configuration file. The configuration file is the application.conf file under the default resource directory of the Java project. In most cases, the directory is src/main/resources/. The file is in the [HOCON](https://github.com/lightbend/config/blob/master/HOCON.md) \(a JSON superset\) format. The generic-protocol SDK uses typesafe.config to parse the configuration file.

    You can configure a bridge by specifying a device or dynamically registering devices. This section describes how to configure a bridge by specifying a device. For more information about how to dynamically register devices, see [Dynamically register a bridge device](/intl.en-US/Device Access/Generic protocol SDK/Use the advanced features.md).

    The following table describes the bridge parameters.

    |Parameter|Required|Description|
    |:--------|--------|:----------|
    |productKey|Yes|The key of the product to which the bridge device belongs.|
    |deviceName|Yes|The name of the bridge device.|
    |deviceSecret|Yes|The secret of the bridge device.|
    |subDeviceConnectMode|No|The mode that devices use to connect with the bridge.    -   If this parameter is set to 3, a large-sized bridge is returned. A maximum of 200,000 devices can connect with the bridge.
    -   If this parameter is not specified, a small-sized bridge is returned. A maximum of 15,000 devices can connect with the bridge.
Large-sized bridges and small-sized bridges use different policies to disconnect devices. For more information, see [Disconnect device](#section_dx9_225_h22).|
    |http2Endpoint|Yes|The endpoint of the HTTP/2 gateway. The bridge and IoT Platform establish a persistent connection over the HTTP/2 protocol.     -   For the public instance, the endpoint of the HTTP/2 gateway is in the format of `https://${productKey}.iot-as-http2. ${RegionId}.aliyuncs.com:443`.

Replace $\{productKey\} with the key of the product to which your bridge device belongs.

Replace $\{RegionId\} with the ID of the region where you purchased the IoT Platform service. For more information, see [Regions and zones](https://www.alibabacloud.com/help/doc-detail/40654.htm).

For example, if the product key of a bridge device is a1abcab\*\*\*\* and the IoT Platform service is purchased in the China \(Shanghai\) region, the endpoint of the HTTP/2 gateway is `https://a1abcab****.iot-as-http2.cn-shanghai.aliyuncs.com:443`.

    -   For a purchased instance, the endpoint of the HTTP/2 gateway is in the format of `https://${IotInstanceId}.http2.iothub.aliyuncs.com:443`.

Replace $\{IotInstanceId\} with the ID of the purchased instance.

For example, if the instance ID is iot-cn-g06kwb\*\*\*\*, the endpoint of the HTTP/2 gateway is `https://iot-cn-g06kwb****.http2.iothub.aliyuncs.com:443`. |
    |authEndpoint|Yes|The endpoint of the device authentication server.     -   For the public instance, the endpoint of the device authentication server is in the format of `https://iot-auth ${RegionId}.aliyuncs.com/auth/bridge`.

Replace $\{RegionId\} with the ID of the region where you purchased the IoT Platform service. For more information, see [Regions and zones](https://www.alibabacloud.com/help/doc-detail/40654.htm).

For example, if the IoT Platform service is purchased in the China \(Shanghai\) region, the endpoint of the device authentication server is `https://iot-auth.cn-shanghai.aliyuncs.com/auth/bridge`.

    -   For a purchased instance, the endpoint of the device authentication server is in the format of `https://${IotInstanceId}.auth.iothub.aliyuncs.com/auth/bridge`.

Replace $\{IotInstanceId\} with the ID of the purchased instance.

For example, if the instance ID is iot-cn-g06kwb\*\*\*\*, the endpoint of the device authentication server is `https://iot-cn-g06kwb****.auth.iothub.aliyuncs.com/auth/bridge`. |

    The following example shows how to configure the certificate information of a small-sized bridge device. The public instance is used in the example.

    ```
    # The endpoint of the server.
    http2Endpoint = "https://a1tN7OBmTcd.iot-as-http2.cn-shanghai.aliyuncs.com:443"
    authEndpoint = "https://iot-auth.cn-shanghai.aliyuncs.com/auth/bridge"
    
    # The information of the bridge device.
    productKey = ${bridge-ProductKey-in-Iot-Plaform}
    deviceName = ${bridge-DeviceName-in-Iot-Plaform}
    deviceSecret = ${bridge-DeviceSecret-in-Iot-Plaform}
    ```


## Authenticate a device and connect the device to IoT Platform

-   Connect a device to the bridge.

    The following example shows how to connect a device to the bridge by using the generic-protocol SDK:

    ```
    /**
     * Device authentication.
     * @param newSession: the device session information that is returned in a downstream callback.
     * @param originalIdentity: the original identifier of the device.
     * @return
     */
    public boolean doOnline(Session newSession, String originalIdentity);
    ```

    When the device is connected to the bridge, the device must pass the Session parameter. The Session parameter is returned to the bridge by using a callback function of a downstream message. The Session parameter contains a field that indicates the original identifier of the device. The field ensures that the bridge can identify the device that sends the messages.

    In addition, the Session parameter contains an optional channel field. The field can carry the information of the device connection. For example, your bridge server is built based on Netty. You can use this field to carry the channel object that corresponds to the persistent connection of the device. When a message is received from IoT Platform, the bridge can directly obtain the channel object from the Session parameter for subsequent use. The data type of the channel field is object. The generic-protocol SDK does not process the data of the channel field. You can also use the channel field to carry the device-related information.

    Sample code:

    ```
    UplinkChannelHandler uplinkHandler = new UplinkChannelHandler();
    // Create a session.
    Object channel = new Object();
    Session session = Session.newInstance(originalIdentity, channel);
    // Connect a device to the bridge.
    boolean success = uplinkHandler.doOnline(session, originalIdentity);
    if (success) {
        // If the device is connected, the bridge accepts subsequent communication requests from the device.
    } else {
        // If the device connection fails, the bridge rejects subsequent communication requests, such as disconnection requests.
    }
    ```

-   Map an original device identifier to a device certificate.

    You must configure the mappings between device certificates and original device identifiers. By default, the mappings are configured in a configuration file. The configuration file is the devices.conf file under the default resource directory of the Java project. In most cases, the directory is src/main/resources/. The file is in the [HOCON](https://github.com/lightbend/config/blob/master/HOCON.md) \(a JSON superset\) format. The generic-protocol SDK uses the typesafe.config file to parse the configuration file.

    You must configure the device certificate information in the following format:

    ```
    ${device-originalIdentity} {
      productKey : ${device-ProductKey-in-Iot-Plaform}
      deviceName : ${device-DeviceName-in-Iot-Platform}
      deviceSecret : ${device-DeviceSceret-in-Iot-Platform}
    }
    ```

    |Parameter|Required|Description|
    |:--------|:-------|-----------|
    |productKey|Yes|The key of the product to which the device belongs.|
    |deviceName|Yes|The name of the device.|
    |deviceSecret|Yes|The secret of the device.|


## Send data from a device to IoT Platform

The following example shows how to send data from a device to IoT Platform by using the generic-protocol SDK:

```
/**
 * Send a message from the device by using a synchronous call.
 * @param originalIdentity: the original identifier of the device.
 * @param protocolMsg: the message to be sent, including the topic, payload, and quality of service (QoS) information.
 * @param timeout: the timeout period. Unit: seconds.
 * @return: indicates whether the message is sent within the timeout period.
 */
boolean doPublish(String originalIdentity, ProtocolMessage protocolMsg, int timeout);
/**
 * Send a message from the device by using an asynchronous call.
 * @param originalIdentity: the original identifier of the device.
 * @param protocolMsg: the message to be sent, including the topic, payload, and QoS information.
 * @return: After this method is called, the CompletableFuture is immediately returned and available for subsequent use.
 */
CompletableFuture<ProtocolMessage> doPublishAsync(String originalIdentity, 
                                                  ProtocolMessage protocolMsg);
```

Sample code:

```
DeviceIdentity deviceIdentity = 
    ConfigFactory.getDeviceConfigManager().getDeviceIdentity(originalIdentity);
ProtocolMessage protocolMessage = new ProtocolMessage();
protocolMessage.setPayload("Hello world".getBytes());
protocolMessage.setQos(0);
protocolMessage.setTopic(String.format("/%s/%s/update", 
        deviceIdentity.getProductKey(), deviceIdentity.getDeviceName()));
// Synchronous sending.
int timeoutSeconds = 3;
boolean success = upLinkHandler.doPublish(originalIdentity, protocolMessage, timeoutSeconds);
// Asynchronous sending.
upLinkHandler.doPublishAsync(originalIdentity, protocolMessage);
```

## Push data from the bridge to devices

When the bridge calls the bootstrap\(\) method, it registers DownlinkChannelHandler with the generic-protocol SDK. When the generic-protocol SDK receives a message from IoT Platform, it calls the pushToDevice\(\) method in DownlinkChannelHandler\(\) method. You can modify the pushToDevice\(\) method to enable the bridge to process the downstream message.

**Note:** Do not implement a time-consuming logic in the pushToDevice method. Otherwise, the thread that receives downstream messages will be blocked. If a time-consuming logic or I/O logic is required, implement the logic in an asynchronous manner. For example, if a bridge uses a persistent connection to forward downstream messages to a device, you can implement the logic in an asynchronous manner.

Sample code:

```
private static ExecutorService executorService  = new ThreadPoolExecutor(
    Runtime.getRuntime().availableProcessors(),
    Runtime.getRuntime().availableProcessors() * 2,
    60, TimeUnit.SECONDS,
    new LinkedBlockingQueue<>(1000),
    new ThreadFactoryBuilder().setDaemon(true).setNameFormat("bridge-downlink-handle-%d").build(),
    new ThreadPoolExecutor.AbortPolicy());
public static void main(String args[]) {
    // By default, application.conf and devices.conf are used.
    bridgeBootstrap = new BridgeBootstrap();
    bridgeBootstrap.bootstrap(new DownlinkChannelHandler() {
        @Override
        public boolean pushToDevice(Session session, String topic, byte[] payload) {
            // Receive messages from IoT Platform.
            executorService.submit(() -> handleDownLinkMessage(session, topic, payload));
            return true;
        }
        @Override
        public boolean broadcast(String s, byte[] bytes) {
            return false;
        }
    });
}
private static void handleDownLinkMessage(Session session, String topic, byte[] payload) {
    String content = new String(payload);
    log.info("Get DownLink message, session:{}, topic:{}, content:{}", session, topic, content);
    Object channel = session.getChannel();
    String originalIdentity = session.getOriginalIdentity();
}
```

|Parameter|Description|
|:--------|:----------|
|Session|A session that is received from a device when the device is connecting to IoT Platform. A session can be used to identify the device to which the downstream message is sent.|
|topic|The topic of the downstream message.|
|payload|The payload of a downstream message in the binary format.|

## Disconnect device

A device is disconnected in the following scenarios:

-   If a small-sized bridge is disconnected from IoT Platform, all devices connected to the bridge are automatically disconnected from IoT Platform.
-   If a large-sized bridge is disconnected from IoT Platform, the devices connected to the bridge are not automatically disconnected from IoT Platform. After the bridge is reconnected to IoT Platform, the bridge can update the status of the devices by using the device offline interface.

    The status of a sub-device indicates whether the sub-device is connected to a gateway. The gateway reports the status of sub-devices to IoT Platform. If the gateway cannot report the status of the sub-devices to IoT Platform, the status that is displayed on IoT Platform remains unchanged.

    For example, assume that a sub-device is connected to IoT Platform through a gateway and the status of the sub-device is online. If the gateway is disconnected from IoT Platform, the gateway cannot report the status of the sub-device to IoT Platform. Therefore, the status of the sub-device remains online.

-   If small-sized and large-sized bridges are connected to IoT Platform, they can send a request to disconnect a device from IoT Platform.

    The following example shows how to send a disconnection request:

    ```
    /**
     * Send a request to disconnect a device from IoT Platform.
     * @param originalIdentity: the original identifier of the device.
     * @return: indicates whether the disconnection request is sent.
     */
    boolean doOffline(String originalIdentity);
    ```

    Sample code:

    ```
    upLinkHandler.doOffline(originalIdentity);
    ```



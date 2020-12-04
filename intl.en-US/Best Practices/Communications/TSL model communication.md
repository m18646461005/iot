---
keyword: [Internet of Things, IoT, IoT Platform, TSL model, TSL, Communications]
---

# TSL model communication

Devices exchange Thing Specification Language \(TSL\) models with IoT Platform over the Alink protocol. During the communication, devices report properties or events to IoT Platform, and IoT Platform also delivers messages to devices to set properties or invoke services. This topic provides the Java demo to describe how to configure the code for TSL model communication.

-   You have activated the [IoT Platform](https://www.alibabacloud.com/product/iot) service.
-   You have installed a Java development environment.

## Create a product and a device

You must create a product and a device, and define features for the product.

1.  Log on to the [IoT Platform console](https://iot.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Devices** \> **Products**.

3.  Click **Create Product** to create a product.

    For more information, see [Create a product](/intl.en-US/Device Access/Create a product.md).

4.  Click the name of the product to go to the Product Details page, and click the Define Feature tab to define the TSL model.

    The following example shows the properties, services, and events of the product.

    ![TSL model communication](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1837549951/p53967.png)

    For more information, see [Add a TSL feature](/intl.en-US/Device Management/TSL/Add a TSL feature.md).

5.  In the left-side navigation pane, click **Devices** to create devices.

    The following example includes how to set the same property of multiple devices under the same product and invoke the same service of multiple devices. Therefore, you must create at least two devices. For more information, see [Create multiple devices at a time](/intl.en-US/Device Access/Create devices/Create multiple devices at a time.md).


## Download and install the SDK demo

In the following example, the SDK demo contains the server SDK and the device SDK.

1.  Click [here](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/44229/intl_en/1565952427116/iotx-api-demo.zip) to download iotx-api-demo, and decompress the package.

2.  Open the Java development tool and import the decompressed iotx-api-demo folder.

3.  In the java directory, add the following Maven dependencies to the pom file to import the server SDK and device SDK.

    ```
    <! -- https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-iot -->
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-iot</artifactId>
        <version>6.5.0</version>
    </dependency>
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-core</artifactId>
        <version>3.5.1</version>
    </dependency>
    <dependency>
      <groupId>com.aliyun.alink.linksdk</groupId>
      <artifactId>iot-linkkit-java</artifactId>
      <version>1.2.0.1</version>
      <scope>compile</scope>
    </dependency>
    ```

4.  In the directory java/src/main/resources/, configure the initialization in the config file.

    ```
    user.accessKeyID = <your accessKey ID>
    user.accessKeySecret = <your accessKey Secret>
    iot.regionId = <regionId>
    iot.productCode = Iot
    iot.domain = iot.<regionId>.aliyuncs.com
    iot.version = 2018-01-20
    ```

    |Parameter|Description|
    |:--------|:----------|
    |accessKeyID|The AccessKey ID of your Alibaba Cloud account. Place the pointer on your profile icon in the console, select **AccessKey** to go to the User Management page. You can create or check your AccessKey in User Management. |
    |accessKeySecret|The AccessKey Secret of your Alibaba Cloud account. You can check the AccessKey Secret in the same way as the AccessKey ID.|
    |regionId|The ID of the region where your IoT devices are located. For more information about region ID expressions, see [Regions and zones]().|


## Report properties and events by using the device SDK

Configure the device SDK to connect to IoT Platform and report properties and events.

The ThingTemplate file in the directory java/src/main/com.aliyun.iot.api.common.deviceApi contains the demo that devices use to report properties and events.

-   Configure the connection information.

    In this demo, replace the parameters productKey, deviceName, and deviceSecret with the certificate of your device, and replace the regionId parameter with the region ID.

    ```
    public static void main(String[] args) {
            /**
             * The certificate of your device.
             */
            String productKey = "your productKey";
            String deviceName = "your deviceName";
            String deviceSecret = "your deviceSecret";
            /**
             * The information about the MQTT connection.
             */
            String regionId = "your device regionId";
            ThingTemplate manager = new ThingTemplate();
    
            DeviceInfo deviceInfo = new DeviceInfo();
            deviceInfo.productKey = productKey;
            deviceInfo.deviceName = deviceName;
            deviceInfo.deviceSecret = deviceSecret;
    
            /**
             * The Java HTTP client of this device server supports TSLv1.2.
             */
            System.setProperty("https.protocols", "TLSv2");
            manager.init(deviceInfo, regionId);
        }
    ```

-   Initialize the connection.

    ```
    public void init(final DeviceInfo deviceInfo, String region) {
            LinkKitInitParams params = new LinkKitInitParams();
            /**
             * Specifies the parameters for the MQTT initialization.
             */
            IoTMqttClientConfig config = new IoTMqttClientConfig();
            config.productKey = deviceInfo.productKey;
            config.deviceName = deviceInfo.deviceName;
            config.deviceSecret = deviceInfo.deviceSecret;
            config.channelHost = deviceInfo.productKey + ".iot-as-mqtt." + region + ".aliyuncs.com:1883";
            /**
             * Specifies whether to receive offline messages.
             * The cleanSession field corresponding to the MQTT connection.
             */
            config.receiveOfflineMsg = false;
            params.mqttClientConfig = config;
            ALog.setLevel(LEVEL_DEBUG);
            ALog.i(TAG, "mqtt connection info=" + params);
    
            /**
             * Specifies the initialization and passes in the certificate information of the specified device.
             */
            params.deviceInfo = deviceInfo;
    
            /**Establishes a connection.**/
            LinkKit.getInstance().init(params, new ILinkKitConnectListener() {
                public void onError(AError aError) {
                    ALog.e(TAG, "Init Error error=" + aError);
                }
    
                public void onInitDone(InitResult initResult) {
                    ALog.i(TAG, "onInitDone result=" + initResult);
    
                    List<Property> properties =   LinkKit.getInstance().getDeviceThing().getProperties();
    
                    ALog.i(TAG, "List of device properties" + JSON.toJSONString(properties));
    
                    List<Event> getEvents  =   LinkKit.getInstance().getDeviceThing().getEvents();
    
                    ALog.i(TAG, "List of device events" + JSON.toJSONString(getEvents));
    
                    //Reports a property.
                    handlePropertySet("MicSwitch", new ValueWrapper.IntValueWrapper(3));
    
                    Map<String,ValueWrapper> values = new HashMap<>();
                    values.put("eventValue",new ValueWrapper.IntValueWrapper(0));
                    OutputParams outputParams = new OutputParams(values);
                    //Reports an event.
                     handleEventSet("Offline_alarm",outputParams);
    
                }
            });
        }
    ```

    **Note:** The property and event identifiers in the code must be the same as the identifiers defined in the TSL model.

-   Configure the SDK for the device to report properties.

    ```
    /**
         * The device reports properties in the Alink JSON format.
         * @param identifier  The identifier of the property.
         * @param value       The value of the property.
         * @return
         */
        private void handlePropertySet(String identifier, ValueWrapper value ) {
            ALog.i(TAG, "Identifier of the property=" + identifier);
    
            Map<String, ValueWrapper> reportData = new HashMap<>();
            reportData.put(identifier, value);
    
            LinkKit.getInstance().getDeviceThing().thingPropertyPost(reportData, new IPublishResourceListener() {
    
                public void onSuccess(String s, Object o) {
                    // The property is reported.
                    ALog.i(TAG, "Reported. onSuccess() called with: s = [" + s + "], o = [" + o + "]");
                }
    
                public void onError(String s, AError aError) {
                    // Failed to report the property.
                    ALog.i(TAG, "Failed to report. onError() called with: s = [" + s + "], aError = [" + JSON.toJSONString(aError) + "]");
                }
            });
        }
    ```

-   Configure the SDK for the device to report events.

    ```
    /**
         * The device reports events in the Alink JSON format.
         * @param identifyID  The identifier of the event.
         * @param params      The parameters of the event.
         * @return
         */
        private void handleEventSet(String identifyID, OutputParams params ) {
            ALog.i(TAG, "Identifier of the event=" + identifyID + "  params=" + JSON.toJSONString(params));
    
    
            LinkKit.getInstance().getDeviceThing().thingEventPost( identifyID,  params, new IPublishResourceListener() {
    
                public void onSuccess(String s, Object o) {
                    // The event is reported.
                    ALog.i(TAG, "Reported. onSuccess() called with: s = [" + s + "], o = [" + o + "]");
                }
    
                public void onError(String s, AError aError) {
                    // Failed to report the event.
                    ALog.i(TAG, "Failed to report. onError() called with: s = [" + s + "], aError = [" + JSON.toJSONString(aError) + "]");
                }
            });
        }
    ```


## The server SDK of IoT Platform issues commands to set properties and invoke services

-   Initialize the SDK client.

    The IotClient file in the directory java/src/main/com.aliyun.iot.client contains the demo for initializing the SDK client.

    ```
    public class IotClient {
      private static String accessKeyID;
      private static String accessKeySecret;
      private static String regionId;
        private static String domain;
        private static String version;
        public static DefaultAcsClient getClient() {
        DefaultAcsClient client = null;
        Properties prop = new Properties();
        try {
          prop.load(Object.class.getResourceAsStream("/config.properties"));
          accessKeyID = prop.getProperty("user.accessKeyID");
          accessKeySecret = prop.getProperty("user.accessKeySecret");
          regionId = prop.getProperty("iot.regionId");
                domain = prop.getProperty("iot.domain");
                version = prop.getProperty("iot.version");
    
          IClientProfile profile = DefaultProfile.getProfile(regionId, accessKeyID, accessKeySecret);
          DefaultProfile.addEndpoint(regionId, regionId, prop.getProperty("iot.productCode"),
              prop.getProperty("iot.domain"));
          // Initializes the client.
          client = new DefaultAcsClient(profile);
    
        } catch (Exception e) {
          LogUtil.print("Failed to initialize the client. exception:" + e.getMessage());
        }
        return client;
      }
        public static String getRegionId() {
            return regionId;
        }
        public static void setRegionId(String regionId) {
            IotClient.regionId = regionId;
        }
        public static String getDomain() {
            return domain;
        }
        public static void setDomain(String domain) {
            IotClient.domain = domain;
        }
        public static String getVersion() {
            return version;
        }
        public static void setVersion(String version) {
            IotClient.version = version;
        }
    }
    ```

-   Initialize the CommonRequest public class encapsulated in the demo.

    The AbstractManager file in the directory java/src/main/com.aliyun.iot.api.common.openApi contains the demo that encapsulates the CommonRequest public class. You can use the public class to call API operations of IoT Platform.

    ```
    public class AbstractManager {
        private static DefaultAcsClient client;
        static {
            client = IotClient.getClient();
        }
        /**
         *  action: the operation that you want to perform.
         *  domain: the endpoint of the service of IoT Platform.
         *  version: the version of the operation.
         */
        public static CommonRequest executeTests(String action) {
            CommonRequest request = new CommonRequest();
            request.setDomain(IotClient.getDomain());
            request.setMethod(MethodType.POST);
            request.setVersion(IotClient.getVersion());
            request.setAction(action);
            return request;
        }
    ```

-   Configure the server SDK to call the API operations of IoT platform, and issue corresponding commands to set properties and invoke services.

    The file ThingManagerForPopSDk in the directory java/src/main/com.aliyun.iot.api.common.openApi contains the server SDK demo for calling API operations to set properties and invoke services.

    -   Call the [SetDeviceProperty](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/SetDeviceProperty.md) operation to set a device property.

        ```
        public static void SetDeviceProperty(String IotId, String ProductKey, String DeviceName , String Items) {
                SetDevicePropertyResponse response =null;
                SetDevicePropertyRequest request=new SetDevicePropertyRequest();
                request.setDeviceName(DeviceName);
                request.setIotId(IotId);
                request.setItems(Items);
                request.setProductKey(ProductKey);
        
                try {
                    response = client.getAcsResponse(request);
        
                    if (response.getSuccess() ! = null && response.getSuccess()) {
                        LogUtil.print("The device property is set.");
                        LogUtil.print(JSON.toJSONString(response));
                    } else {
                        LogUtil.print("Failed to set device property.");
                        LogUtil.error(JSON.toJSONString(response));
                    }
        
                } catch (ClientException e) {
                    e.printStackTrace();
                    LogUtil.error("Failed to set device property." + JSON.toJSONString(response));
                }
            }
        ```

    -   Call the [SetDevicesProperty](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/SetDevicesProperty.md) operation to set same properties of multiple devices under the same product.

        ```
        /**
             * Set the same properties of multiple devices under the same product.
             *
             * @param ProductKey      The ProductKey that the target devices belong to.
             * @param DeviceNames     The list of the target devices.
             * @param Items  The property key:value list in JSON format.  You must specify this parameter.
             *
             * @Des Description:
             */
            public static void SetDevicesProperty(String ProductKey, List<String> DeviceNames, String Items) {
                SetDevicesPropertyResponse response = new SetDevicesPropertyResponse();
                SetDevicesPropertyRequest request = new SetDevicesPropertyRequest();
                request.setDeviceNames(DeviceNames);
                request.setItems(Items);
                request.setProductKey(ProductKey);
        
                try {
                    response = client.getAcsResponse(request);
        
                    if (response.getSuccess() ! = null && response.getSuccess()) {
                        LogUtil.print("The properties are set.");
                        LogUtil.print(JSON.toJSONString(response));
                    } else {
                        LogUtil.print("Failed to set the properties.");
                        LogUtil.error(JSON.toJSONString(response));
                    }
                } catch (ClientException e) {
                    e.printStackTrace();
                    LogUtil.error("Failed to set the properties." + JSON.toJSONString(response));
                }
            }
        ```

    -   Call the [InvokeThingService](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/InvokeThingService.md) operation to invoke a device service.

        ```
             /**
             * @param Identifier The identifier of the service. You must specify this parameter.
             * @param Args       The arguments for invoking the target service. You must specify this parameter.
             */
            public static InvokeThingServiceResponse.Data InvokeThingService(String IotId, String ProductKey, String DeviceName,
                                                                             String Identifier, String Args) {
                InvokeThingServiceResponse response =null;
                InvokeThingServiceRequest request = new InvokeThingServiceRequest();
                request.setArgs(Args);
                request.setDeviceName(DeviceName);
                request.setIotId(IotId);
                request.setIdentifier(Identifier);
                request.setProductKey(ProductKey);
        
                try {
                    response = client.getAcsResponse(request);
        
                    if (response.getSuccess() ! = null && response.getSuccess()) {
                        LogUtil.print("The service is invoked.");
                        LogUtil.print(JSON.toJSONString(response));
                    } else {
                        LogUtil.print("Failed to invoke the service.");
                        LogUtil.error(JSON.toJSONString(response));
                    }
                    return response.getData();
        
                } catch (ClientException e) {
                    e.printStackTrace();
                    LogUtil.error("Failed to invoke the service." + JSON.toJSONString(response));
                }
                return null;
            }
        ```

    -   Call the [InvokeThingsService](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/InvokeThingsService.md) operation to invoke the same service of multiple devices.

        ```
             /**
             * @param Identifier  The identifier of the service. You must specify this parameter.
             * @param Args The arguments for invoking the service. You must the specify this parameter.
             */
            public static void InvokeThingsService(String IotId, String ProductKey, List<String> DeviceNames,
                                                   String Identifier, String Args) {
                InvokeThingsServiceResponse response =null;
                InvokeThingsServiceRequest request = new InvokeThingsServiceRequest();
                request.setArgs(Args);
                request.setIdentifier(Identifier);
                request.setDeviceNames(DeviceNames);
                request.setProductKey(ProductKey);
        
        
                try {
                    response = client.getAcsResponse(request);
        
                    if (response.getSuccess() ! = null && response.getSuccess()) {
                        LogUtil.print("The services are invoked.");
                        LogUtil.print(JSON.toJSONString(response));
                    } else {
                        LogUtil.print("Failed to invoke the services.");
                        LogUtil.error(JSON.toJSONString(response));
                    }
        
                } catch (ClientException e) {
                    e.printStackTrace();
                    LogUtil.error("Failed to invoke the services." + JSON.toJSONString(response));
                }
            }
        ```


Sample requests for setting properties and invoking services:

```
public static void main(String[] args) {
        /**Connects a device to IoT Platform.*/
        String deviceName = "2pxuAQB2I7wGPmqq****";
        String deviceProductkey = "a1QbjI2***";
        //1. Sets a property of the device.
        SetDeviceProperty(null, deviceProductkey, deviceName,"{\"hue\":0}");
        //2. Sets the same property of multiple devices under the same product.
        List<String>  deviceNames = new ArrayList<>();
        deviceNames.add(deviceName);
        SetDevicesProperty(deviceProductkey, deviceNames, "{\"hue\":0}");
        //3. Invokes the service of the specified device.
        InvokeThingService(null, deviceProductkey, deviceName, "ModifyVehicleInfo", "{}");
        //4. Invokes the same service of multiple devices.
        List<String>  deviceNamesService = new ArrayList<>();
        deviceNamesService.add(deviceName);
        InvokeThingsService(null, deviceProductkey, deviceNamesService, "ModifyVehicleInfo", "{}");
    }
```

## Debug the SDKs

After you configure the device SDK and server SDK, run these SDKs.

Check results:

-   Check local logs.

    ![TSL model communication](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2837549951/p54075.png)

-   Go to the IoT Platform console, click the name of the device to go the Device Details page.

    -   Click the Status tab to check the property values that the device reported last time.
    -   Click the Events tab to check the events that the device reported last time.
    -   Click the Invoke Service tab to check the records of invoking services.
    ![TSL model communication](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2837549951/p54079.png)



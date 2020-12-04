# Call a synchronous service

To meet the requirements for managing devices and obtaining responses from the devices, IoT Platform provides synchronous services. This topic describes how to call a synchronous service.

A server calls an IoT Platform API operation to invoke a synchronous service. IoT Platform sends a request to a device. Then, the device responds to the request within a certain period of time and returns the results to IoT Platform. Servers use synchronous services to manage devices and obtain results from devices. IoT Platform calls synchronous services by using Revert-RPC \(RRPC\). For more information, see [Invoke device services in an asynchronous manner](/intl.en-US/Device Management/Develop devices based on Alink Protocol/Device properties, events, and services.md).

## Precautions

-   Before you can call a synchronous service, make sure that the device that the synchronous service manages is in the online state.
-   After IoT Platform calls a synchronous service, the maximum timeout period for IoT Platform to wait before a response is received is 8 seconds. If no response is received within 8 seconds, a timeout error occurs.

## Step 1: Create a custom service

1.  Log on to the [IoT Platform console](http://iot.console.aliyun.com/) by using an Alibaba Cloud account.

2.  In the left-side navigation pane, choose **Devices** \> **Products**, find the target product, and click **View** next to the product.

3.  On the Product Details page, click the Define Feature tab, and add a self-defined feature as shown in the following figure.

    ![Add a custom service](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0937549951/p135980.png)

    For more information about the required parameters that you need to specify for a custom service, see [Add a TSL feature](/intl.en-US/Device Management/TSL/Add a TSL feature.md).

4.  The following figure shows how to add **input parameters** and **output parameters**.

    ![Input parameters](../images/p135981.png "Input parameters")

    ![Output parameters](../images/p135985.png "Output parameters")


## Step 2: Create a device SDK-based application

1.  Add the following dependencies to the pom.xml file.

    ```
    <dependency>
      <groupId>com.aliyun.alink.linksdk</groupId>
      <artifactId>iot-linkkit-java</artifactId>
      <version>1.2.0.1</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.8.1</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>fastjson</artifactId>
      <version>1.2.40</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>com.google.guava</groupId>
      <artifactId>guava</artifactId>
      <version>23.0</version>
    </dependency>
    ```

2.  Add Java classes and specify the information of your device in the Config. \* file.

    ```
    /*   
     * Copyright © 2019 Alibaba. All rights reserved.
     */
    package com.aliyun.iot.demo.alink;
    
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.LinkedBlockingQueue;
    import java.util.concurrent.Executors;
    import java.util.concurrent.TimeUnit;
    
    import com.alibaba.fastjson.JSONObject;
    import com.aliyun.alink.dm.api.DeviceInfo;
    import com.aliyun.alink.dm.api.InitResult;
    import com.aliyun.alink.linkkit.api.ILinkKitConnectListener;
    import com.aliyun.alink.linkkit.api.IoTMqttClientConfig;
    import com.aliyun.alink.linkkit.api.LinkKit;
    import com.aliyun.alink.linkkit.api.LinkKitInitParams;
    import com.aliyun.alink.linksdk.cmp.connect.channel.MqttPublishRequest;
    import com.aliyun.alink.linksdk.cmp.core.base.AMessage;
    import com.aliyun.alink.linksdk.cmp.core.base.ARequest;
    import com.aliyun.alink.linksdk.cmp.core.base.AResponse;
    import com.aliyun.alink.linksdk.cmp.core.base.AMessage;
    import com.aliyun.alink.linksdk.cmp.core.listener.IConnectNotifyListener;
    import com.aliyun.alink.linksdk.cmp.core.listener.IConnectSendListener;
    import com.aliyun.alink.linksdk.tools.AError;
    import com.google.common.util.concurrent.ThreadFactoryBuilder;
    
    /**
     * Call a synchronous service.
     */
    public class SyncServiceProcessor {
    
      // ===================The start of the section where you can specify the required parameters===========================
      // Specify the information of your device in the Config. * file.
      // The ID of the region. 
      private static String regionId = "cn-shanghai";
      // The productKey specifies the key of a product.
      private static String productKey = "Config.productKey";
      // The deviceName specifies the name of a device.
      private static String deviceName = "Config.deviceName";
      // The deviceSecret specifies the key of the device.
      private static String deviceSecret = "Config.deviceSecret";
      // ===================The end of the section where you can specify the required parameters===========================
    
      private static ExecutorService executorService = new ThreadPoolExecutor(Runtime.getRuntime().availableProcessors(),
          Runtime.getRuntime().availableProcessors() * 2, 60, TimeUnit.SECONDS, new LinkedBlockingQueue<>(100),
          new ThreadFactoryBuilder().setDaemon(true).setNameFormat("http2-downlink-handle-%d").build(),
          new ThreadPoolExecutor.AbortPolicy());
    
      /**
       * 1 Start the application to simulate an online device. <br>
       * 2 Initialize an InvokeSyncService object to call a synchronous service.<br>
       * 
       * @param args
       * @throws InterruptedException
       */
      public static void main(String[] args) throws InterruptedException {
    
        // Listen for downstream data.
        registerNotifyListener();
    
        // Connect the device to IoT Platform.
        connect(productKey, deviceName, deviceSecret);
      }
    
      /**
       * Establish a connection.
       * 
       * @param productKey The key of the product.
       * @param deviceName The name of the device.
       * @param deviceSecret The key of the device.
       * @throws InterruptedException
       */
      private static void connect(String productKey, String deviceName, String deviceSecret) throws InterruptedException {
    
        // Initialize parameters.
        LinkKitInitParams params = new LinkKitInitParams();
    
        // Specify MQTT-related initialization parameters.
        IoTMqttClientConfig config = new IoTMqttClientConfig();
        config.channelHost = productKey + ".iot-as-mqtt." + regionId + ".aliyuncs.com:1883";
        config.productKey = productKey;
        config.deviceName = deviceName;
        config.deviceSecret = deviceSecret;
        params.mqttClientConfig = config;
    
        // Specify the certificate information of the device.
        DeviceInfo deviceInfo = new DeviceInfo();
        deviceInfo.productKey = productKey;
        deviceInfo.deviceName = deviceName;
        deviceInfo.deviceSecret = deviceSecret;
        params.deviceInfo = deviceInfo;
    
        // Initialize the device.
        LinkKit.getInstance().init(params, new ILinkKitConnectListener() {
          public void onError(AError aError) {
            System.out.println("init failed !! code=" + aError.getCode() + ",msg=" + aError.getMsg() + ",subCode="
                + aError.getSubCode() + ",subMsg=" + aError.getSubMsg());
          }
    
          public void onInitDone(InitResult initResult) {
            System.out.println("upload success!") ;
          }
        });
    
        // Before you proceed to the following steps, make sure the initialization is complete. You can specify a custom value based on your business requirement.
        Thread.sleep(2000);
      }
    
      /**
       * Send messages.
       * 
       @param topic The topic to which messages are sent.
       * @param payload The contents of messages.
       */
      private static void publish(String topic, String payload) {
        MqttPublishRequest request = new MqttPublishRequest();
        request.topic = topic;
        request.payloadObj = payload;
        request.qos = 0;
        LinkKit.getInstance().getMqttClient().publish(request, new IConnectSendListener() {
          @Override
          public void onResponse(ARequest aRequest, AResponse aResponse) {
          }
    
          @Override
          public void onFailure(ARequest aRequest, AError aError) {
          }
        });
      }
    
      /**
       * Listen for downstream data.
       */
      private static void registerNotifyListener() {
        LinkKit.getInstance().registerOnNotifyListener(new IConnectNotifyListener() {
          @Override
          public boolean shouldHandle(String connectId, String topic) {
            return true;
          }
    
          @Override
          public void onNotify(String connectId, String topic, AMessage aMessage) {
            // Accept the call from the synchronous service and response to the service.
            // Create a new thread to avoid callback blocks.
            executorService.submit(() -> doService(topic, aMessage));
          }
    
          @Override
          public void onConnectStateChange(String s, ConnectState connectState) {
          }
        });
      }
    
      /**
       * Process the request that is used to call the synchronous service.
       * 
       * @param topic The topic of the request.
       * @param aMessage The contents of the request.
       */
      private static void doService(String topic, AMessage aMessage) {
    
        String content = new String((byte[]) aMessage.getData());
        System.out.println("Service Request Topic：" + topic);
        System.out.println("Service Request:" + content);
    
        /**
         * The aMessage parameter includes a JSON text.
         *   {
         *     "id": "123",
         *     "version": "1.0",
         *     "params": // The required parameters for the synchronous service. These parameters change based on the definition of the synchronous service.
         *       {
         *         "input": 50
         *     },
         *     "method": "thing.service.{tsl.service.identifier}"
         *   }
         */
        JSONObject request = JSONObject.parseObject(content);
        JSONObject params = request.getJSONObject("params");
        if (! params.containsKey("input")) { // Validate the request parameters.
          return;
        }
        Integer input = params.getInteger("input"); // Obtain the request parameters.
    
        /**
         * The response from the synchronous service includes a JSON text.
         *   {
         *     "id": "123",  // The ID of the request.
         *     "code": 200,  // The value 200 indicates a successful call. 
         *     "data": {}    // The response from the synchronous service. The response changes based on the definition of the synchronous service.
         *   }
         */
        JSONObject response = new JSONObject();
        JSONObject data = new JSONObject();
        data.put("output", input + 1);
        response.put("id", request.get("id"));
        response.put("code", 200);
        response.put("data", data);
    
        // The response from the synchonous service.
        String respTopic = topic.replace("/request/", "/response/");
        publish(respTopic, response.toString());
        System.out.println("Service Response Topic:" + respTopic);
        System.out.println("Service Response Contents" + response.toString());
      }
    }
    ```


## Step 3: Create a service SDK-based application

1.  Add the following dependencies to the pom.xml file.

    ```
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-iot</artifactId>
        <version>7.0.0</version>
    </dependency>
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-core</artifactId>
        <version>3.5.1</version>
    </dependency>
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>1.2.40</version>
    </dependency>
    ```

2.  Add the following Java classes and specify the information of your device in the Config. \* file.

    ```
    /*   
     * Copyright © 2019 Alibaba. All rights reserved.
     */
    package com.aliyun.iot.demo.alink;
    
    import com.alibaba.fastjson.JSONObject;
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.exceptions.ServerException;
    import com.aliyuncs.iot.model.v20180120.InvokeThingServiceRequest;
    import com.aliyuncs.iot.model.v20180120.InvokeThingServiceResponse;
    import com.aliyuncs.profile.DefaultProfile;
    import com.aliyuncs.profile.IClientProfile;
    
    /**
     * Call a synchronous service.
     */
    public class InvokeSyncService {
    
      ===============The start of the section where you can specify the required parameters========================================
      // Specify the information of your device in the Config. * file.
      // The ID of the region. 
      private static String regionId = "cn-shanghai";
      // The AccessKey ID of your Alibaba Cloud account.
      private static String accessKeyID = "Config.accessKey";
      // The AccesseKey secret of your Alibaba Cloud account.
      private static String accessKeySecret = "Config.accessKeySecret";
      // productKey. The key of a product.
      private static String productKey = "Config.productKey";
      // deviceName. The name of a device.
      private static String deviceName = "Config.deviceName";
      ==========================The end of the section where you need to specify the required parameters=============================
    
      /**
       * 1. Initialize the SyncServiceProcessor class to simulate an online device.<br>
       * 2. Start the application to call a synchronous service. <br>
       * 
       * @param args
       * @throws ServerException
       * @throws ClientException
       */
      public static void main(String[] args) throws ServerException, ClientException {
    
        // Obtain exceptions from a client.
        DefaultAcsClient client = null;
        try {
          IClientProfile profile = DefaultProfile.getProfile(regionId, accessKeyID, accessKeySecret);
          DefaultProfile.addEndpoint(regionId, regionId, "Iot", "iot." + regionId + ".aliyuncs.com");
          client = new DefaultAcsClient(profile);
        } catch (Exception e) {
          System.out.println("create OpenAPI Client failed !! exception:" + e.getMessage());
        }
    
        // Specify the required parameters.
        InvokeThingServiceRequest request = new InvokeThingServiceRequest();
        request.setProductKey(productKey); // The productKey specifies the key of the product.
        request.setDeviceName(deviceName); // The deviceName specifies the name of the device.
        request.setIdentifier("MySyncService"); // The identifier of the synchronous service that you want to call. The identifier changes based on the definition of the synchronous service.
        JSONObject json = new JSONObject(); // Create a request parameter. The request parameter includes a JSON string.
        json.put("input", 50); // You can specify a custom value based on the definition of the synchronous service.
        request.setArgs(json.toString());
    
        // Obtain a response from the synchronous service.
        InvokeThingServiceResponse response = client.getAcsResponse(request);
        if (response == null) {
          System.out.println("Failed to call the synchronous service");
          return;
        }
        System.out.println("requestId:" + response.getRequestId());
        System.out.println("code:" + response.getCode());
        System.out.println("success:" + response.getSuccess());
        System.out.println("error message:" + response.getErrorMessage());
        if (response ! = null && response.getSuccess()) { // The synchronous service is called successfully. The return value true indicates that a request is sent to the synchronous service rather than that the synchronous service is run successfully.
          System.out.println("The synchronous service is called");
          System.out.println("Message ID：" + response.getData().getMessageId());
          System.out.println("Results" + response.getData().getResult()); // If the synchronous service is called successfully, results are returned.
        } else {
          System.out.println("Failed to call the synchronous service");
        }
      }
    
    }
    ```



---
keyword: [IoT, Internet of Things, Paho.MQTT, Android]
---

# Using Paho MQTT Android client

This topic describes how to use Paho Android Service to access Alibaba Cloud IoT Platform and send and receive data.

Products and devices are created in IoT Platform.

For more information, see [Create a product](/intl.en-US/Device Access/Create a product.md) and [Create a device](/intl.en-US/Device Access/Create devices/Create a device.md).

The Paho Android Service is an MQTT client library based on the Java Paho MQTT Library.

## Prepare the development environment

In this example, Android Studio is of version 3.5.1 and Gradle is of version 3.5.1.

Visit the [Android Studio official website](https://developer.android.com/studio) to download Android Studio. For more information about Android development, see the Android Studio official documentation.

## Install Paho Android client

1.  Create an Android project.

2.  In the Gradle file, add the Paho Android client dependencies. In this example, PahoAndroidClient 1.1.1 is used.

    -   In the build.gradle project, add the Paho repository address. This example uses the release repository.

        ```
        repositories {
            maven {
                url "https://repo.eclipse.org/content/repositories/paho-releases/"
            }
        }
        ```

    -   In the build.gradle project, add Paho Android Service. In this example, the Paho Android Service 1.1.1 is used. It is based on paho.client.mqttv3-1.1.0.

        ```
        dependencies {
            implementation 'org.eclipse.paho:org.eclipse.paho.client.mqttv3:1.1.0'
            implementation 'org.eclipse.paho:org.eclipse.paho.android.service:1.1.1'
        }
        ```

3.  To bind an app to the Paho Android Service, you add the following information to AndroidManifest.xml.

    -   Add the following services.

        ```
        <! -- Mqtt Service -->
        <service android:name="org.eclipse.paho.android.service.MqttService">
        </Service>
        ```

    -   Add required permissions for the Paho MQTT Service.

        ```
        <uses-permission android:name="android.permission.WAKE_LOCK" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        ```


## Connect to IoT Platform

1.  Click [AiotMqttOption.java](http://code.aliyun.com/edward.yangx/public-docs/wikis/user-guide/linkkit/Paho_MQTT_Guide/AiotMqttOption.java) to download the source code provided by Alibaba Cloud to calculate the MQTT connection parameters.

    The AiotMqttOption.java file defines the AiotMqttOption\(\) class.

    -   Prototype

        ```
        class AiotMqttOption
        ```

    -   Functionality

        Calculates the username, password, and clientId parameters for MQTT connections to IoT Platform.

    -   Methods

        |Type|Method description|
        |----|------------------|
        |public AiotMqttOption|`getMqttOption(String productKey, String deviceName, String deviceSecret)`You can call this method to calculate the username, password, and clientid based on the productKey, deviceName, and deviceSecret of the device. |
        |public String|`getUsername()`You can call this method to obtain the MQTT connection parameter username. |
        |public String|`getPassword()`You can call this method to obtain the MQTT connection parameter password. |
        |public String|`getClientid()`You can call this method to obtain the MQTT connection parameter clientid. |

2.  Import AiotMqttOption.java to the Android project.

3.  In the Android project, add a program file that enables devices to access IoT Platform.

    You must write a program which can call the AiotMqttOption\(\) class in the AiotMqttOption.java file to calculate the MQTT connection parameters for communications with IoT Platform.

    The development instructions and sample code are as follows.

    -   Calculate the MQTT connection parameters clientId,username, and password. Configure the username and password parameters in the MqttConnectOptions object.

        ```
        final private String PRODUCTKEY = "a11xsrW****";
        final private String DEVICENAME = "paho_android";
        final private String DEVICESECRET = "tLMT9QWD36U2SArglGqcHCDK9rK9****";
        
        /* Obtain the MQTT connection information clientId, username, and password. */
        AiotMqttOption aiotMqttOption = new AiotMqttOption().getMqttOption(PRODUCTKEY, DEVICENAME, DEVICESECRET);
        if (aiotMqttOption == null) {
            Log.e(TAG, "device info error");
        } else {
            clientId = aiotMqttOption.getClientId();
            userName = aiotMqttOption.getUsername();
            passWord = aiotMqttOption.getPassword();
        }
        
        /* Create an MqttConnectOptions object and configure the username and password. */
        MqttConnectOptions mqttConnectOptions = new MqttConnectOptions();
        mqttConnectOptions.setUserName(userName);
        mqttConnectOptions.setPassword(passWord.toCharArray());
        ```

    -   Connect the device to IoT Platform.

        Create an MqttAndroidClient object, and set the callback interface. Use the mqttConnectOptions object to call the connect\(\) method and establish the connection.

        ```
        /* Create an MqttAndroidClient object and set a callback interface. */
        mqttAndroidClient = new MqttAndroidClient(getApplicationContext(), host, clientId);
        mqttAndroidClient.setCallback(new MqttCallback() {
            @Override
            public void connectionLost(Throwable cause) {
                Log.i(TAG, "connection lost");
            }
        
            @Override
            public void messageArrived(String topic, MqttMessage message) throws Exception {
                Log.i(TAG, "topic: " + topic + ", msg: " + new String(message.getPayload()));
            }
        
            @Override
            public void deliveryComplete(IMqttDeliveryToken token) {
                Log.i(TAG, "msg delivered");
            }
        });
        
        /* Establish an MQTT connection */
        try {
            mqttAndroidClient.connect(mqttConnectOptions, null, new IMqttActionListener() {
                @Override
                public void onSuccess(IMqttToken asyncActionToken) {
                    Log.i(TAG, "connect succeed");
        
                    subscribeTopic(SUB_TOPIC);
                }
        
                @Override
                public void onFailure(IMqttToken asyncActionToken, Throwable exception) {
                    Log.i(TAG, "connect failed");
                }
            });
        
        } catch (MqttException e) {
            e.printStackTrace();
        }
        ```

    -   Publishes messages.

        Encapsulate the publish method.

        ```
        public void publishMessage(String payload) {
            try {
                if (mqttAndroidClient.isConnected() == false) {
                    mqttAndroidClient.connect();
                }
        
                MqttMessage message = new MqttMessage();
                message.setPayload(payload.getBytes());
                message.setQos(0);
                mqttAndroidClient.publish(PUB_TOPIC, message,null, new IMqttActionListener() {
                    @Override
                    public void onSuccess(IMqttToken asyncActionToken) {
                        Log. I (TAG, "publish succeed! ") ;
                    }
        
                    @Override
                    public void onFailure(IMqttToken asyncActionToken, Throwable exception) {
                        Log.i(TAG, "publish failed!") ;
                    }
                });
            } catch (MqttException e) {
                Log.e(TAG, e.toString());
                e.printStackTrace();
            }
        }
        ```

        For more information about communication topics, see[What is a topic?](/intl.en-US/Device Access/Topics/What is a topic?.md).

    -   Encapsulate the subscribe\(\) method. You can use this method to subscribe to a specified topic and obtain messages from the cloud.

        ```
        public void subscribeTopic(String topic) {
            try {
                mqttAndroidClient.subscribe(topic, 0, null, new IMqttActionListener() {
                    @Override
                    public void onSuccess(IMqttToken asyncActionToken) {
                        Log.i(TAG, "subscribed succeed");
                    }
        
                    @Override
                    public void onFailure(IMqttToken asyncActionToken, Throwable exception) {
                        Log.i(TAG, "subscribed failed");
                    }
                });
        
            } catch (MqttException e) {
                e.printStackTrace();
            }
        }
        ```

    For more information about the communication methods of devices, servers, and IoT Platform, see [Communication methods](/intl.en-US/Communications/Overview.md).

4.  Compile the project.


## Demo

Use the Demo code to access the IoT Platform.

1.  Click [here](https://code.aliyun.com/edward.yangx/public-docs/wikis/user-guide/linkkit/Paho_MQTT_Guide/aiot-android-demo.zip) to download the Demo package and decompress it.

2.  Import the aiot-csharp-demo file to Android Studio.

3.  In the MainActivity file of the app/src/main/java/com.linkkit.aiot\_android\_demo directory, replace the device information with your device information.

    -   Replace the productKey, deviceName, and deviceSecret with your device information.
    -   Replace cn-shanghai in `final String host = "tcp://" + PRODUCTKEY + ".iot-as-mqtt.cn-shanghai.aliyuncs.com:443";` with the region ID of your IoT Platform device. For more information about region IDs, see [Regions and zones]().
4.  Create and run the application.

    After running the application, you can view the local logs in Logcat.

    ```
    2019-12-04 19:44:01.824 5952-5987/com.linkkit.aiot_android_demo W/OpenGLRenderer: Failed to choose config with EGL_SWAP_BEHAVIOR_PRESERVED, retrying without...
    2019-12-04 19:44:01.829 5952-5987/com.linkkit.aiot_android_demo D/EGL_emulation: eglCreateContext: 0xec073240: maj 3 min 0 rcv 3
    2019-12-04 19:44:01.830 5952-5987/com.linkkit.aiot_android_demo D/EGL_emulation: eglMakeCurrent: 0xec073240: ver 3 0 (tinfo 0xec09b470)
    2019-12-04 19:44:01.852 5952-5987/com.linkkit.aiot_android_demo W/Gralloc3: mapper 3.x is not supported
    2019-12-04 19:44:01.854 5952-5987/com.linkkit.aiot_android_demo D/HostConnection: createUnique: call
    ...
    ...
    2019-12-04 19:44:01.860 5952-5987/com.linkkit.aiot_android_demo D/eglCodecCommon: allocate: Ask for block of size 0x1000
    2019-12-04 19:44:01.861 5952-5987/com.linkkit.aiot_android_demo D/eglCodecCommon: allocate: ioctl allocate returned offset 0x3ff706000 size 0x2000
    2019-12-04 19:44:01.897 5952-5987/com.linkkit.aiot_android_demo D/EGL_emulation: eglMakeCurrent: 0xec073240: ver 3 0 (tinfo 0xec09b470)
    2019-12-04 19:44:02.245 5952-6023/com.linkkit.aiot_android_demo D/AlarmPingSender: Register alarmreceiver to MqttServiceMqttService.pingSender.a11xsrW****.paho_android|timestamp=1575459841629,_v=sdk-android-1.0.0,securemode=2,signmethod=hmacsha256|
    2019-12-04 19:44:02.256 5952-6023/com.linkkit.aiot_android_demo D/AlarmPingSender: Schedule next alarm at 1575459902256
    2019-12-04 19:44:02.256 5952-6023/com.linkkit.aiot_android_demo D/AlarmPingSender: Alarm scheule using setExactAndAllowWhileIdle, next: 60000
    2019-12-04 19:44:02.272 5952-5952/com.linkkit.aiot_android_demo I/AiotMqtt: connect succeed
    2019-12-04 19:44:02.301 5952-5952/com.linkkit.aiot_android_demo I/AiotMqtt: subscribed succeed
    ```

    In the [IoT Platform console](http://iot.console.aliyun.com/), you can view the device status and logs.

    -   Choose **Devices** \> **Devices**. You can view that the status of the device is **Online**.
    -   Choose **Maintenance** \> **Device Log**. You can view the **Device Activity Analysis** and **Upstream Analysis** logs.


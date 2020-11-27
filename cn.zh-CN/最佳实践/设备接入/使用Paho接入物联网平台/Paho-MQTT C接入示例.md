---
keyword: [IoT, 物联网, Paho.MQTT. C]
---

# Paho-MQTT C接入示例

本文介绍如何使用Paho提供的嵌入式C语言MQTT开源工程接入阿里云物联网平台，并进行消息收发。

已在物联网平台中，创建了产品和设备。

请参见[创建产品](/cn.zh-CN/设备接入/创建产品.md)和[单个创建设备](/cn.zh-CN/设备接入/创建设备/单个创建设备.md)。

## 准备开发环境

本示例使用Ubuntu 16.04-LTS作为开发环境。执行以下命令构建开发环境。

```
sudo apt-get update
sudo apt-get install build-essential git sed cmake
```

## 下载C语言Paho MQTT库

执行以下命令，克隆C语言版本的Paho MQTT库。

```
git clone https://github.com/eclipse/paho.mqtt.embedded-c.git
```

**说明：** 编写本Demo示例时，使用master分支，commit id为`29ab2aa29c5e47794284376d7f8386cfd54c3eed`。

Paho嵌入式C工程提供了以下三个子项目：

-   MQTTPacket：提供MQTT数据包的序列化与反序列化，以及部分辅助函数。
-   MQTTClient：封装MQTTPacket生成的高级别C++客户端程序。
-   MQTTClient-C：封装MQTTPacket生成的高级别C客户端程序。

    MQTTClient-C中包含：

    ```
    ├── CMakeLists.txt
    ├── samples
    │   ├── CMakeLists.txt
    │   ├── FreeRTOS
    │   └── linux
    ├── src
    │   ├── CMakeLists.txt
    │   ├── FreeRTOS
    │   ├── MQTTClient.c
    │   ├── MQTTClient.h
    │   ├── cc3200
    │   └── linux
    └── test
        ├── CMakeLists.txt
        └── test1.c
    ```

    -   samples目录提供FreeRTOS和linux两个例程，分别支持FreeRTOS和Linux系统。
    -   src目录提供MQTTClient的代码实现能力，以及用于移植到FreeRTOS、cc3200和Linux的网络驱动。
    了解Paho MQTT的更多API细节，可以查看MQTTClient.h。


## 接入物联网平台

1.  单击打开[aiot\_mqtt\_sign.c](http://code.aliyun.com/edward.yangx/public-docs/wikis/user-guide/linkkit/Paho_MQTT_Guide/aiot_mqtt_sign.c?spm=a2c4g.11186623.2.19.704d6870eOnCNr&file=aiot_mqtt_sign.c)，下载阿里云提供的计算MQTT连接参数所需的源码。

    aiot\_mqtt\_sign.c文件定义了函数aiotMqttSign\(\)，函数说明如下：

    -   原型：

        ```
        int aiotMqttSign(const char *productKey, const char *deviceName, const char *deviceSecret,
                         char clientId[150], char username[65], char password[65]);
        ```

    -   功能：

        用于计算设备接入物联网平台的MQTT连接参数username、password和clientid。

    -   输入参数：

        |参数|类型|说明|
        |--|--|--|
        |productKey|const char \*|设备所属产品的ProductKey，该设备在物联网平台上的身份证书信息之一。|
        |deviceName|const char \*|设备名称，该设备在物联网平台上的身份证书信息之一。|
        |deviceSecret|const char \*|设备密钥，该设备在物联网平台上的身份证书信息之一。|

    -   输出参数：

        |参数|类型|说明|
        |--|--|--|
        |username|char \*|MQTT连接所需的用户名。|
        |password|char \*|MQTT连接所需的密码。|
        |clientId|char \*|MQTT客户端ID。|

    -   返回码说明：

        |返回码|说明|
        |---|--|
        |0|成功|
        |-1|失败|

2.  添加实现设备接入物联网平台的程序文件。

    您需编写程序调用aiot\_mqtt\_sign.c中的aiotMqttSign\(\)函数计算MQTT连接参数，实现接入物联网平台和通信。

    开发说明和示例代码如下：

    -   调用aiotMqttSign\(\)接口，生成连接MQTT服务端的三个建连参数clientId、username和password。

        ```
        #define EXAMPLE_PRODUCT_KEY            "a11xsrW****"
        #define EXAMPLE_DEVICE_NAME            "paho_****"
        #define EXAMPLE_DEVICE_SECRET       "Y877Bgo8X5owd3lcB5wWDjryNPoB****"
        
        extern int aiotMqttSign(const char *productKey, const char *deviceName, const char *deviceSecret,
                                char clientId[150], char username[65], char password[65]);
        
        /* invoke aiotMqttSign to generate mqtt connect parameters */
        char clientId[150] = {0};
        char username[65] = {0};
        char password[65] = {0};
        
        if ((rc = aiotMqttSign(EXAMPLE_PRODUCT_KEY, EXAMPLE_DEVICE_NAME, EXAMPLE_DEVICE_SECRET, clientId, username, password) < 0)) {
            printf("aiotMqttSign -%0x4x\n", -rc);
            return -1;
        }
        printf("clientid: %s\n", clientId);
        printf("username: %s\n", username);
        printf("password: %s\n", password);
        ```

    -   接入物联网平台。

        需配置以下内容：

        -   调用NetworkInit和NetworkConnect建立TCP连接。
        -   调用MQTTClientInit初始化MQTT客户端。
        -   配置MQTT建连参数结构体MQTTPacket\_connectData。
        示例代码：

        ```
        /* network init and establish network to aliyun IoT platform */
        NetworkInit(&n);
        rc = NetworkConnect(&n, host, port);
        printf("NetworkConnect %d\n", rc);
        
        /* init mqtt client */
        MQTTClientInit(&c, &n, 1000, buf, sizeof(buf), readbuf, sizeof(readbuf));
        
        /* set the default message handler */
        c.defaultMessageHandler = messageArrived;
        
        /* set mqtt connect parameter */
        MQTTPacket_connectData data = MQTTPacket_connectData_initializer;
        data.willFlag = 0;
        data.MQTTVersion = 3;
        data.clientID.cstring = clientId;
        data.username.cstring = username;
        data.password.cstring = password;
        data.keepAliveInterval = 60;
        data.cleansession = 1;
        printf("Connecting to %s %d\n", host, port);
        
        rc = MQTTConnect(&c, &data);
        printf("MQTTConnect %d, Connect aliyun IoT Cloud Success!\n", rc);
        ```

    -   发布消息。

        调用MQTTPublish\(\)接口，向指定的自定义Topic发布自定义格式消息。

        ```
        char *pubTopic = "/"EXAMPLE_PRODUCT_KEY"/"EXAMPLE_DEVICE_NAME"/user/update";
        int cnt = 0;
        unsigned int msgid = 0;
        while (!toStop)
        {
            MQTTYield(&c, 1000);    
        
            if (++cnt % 5 == 0) {
                MQTTMessage msg = {
                    QOS1,
                    0,
                    0,
                    0,
                    "Hello world",
                    strlen("Hello world"),
                };
                msg.id = ++msgid;
                rc = MQTTPublish(&c, pubTopic, &msg);
                printf("MQTTPublish %d, msgid %d\n", rc, msgid);
            }
        }
        ```

        通信Topic介绍，请参见[什么是Topic](/cn.zh-CN/设备接入/消息通信Topic/什么是Topic.md)。

    -   订阅Topic，获取云端下发的消息。

        ```
        void messageArrived(MessageData* md)
        {
            MQTTMessage* message = md->message;
        
            printf("%.*s\t", md->topicName->lenstring.len, md->topicName->lenstring.data);
            printf("%.*s\n", (int)message->payloadlen, (char*)message->payload);
        }
        
        char *subTopic = "/"EXAMPLE_PRODUCT_KEY"/"EXAMPLE_DEVICE_NAME"/user/get";
        
        printf("Subscribing to %s\n", subTopic);
        rc = MQTTSubscribe(&c, subTopic, 1, messageArrived);
        printf("MQTTSubscribe %d\n", rc);
        ```

    关于设备、服务器和物联网平台的通信方式介绍，请参见[通信方式概述](/cn.zh-CN/消息通信/通信方式概述.md)。

3.  将第一步下载的aiot\_mqtt\_sign.c文件和第二步编辑的文件放到../paho.mqtt.embedded-c/MQTTClient-C/samples/linux中，然后编译工程。


## 示例Demo

使用Demo代码程序接入物联网平台。

1.  [下载Demo包](https://linkkit-export.oss-cn-shanghai.aliyuncs.com/paho/aiot_c_demo.zip)，并解压缩。

    解压缩后，代码包里有以下两个文件：

    ```
    .
    +-- aiot_c_demo.c
    +-- aiot_mqtt_sign.c
    ```

    |文件|说明|
    |--|--|
    |aiot\_mqtt\_sign.c|该文件中的代码用于生成MQTT建连参数。aiot\_c\_demo.c运行时，会调用该文件中定义的aiotMqttSign\(\)函数，计算出连接参数username、password和clientId。|
    |aiot\_c\_demo.c|该文件包含设备与物联网平台连接和通信的逻辑代码。|

2.  在aiot\_c\_demo.c中，修改设备信息为您的设备信息。

    -   替换以下代码中EXAMPLE\_PRODUCT\_KEY、EXAMPLE\_DEVICE\_NAME和EXAMPLE\_DEVICE\_SECRET后的值为您的设备证书信息。

        ```
        #define EXAMPLE_PRODUCT_KEY            "产品ProductKey" 
        #define EXAMPLE_DEVICE_NAME            "设备名称DeviceName" 
        #define EXAMPLE_DEVICE_SECRET          "设备密钥DeviceSecret"
        ```

    -   修改代码`char *host = EXAMPLE_PRODUCT_KEY".iot-as-mqtt.cn-shanghai.aliyuncs.com"`中的值为对应接入域名。
        -   对于企业版实例：`char *host = "${企业版实例下接入域名}"`。

            您可登录[物联网平台控制台](https://iot.console.aliyun.com)，在**实例概览**页，找到并单击对应实例，进入实例详情页查看。具体操作，请参见[查看实例终端节点](/cn.zh-CN/.md)。

        -   对于公共实例：`char *host = "${EXAMPLE_PRODUCT_KEY}.iot-as-mqtt.cn-shanghai.aliyuncs.com"`。

            $\{EXAMPLE\_PRODUCT\_KEY\}替换为设备所属产品的ProductKey。您可登录[物联网平台控制台](https://iot.console.aliyun.com)在对应实例的设备详情页获取。

            地域代码（cn-shanghai）替换为您的物联网平台设备所在地域代码。地域代码的表达方法，请参见[地域和可用区]()。

3.  将aiot\_mqtt\_sign.c和已修改的aiot\_c\_demo.c文件放到Paho工程的目录../paho.mqtt.embedded-c/MQTTClient-C/samples/linux中。

4.  编译工程，并运行程序。

    有两种方法可以编译出可执行的程序：

    -   使用CMake。
        1.  在/paho.mqtt.embedded-c/MQTTClient-C/samples/linux目录下的CMakeLists.txt文件中，增加aiot\_c\_demo.c和aiot\_mqtt\_sign.c。

            修改后的CMakeLists.txt文件内容如下。

            ```
            add_executable(
              stdoutsubc
              stdoutsub.c
            )
            
            add_executable(
              aiot_c_demo
              aiot_c_demo.c
              aiot_mqtt_sign.c
            )
            
            target_link_libraries(stdoutsubc paho-embed-mqtt3cc paho-embed-mqtt3c)
            target_include_directories(stdoutsubc PRIVATE "../../src" "../../src/linux")
            target_compile_definitions(stdoutsubc PRIVATE MQTTCLIENT_PLATFORM_HEADER=MQTTLinux.h)
            
            target_link_libraries(aiot_c_demo paho-embed-mqtt3cc paho-embed-mqtt3c)
            target_include_directories(aiot_c_demo PRIVATE "../../src" "../../src/linux")
            target_compile_definitions(aiot_c_demo PRIVATE MQTTCLIENT_PLATFORM_HEADER=MQTTLinux.h)
            ```

        2.  回到/paho.mqtt.embedded-c目录，执行以下命令，完成编译。

            ```
            mkdir build.paho
            cd build.paho
            cmake ..
            make
            ```

        3.  编译完成后，在/paho.mqtt.embedded-c/build.paho目录下执行以下命令，运行程序。

            ```
            ./MQTTClient-C/samples/linux/aiot_c_demo
            ```

    -   使用build.sh。
        1.  修改/paho.mqtt.embedded-c/MQTTClient-C/samples/linux目录下的build.sh文件为以下内容：

            ```
            cp ../../src/MQTTClient.c .
            sed -e 's/""/"MQTTLinux.h"/g' ../../src/MQTTClient.h > MQTTClient.h
            gcc \
                -o aiot_c_demo \
                -I ../../src -I ../../src/linux -I ../../../MQTTPacket/src \
                aiot_mqtt_sign.c aiot_c_demo.c \
                MQTTClient.c \
                ../../src/linux/MQTTLinux.c \
                ../../../MQTTPacket/src/MQTTFormat.c \
                ../../../MQTTPacket/src/MQTTPacket.c \
                ../../../MQTTPacket/src/MQTTDeserializePublish.c \
                ../../../MQTTPacket/src/MQTTConnectClient.c \
                ../../../MQTTPacket/src/MQTTSubscribeClient.c \
                ../../../MQTTPacket/src/MQTTSerializePublish.c \
                ../../../MQTTPacket/src/MQTTConnectServer.c \
                ../../../MQTTPacket/src/MQTTSubscribeServer.c \
                ../../../MQTTPacket/src/MQTTUnsubscribeServer.c \
                ../../../MQTTPacket/src/MQTTUnsubscribeClient.c
            ```

        2.  修改完成后，在当前目录下执行命令`./build.sh`，完成编译。

            完成编译后，生成aiot\_c\_demo可执行文件。

        3.  执行命令`./aiot_c_demo`，运行程序。
    运行成功，接入物联网平台的本地日志如下：

    ```
    clientid: paho_mqtt&a11xsrW****|timestamp=2524608000000,_v=sdk-c-1.0.0,securemode=3,signmethod=hmacsha256,lan=C|
    username: paho_mqtt&a11xsrW****
    password: 36E955DC3D9D012EF62C80657A29328B1CFAE6186C611A17DC7939FAB637****
    NetworkConnect 0
    Connecting to a11xsrW****.iot-as-mqtt.cn-shanghai.aliyuncs.com 443
    MQTTConnect 0, Connect aliyun IoT Cloud Success!
    Subscribing to /a11xsrW****/paho_mqtt/user/get
    MQTTSubscribe 0
    MQTTPublish 0, msgid 1
    MQTTPublish 0, msgid 2
    MQTTPublish 0, msgid 3
    MQTTPublish 0, msgid 4
    MQTTPublish 0, msgid 5
    ...
    ```

    登录[物联网平台控制台](http://iot.console.aliyun.com/)，在对应的实例下，可查看设备状态和日志。

    -   选择**设备管理** \> **设备**，可看到该设备的状态显示为**在线**。
    -   选择**监控运维** \> **日志服务**，可查看**云端运行日志**和**设备本地日志**日志。详情请参见[云端运行日志](/cn.zh-CN/监控运维/日志服务/云端运行日志.md)、[设备本地日志](/cn.zh-CN/监控运维/日志服务/设备本地日志.md)。

## 错误码

如果设备通过MQTT协议接入物联网平台失败，请根据错误码排查问题。服务端错误码说明，请参见[错误排查](/cn.zh-CN/最佳实践/设备接入/使用Paho接入物联网平台/错误排查.md)。


---
keyword: [IoT, 物联网, Paho-MQTT C\#, .NET]
---

# Paho-MQTT C\#接入示例

本文档介绍如何使用C\#语言的Paho MQTT类库接入阿里云物联网平台，并进行物模型数据通信。

已在物联网平台中，创建了产品和设备，并在产品的功能定义页签下，定义一个LightSwitch属性。

请参见[创建产品](/cn.zh-CN/设备接入/创建产品.md)、[单个创建设备](/cn.zh-CN/设备接入/创建设备/单个创建设备.md)和[单个添加物模型](/cn.zh-CN/设备管理/物模型/单个添加物模型.md)。

Paho提供的MQTT C\#开源代码中，已包含Visual Studio解决方案工程。工程中的每个项目针对不同的.NET平台，可生成对应的类库。

本示例中，在工程中新建一个控制台应用项目， 调用Paho的MQTT类库连接阿里云物联网平台。

## 准备开发环境

本示例使用的操作系统和开发工具：

-   操作系统：Win10
-   集成开发环境：Visual Studio 2019

安装开发环境：

1.  下载[Visual Studio 2019社区版](https://visualstudio.microsoft.com/zh-hans/downloads/)，并解压缩。

2.  打开Visual Studio Installer，选择**.NET桌面开发**，单击**安装**。


## 下载Paho客户端

访问[Eclipse Paho](https://github.com/eclipse/paho.mqtt.m2mqtt)，从.Net（C\#）对应的GitHub中[下载Paho MQTT for C\#](https://github.com/eclipse/paho.mqtt.m2mqtt/archive/master.zip)。

编写本示例Demo时，使用master分支，commit id为`b2e64bc4485721a0bd5ae805d9f4917e8d040e81`。

Paho提供的源代码中，包含Visual Studio解决方案工程文件M2MMqtt.sln，可以使用该工程文件开发您自己的设备端。

## 接入物联网平台

1.  单击打开[MqttSign.cs](http://code.aliyun.com/edward.yangx/public-docs/wikis/user-guide/linkkit/Paho_MQTT_Guide/MqttSign.cs)，下载阿里云提供的计算MQTT连接参数所需的源码。

    MqttSign.cs文件中，定义了`MqttSign`类，类说明如下：

    -   原型：

        ```
        class MqttSign
        ```

    -   功能：

        用于计算设备接入物联网平台的MQTT连接参数username、password和clientid。

    -   成员：

        |类型定义|方法描述|
        |----|----|
        |public bool|`calculate(String productKey, String deviceName, String deviceSecret)`根据设备的productKey、deviceName和deviceSecret计算出MQTT连接参数username、password和clientid。 |
        |public String|`getUsername()`用于获取MQTT建连参数username。 |
        |public String|`getPassword()`用于获取MQTT建连参数password。 |
        |public String|`getClientid()`用于获取MQTT建连参数clientid。 |

2.  打开Visual Studio，导入Paho源代码中的Visual Studio解决方案文件M2Mqtt.sln，并创建一个应用项目。

3.  将第一步中下载的MqttSign.cs文件导入到应用项目中。

4.  在应用项目中，添加实现设备接入物联网平台的程序文件。

    您需编写程序调用MqttSign.cs中的MqttSign类计算MQTT连接参数，实现接入物联网平台和通信。

    开发说明和代码示例如下：

    -   计算MQTT连接参数。

        调用MqttSign.cs中的MqttSign计算MQTT连接参数。

        ```
        String productKey = "a1X2bEn****";
        String deviceName = "example1";
        String deviceSecret = "ga7XA6KdlEeiPXQPpRbAjOZXwG8y****";
        
        // 计算MQTT连接参数。
        MqttSign sign = new MqttSign();
        sign.calculate(productKey, deviceName, deviceSecret);
        
        Console.WriteLine("username: " + sign.getUsername());
        Console.WriteLine("password: " + sign.getPassword());
        Console.WriteLine("clientid: " + sign.getClientid());
        ```

    -   调用Paho MQTT客户端连接物联网平台。

        ```
        // 使用Paho连接阿里云物联网平台。
        int port = 443;
        String broker = productKey + ".iot-as-mqtt.cn-shanghai.aliyuncs.com";
        
        MqttClient mqttClient = new MqttClient(broker, port, true, MqttSslProtocols.TLSv1_2, null, null);
        mqttClient.Connect(sign.getClientid(), sign.getUsername(), sign.getPassword());
        
        Console.WriteLine("Broker: " + broker + " Connected");
        ```

        **说明：**

        -   对于企业版实例：`String broker = "${企业版实例下接入域名}"`。

            您可登录[物联网平台控制台](https://iot.console.aliyun.com)，在**实例概览**页，找到并单击对应实例，进入实例详情页查看。具体操作，请参见[查看实例终端节点](/cn.zh-CN/.md)。

        -   对于公共实例：`String broker = productKey + ".iot-as-mqtt.cn-shanghai.aliyuncs.com";`。

            其中，地域代码（cn-shanghai）替换为您的物联网平台设备所在地域代码。地域代码的表达方法，请参见[地域和可用区]()。

    -   设备上报数据到物联网平台。

        以下示例代码上报物模型属性LightSwitch。

        ```
        // Paho MQTT消息发布。
        String topic = "/sys/" + productKey + "/" + deviceName + "/thing/event/property/post";
        String message = "{\"id\":\"1\",\"version\":\"1.0\",\"params\":{\"LightSwitch\":0}}";
        mqttClient.Publish(topic, Encoding.UTF8.GetBytes(message));
        ```

        物模型通信数据格式，请参见[设备属性、事件、服务](/cn.zh-CN/设备管理/Alink协议/设备属性、事件、服务.md)。

        如果您要使用自定义Topic通信，请参见[什么是Topic](/cn.zh-CN/设备接入/消息通信Topic/什么是Topic.md)。

    -   订阅Topic，接收物联网平台下发数据。

        以下示例中，订阅的是上报属性值后，物联网平台返回应答消息的Topic。

        ```
        // Paho MQTT消息订阅。
        String topicReply = "/sys/" + productKey + "/" + deviceName + "/thing/event/property/post_reply";
        
        mqttClient.MqttMsgPublishReceived += MqttPostProperty_MqttMsgPublishReceived;
        mqttClient.Subscribe(new string[] { topicReply }, new byte[] { MqttMsgBase.QOS_LEVEL_AT_MOST_ONCE });
        ...
        private static void MqttPostProperty_MqttMsgPublishReceived(object sender, uPLibrary.Networking.M2Mqtt.Messages.MqttMsgPublishEventArgs e)
        {
            Console.WriteLine("reply topic  :" + e.Topic);
            Console.WriteLine("reply payload:" + e.Message.ToString());
        }
        ```

    关于设备、服务器和物联网平台的通信方式介绍，请参见[通信方式概述](/cn.zh-CN/消息通信/通信方式概述.md)。

5.  编译项目。


## 示例Demo

使用Demo代码程序接入物联网平台。

1.  [下载Demo代码包](https://linkkit-export.oss-cn-shanghai.aliyuncs.com/paho/aiot_c_demo.zip)，然后解压到文件夹aiot-csharp-demo。

    文件夹aiot-csharp-demo\\paho.mqtt.m2mqtt-master\\aiot-csharp-demo中，包含了设备接入物联网平台，并上报物模型属性的完整程序。

    |文件|说明|
    |--|--|
    |MqttSign.cs|阿里云提供的MQTT建连参数生成源代码。Program.cs运行时，会调用该文件中定义的MqttSign\(\)函数，计算出连接参数username、password和clientId。|
    |Program.cs|该文件包含设备与物联网平台连接，并上报属性数据的逻辑代码。|

2.  打开Visual Studio 2019社区版 , 选择**打开项目或解决方案**，打开aiot-csharp-demo\\paho.mqtt.m2mqtt-master\\M2Mqtt.sln文件。

    Visual Studio中即可导入aiot-csharp-demo项目文件。

3.  在Program.cs中，修改设备信息为您的设备信息。

    -   替换一下代码中productKey、deviceName和deviceSecret的值为您的设备证书信息。

        ```
        String productKey = "${ProductKey}";
        String deviceName = "${DeviceName}";
        String deviceSecret = "${DeviceSecret}";
        ```

    -   修改代码`String broker = productKey + ".iot-as-mqtt.cn-shanghai.aliyuncs.com";`中的接入域名。详细说明，请参见上文“接入物联网平台”中的步骤4。
4.  将aiot-csharp-demo设为启动项目，然后运行，将设备接入物联网平台。

    ![接入物联网平台](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3351186061/p72265.png)

    接入成功后，本地日志中包含连接成功、数据上报成功和订阅消息成功的内容。

    ```
    ...
    broker: a1X2bEn****.iot-as-mqtt.cn-shanghai.aliyuncs.com Connected
    ...
    publish: {"id":"1","version":"1.0","params":{"LightSwitch":0}}
    ...
    subscribe: /sys/a1X2bEn****/example1/thing/event/property/post_reply
    ...
    ```

    登录[物联网平台控制台](http://iot.console.aliyun.com/)，在对应的实例下，可查看设备状态和日志。

    -   选择**设备管理** \> **设备**，可看到该设备的状态显示为**在线**。
    -   选择**监控运维** \> **日志服务**，可查看**云端运行日志**和**设备本地日志**日志。详情请参见[云端运行日志](/cn.zh-CN/监控运维/日志服务/云端运行日志.md)、[设备本地日志](/cn.zh-CN/监控运维/日志服务/设备本地日志.md)。

## 错误码

如果设备通过MQTT协议接入物联网平台失败，请根据错误码排查问题。服务端错误码说明，请参见[错误排查](/cn.zh-CN/最佳实践/设备接入/使用Paho接入物联网平台/错误排查.md)。


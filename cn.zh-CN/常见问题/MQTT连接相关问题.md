# MQTT连接相关问题

本文介绍MQTT连接可能出现的问题和解决方法。

## 云端接入域名和端口号是什么？

接入域名：

-   企业版实例的接入域名，请在物联网平台控制台**实例概览**页面，单击实例，进入实例详情页查看。
-   公共实例的接入域名：`${YourProductKey}.iot-as-mqtt.${YourRegionId}.aliyuncs.com`。 其中：
    -   $\{YourProductKey\}：请替换为设备所属产品的的ProductKey。可从物联网平台控制台设备详情页获取。
    -   $\{YourRegionId\}：请参见[地域和可用区]()，替换为您的Region ID。

端口号：1883。

## 使用MQTT协议连接，不同的设备可以使用相同的clientID连接服务器吗？

clientID需为全局唯一。如果不同的设备使用相同的clientID同时连接物联网平台，那么先连接的那个设备会被强制断开。

## MQTT协议版本是多少？

在MQTT connect packet中设置MQTT的版本。目前SDK（V2.02）使用MQTT 3.1.1。

可以修改SDK代码中`src\mqtt\mqtt_client.h IOTX_MC_MQTT_VERSION`的值，来修改支持的版本，3表示3.1版，4表示3.1.1版。

## MQTT进行设备认证时，server返回“400”错误

认证返回400错误，表示鉴权认证失败。请检查设备证书信息ProductKey、DeviceName和DeviceSecret是否正确。

## C语言SDK中MQTT是否支持iOS接入？

C语言SDK可以移植到任何能够支持C语言的系统上。如果是iOS系统建议寻找开源的Object-C实现。

## 目前mqtt-example设备上线后会立刻下线，请问如何修改mqtt-example让设备一直处于上线状态？

mqtt-example程序发送一次消息后会自动退出，可以尝试以下任意一种方式实现长期在线。

-   执行mqtt-example时，使用命令行`./mqtt-example loop`，设备会保持长期在线。
-   修改demo代码。mqtt-example的代码在最后会调用IOT\_MQTT\_Destroy，设备最后会变成离线状态，所以可以修改代码，去掉IOT\_MQTT\_Unregister 和IOT\_MQTT\_Destroy。

    ```
    while(1)      
    {       
        IOT_MQTT_Yield(pclient, 200);   
        HAL_SleepMs(100);  
    }
    ```


## 心跳的时间间隔如何设置？

在IOT\_MQTT\_Construct里面可以设置keepalive\_interval\_ms的取值。物联网平台使用这个值来作为心跳间隔时间。keepalive\_interval\_ms的取值范围是60000~300000。

## 设备端的重连机制是什么？

设备端会在keepalive\_interval\_ms时间间隔发送ping request，然后等待ping response。

如果设备端在keepalive\_interval\_ms时间内无法收到ping response，或是在进行send以及recv时发生错误，平台就认为此时网络断开，而需要进行重连。

重连机制是平台内部触发，无需使用者接入。重连时，会重新进行认证。如果认证成功就会开始再次进行MQTT connect。重连会一直持续直到再次连接成功。

## 云端如何侦测到设备离线？

云端会根据MQTT CONNECT packet里面keepalive的设置，等待ping request。如果在指定时间内没有收到ping request，则认为设备离线。

云端可以接受的最大时延是5秒。

## 设备端SDK是否支持MQTT和CCP协议的断线重连？

支持。测试场景描述：开发板通过Wi-Fi连接上路由器后，把网线拔掉，MQTT和CCP协议都会自动尝试和server重新建立连接。尝试时间间隔是1s、2s、4s、8s、…，最大间隔时间默认是60s，也就是说断网后超过60s时间仍未连接成功，之后会每隔60s尝试和server重连。您可以设置最大间隔时间。

## 发布QoS1数据时，偶尔会出现MQTT\_PUSH\_TO\_LIST\_ERROR\(-42\)，如何解决？

需要等待ACK的packet都会存放起来，等待ACK。存放量有上限，当需要等待的packet太多到达上限时，就会触发`MQTT_PUSH_TO_LIST_ERROR(-42) error`。

出现错误可能是因为当前网络状态不好，或者是发送的频率过高。如果排除上述两个问题，当前的发送的频率是预期的，那么可以适当的调整IOTX\_MC\_REPUB\_NUM\_MAX、IOTX\_MC\_SUB\_REQUEST\_NUM\_MAX和IOTX\_MC\_SUB\_NUM\_MAX的大小。

如果业务允许，也可以把发布的QoS调整成0。

## IOT\_MQTT\_Yield的作用是什么？

IOT\_MQTT\_Yield的作用是尝试接收数据。因此在需要接收数据时，例如订阅和取消订阅之后，发布QoS1消息之后，或是希望收到发布的数据时，都需要主动调用该函数。

## IOT\_MQTT\_Yield参数timeout的意义是什么？

IOT\_MQTT\_Yield会尝试接收数据，直到timeout时间到后才会退出。

## IOT\_MQTT\_Yield与HAL\_SleepMs的区别

IOT\_MQTT\_Yield与HAL\_SleepMs都是阻塞一段时间，但是IOT\_MQTT\_Yield实质是去读取数据，而HAL\_SleepMs则是系统什么也不做，等待timeout。

## 如何循环接收消息？

需要循环调用IOT\_MQTT\_Yield，函数内自动维持心跳和接收数据。

## 订阅了多个Topic，调用一次IOT\_MQTT\_Yield，能接收到多个Topic的消息吗？

首先需要确定Topic的权限，是不是同时满足发布和订阅。如果是，调用一次IOT\_MQTT\_Yield，可以接收到多个packet。

## MQTT连接方式，只能通过不停地调用IOT\_MQTT\_Yield来轮询获取数据吗？

如果使用的TCP/IP协议栈，可以实现TCP主动通知上层有数据到达，可以改动实现事件触发的方式来触发IOT\_MQTT\_Yield。但是改动比较大，所以还请自行评估是否需要修改。

修改流程是：

调整utils\_net.c里面socket的API，变成可以由TCP数据到达时回调的API。

当TCP主动通知上层有数据到达时，通知到MQTT服务器。让MQTT服务器内部执行IOT\_MQTT\_Yield，这样就可以不需要外部调用IOT\_MQTT\_Yield来读取数据。

如果TCP无法做到主动上报数据，但OS支持多线程，也可以在MQTT-example里面再起一个thread，在这个thread里面以下代码用于接收数据。收到数据时，触发主线程进行数据处理，而主线程大部分时间可以用于处理其他逻辑。

```
while(1)
 {      
    IOT_MQTT_Yiled(pclient, 200);    
    HAL_SleepMs(200);   
 }
```

如果使用的系统也不支持多线程，就只能把IOT\_MQTT\_Yield的timeout时间间隔减小，然后提高调用的频率，在每次调用的时间间隔内执行其他操作，从而做到尽量减少对其他操作的阻塞。

## 什么情况下会发生订阅超时（subscribe timeout）？

在2倍request\_timeout\_ms时间内，系统未接收到SUBACK packet时，会触发订阅超时，并通过event\_handle函数发送超时通知。

请在订阅之后，立刻执行IOT\_MQTT\_Yield尝试读取SUBACK，请勿使用HAL\_SleepMs。

## 订阅时，返回IOTX\_MQTT\_EVENT\_SUBCRIBE\_NACK

请检查Topic的操作权限是否为订阅。

如果发布报错“no authorization”，请确认是否为发布权限。

## MQTT发布的消息体大小限制

MQTT的协议包受限于IOT\_MQTT\_Construct里参数的write\_buf和read\_buf的大小。

MQTT协议包大小不能超过256 KB。超过大小限制的消息会被丢弃。

## MQTT协议pub消息payload格式是怎么样的？

物联网平台没有制定pub消息payload的具体字段有那些。您根据应用场景制定自己的协议，然后以JSON格式放到pub消息载体里面传给服务端。

## ota\_mqtt升级的时候报错“mqtt read buffer is too short”

MQTT设置的buffer过小，即mqtt\_param的pread\_buf和pwrite\_buf申请过小造成的。可以根据实际需要修改OTA\_MQTT\_MSGLEN的大小。

## 是否可以使用MQTT直连的方式进行OTA升级？

OTA升级时，必须使用HTTPS进行固件下载。MQTT只接收版本更新指令，与MQTT的连接方式无关。阿里云不支持HTTP下载固件，因此如果设备没有SSL通信的能力，则不能使用OTA服务。

## 打开MQTT over TLS，运行时提示MQTT创建失败，返回错误码0x2700

如果关闭MQTT over TLS则可以成功地订阅和发布信息；打开MQTT over TLS时，建连失败。首先确认mbedtls是否做了修改，这是用于传输层和应用层之间加密的功能，不能随意更改。mbedtls没有修改，则考虑系统时间是否正确，系统时间不对也会导致证书校验失败。

## 进行MQTT连接的时候，是否需要root.crt证书验证？

若使用TLS进行MQTT接入，需要下载根证书。

若使用物联网平台提供的demo进行开发，无需再下载根证书，demo中已自带证书。

## 物联网平台支持哪些QoS Level？

在MQTT协议、CCP协议下，阿里云物联网平台均支持QoS 0和QoS 1，但不支持QoS 2。


# Link SDK运行相关问题

本文介绍使用Link SDK过程中可能遇到的常见问题和解决方法。

## Link SDK支持什么环境？

Link SDK是跨平台的，用户可以自行移植到目标平台上运行，开发环境推荐Ubuntu16.04。

## Link SDK占用多少RAM？

MQTT协议数据传输通过mbedTLS，Link SDK消耗35 K（RAM）= 8 K（stack）+ 27 K（heap）。

CCP协议下，Link SDK消耗45 K（RAM） = 32 K（stack）+ 13 K（heap）。可以通过修改下面的两个宏减小stack的占用：

-   `#define TOPIC_MAX_NUM 64`：Topic数量最大限制。如果设备订阅的Topic数量较小，可以修改为更小的值，如16。
-   `#define TOPIC_MAX_LEN 128` ：Topic长度最大限制。如果设备订阅的Topic名称长度较小，可以修改为更小的值，如32。

## Link SDK的运行需要哪些条件？

运行Link SDK的主要条件是：支持TCP/IP协议栈。

## 是否支持FreeRTOS 操作系统移植？

支持FreeRTOS 操作系统连接阿里云物联网平台，例如乐鑫的Wi-Fi模组使用的就是FreeRTOS。请参见乐鑫提供的开源代码：[FreeRTOS的移植参考代码](https://github.com/espressif/esp8266-aliyun)。

## 如何ECS上使用FreeRTOS 系统？

可以通过导入镜像实现。

导入镜像的方法，请参见[导入镜像实践视频](https://help.aliyun.com/video_detail/54743.html)。

导入镜像注意事项，请参见[导入镜像必读](/cn.zh-CN/镜像/自定义镜像/导入镜像/导入镜像必读.md)。

## 是否支持KEIL？

目前Link SDK不支持直接在Keil环境下开发，但是可以在SDK功能配置后，将抽取的代码添加到已有的Keil工程或者通过交叉编译生成目标库供Keil下的工程调用。

## 如何打开 SDK 日志？

在需要打开日志的地方，调用函数查看日志。具体函数说明如下。

-   IOT\_OpenLog：开始打印日志信息。可使用一个`const char *`作为入参，表示模块名称。
-   IOT\_SetLogLeve：设置打印的日志等级。入参从1到5。数字越大，日志越详细。
-   IOT\_CloseLog：停止打印日志信息。入参为空。
-   IOT\_DumpMemoryStats：打印内存的使用统计情况。入参从1到5。数字越大，日志越详细。

## 是否支持多线程？

目前`IOT_*()`的API都是进程级别，仅支持单进程单线程使用，不支持在同一进程的不同线程并发重入。

## 数据传输的安全性怎么保证？

设备和服务端之间的链路可以通过TLS加密，并且使用设备身份证书信息（productKey、deviceName、deviceSecret）进行认证，任何一个错误都会导致认证失败。

## 一个设备证书可用于多个设备接入吗？

不可以，一个设备证书只能用于一个设备连接。

## 报错“err log：\[error\]rate limiter”，请问是什么原因？

设备被限流，单个设备数据上报上限：QoS0为30条/秒，QoS1为10条/秒。限流后，设备上报的数据就会被丢掉。

## 如果订阅同一个广播Topic的设备数量超过1,000，怎么办？

广播Topic最多支持1,000个订阅者。如果设备数量超过1,000，可以对设备进行分组，每组设备数量等于或小于1,000。例如，有5000个设备，需分为5组，调用5次广播接口广播消息。

## 能不能订阅其他设备Topic？

设备只能订阅和发布自己的Topic。如果两个设备之间需要通信，有两种方式：

[基于规则引擎的M2M设备间通信](/cn.zh-CN/最佳实践/消息通信/M2M设备间通信/基于规则引擎的M2M设备间通信.md)

[基于Topic消息路由的M2M设备间通信](/cn.zh-CN/最佳实践/消息通信/M2M设备间通信/基于Topic消息路由的M2M设备间通信.md)

## 广播消息Topic如何填写？

广播Topic格式：`/broadcast/productKey/xxxx`。

## 广播是否只能针对在线的设备？

广播Topic 默认是QoS=0，且不允许用户设置，因此广播消息只有当前在线设备才能接收到。


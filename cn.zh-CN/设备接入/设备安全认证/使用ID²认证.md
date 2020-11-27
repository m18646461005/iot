---
keyword: [物联网, IoT, 物联网平台, 设备, 连接认证, 安全认证, 设备激活, ID²]
---

# 使用ID²认证

阿里云提供IoT设备身份认证ID²（Internet Device ID）。ID²是一种物联网设备的可信身份标识，具备不可篡改、不可伪造、全球唯一的安全属性。

ID²设备身份认证服务提供设备与云端的双向身份认证和链路加密功能。

使用ID²认证的设备，有两种注册方式：

-   只需在控制台创建产品，无需创建设备。设备使用ID²认证通过后，物联网平台会根据设备端上报的设备名称，自动注册设备。
-   在控制台创建产品后，开启ID²白名单校验，然后注册设备。未注册的设备接入物联网平台时不能通过认证。

**说明：**

-   目前仅华东2（上海）地域支持ID²证书认证。
-   对于企业版实例，请确保已启用ID²设备身份认证。若购买实例时未启用，可通过为实例升配启用该功能。
-   设备身份认证方式设置后，不可更改。

1.  登录[物联网平台控制台](http://iot.console.aliyun.com/)。

2.  在实例概览页，找到对应的实例，单击实例进入实例详情页。

    ![实例概览](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8727475061/p174584.png)

3.  在**设备管理** \> **产品**，创建认证方式为**ID²**的产品。具体操作，请参见[创建产品](/cn.zh-CN/设备接入/创建产品.md)。

    ![创建产品](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5545559951/p135041.png)

    在物联网平台控制台创建ID²产品后，产品会自动列入IoT设备身份认证控制台的产品列表。

4.  登录IoT设备身份认证控制台。

    -   对于企业版实例，登录[物联网平台控制台](http://iot.console.aliyun.com/)，找到对应的实例，单击实例进入实例详情页，在**公网终端节点区**域选择**管理ID²**，复制ID²控制台地址，粘贴到浏览器地址栏并按回车键，进入实例对应的ID²设备身份认证控制台。
    -   对于公共实例，单击进入[IoT设备身份认证控制台](https://iotid.console.aliyun.com/productmanage)。
5.  在左侧导航栏，选择**使用管理** \> **产品管理**，查看创建的ID²产品，如下图所示。

    ![ID²产品列表](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5545559951/p135069.png)

6.  为产品分配ID²授权。

    **说明：**

    -   购买的ID²授权仅能用于指定产品下的设备。
    -   每一个设备至少使用一个ID²授权。购买之后，您还可以根据业务需要，随时为该产品购买更多ID²授权。
    -   对于企业版实例，单击上图中的**分配ID²**，将ID²授权，即启用ID²设备身份认证时购买的ID² License，分配给产品。
    -   对于公共实例，单击上图中的**购买授权**，购买ID²授权并分配给产品。

        购买成功后，可在IoT设备身份认证控制台的产品列表中，单击产品对应的**查看**，进入产品详情页查看ID²授权信息。

7.  （可选）开启ID²白名单校验，注册设备。开启后，未注册的设备接入物联网平台时不能通过认证。

    1.  登录[物联网平台控制台](http://iot.console.aliyun.com/)进入对应实例。

    2.  在左侧导航栏选择**设备管理** \> **产品**，单击ID²产品对应的**查看**。

    3.  在产品详情页，开启**ID²白名单校验**开关。系统将进行短信验证，以确认是您本人操作。

    4.  在**设备管理** \> **设备**，在ID²产品下创建设备，详细操作请参见[单个创建设备](/cn.zh-CN/设备接入/创建设备/单个创建设备.md)、[批量创建设备](/cn.zh-CN/设备接入/创建设备/批量创建设备.md)。

8.  烧录ID²到设备端。

    -   向设备端SDK集成ID² Client SDK。

        阿里云提供ID² Client SDK，用于设备端身份认证开发。请访问[ID² Client SDK](https://github.com/alibaba/id2_client_sdk)，获取SDK和查看编译说明。

    -   配置设备端调用ID²认证接口。Client SDK中已封装了对ID²载体和接口的操作。设备上线时，需调用ID² Client SDK的认证接口激活ID²。具体接口说明，请参见[认证接口](https://help.aliyun.com/document_detail/103157.html)。
    阿里云IoT设备身份认证服务提供芯片、模组和设备级别的合作方案，详情请参见[IoT设备身份认证文档](https://help.aliyun.com/product/100846.html)。

9.  设备接入物联网平台。

    -   向设备端SDK传入设备信息。

        ![iot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5545559951/p65535.png)

        -   将PRODUCT\_KEY和PRODUCT\_SECRET替换为您的产品对应的信息。
        -   设备名称DEVICE\_NAME：
            -   未开启ID²白名单校验时，传入自定义设备名称，需保证设备名称在产品下唯一。
            -   开启ID²白名单校验后，传入的设备名称需已在物联网平台注册。
        -   使用ID²认证的设备不再使用DeviceSecret进行认证，所以DEVICE\_SECRET可传入任意值，系统不会做校验。
    -   MQTT连接参数：
        -   接入域名：
            -   对于企业版实例，请登录[物联网平台控制台](http://iot.console.aliyun.com/)，找到对应的实例，单击实例进入实例详情页，在**公网终端节点区**域选择**管理ID²**，查看ID²认证地址，即为接入域名。
            -   对于公共实例，接入域名为`${YourProductKey}.itls.cn-shanghai.aliyuncs.com`。请将$\{YourProductKey\}替换为您的产品对应的信息。
        -   端口：1883。
        -   mqttClientId：`clientId+"|securemode=8,signmethod=hmacsha1,timestamp=2524608000000,authtype=id2,instanceId=xxxxx|"`。

            instanceId为实例ID，仅在使用企业版实例时传入，请登录[物联网平台控制台](http://iot.console.aliyun.com/)，在实例概览页面查看。


设备通过ID²认证通过后，成功接入物联网平台。物联网平台自动注册该设备，您可以在**设备管理** \> **设备**查看该设备。


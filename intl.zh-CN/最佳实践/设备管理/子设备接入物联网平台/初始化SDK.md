---
keyword: [物联网, IoT, 阿里云物联网平台, 子设备, 网关, 通信]
---

# 初始化SDK

本示例中，提供云端和设备端 Java SDK Demo。您需准备Java开发环境，下载SDK Demo，导入项目和初始化SDK。

[创建网关和子设备](/intl.zh-CN/最佳实践/设备管理/子设备接入物联网平台/创建网关和子设备.md)

1.  单击下载[iotx-api-demo](https://iot-demos.oss-cn-shanghai.aliyuncs.com/topo/iotx-api-demo.zip)，并解压缩。

    SDK Demo中包含了服务端SDK Demo和设备端SDK Demo。

2.  打开Java开发工具，导入解压缩后的iotx-api-demo文件夹。

3.  在java目录下的pom文件中，添加以下依赖，导入阿里云云端SDK和设备端SDK。

    ```
    <!-- https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-iot -->
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

4.  在java/src/main/resources/目录下的config文件中，填入初始化信息。

    ```
    user.accessKeyID = <your accessKey ID>
    user.accessKeySecret = <your accessKey Secret>
    iot.regionId = <regionId>
    iot.productCode = Iot
    iot.domain = iot.<regionId>.aliyuncs.com
    iot.version = 2018-01-20
    ```

    |参数|说明|
    |:-|:-|
    |accessKeyID|您的阿里云账号的AccessKey ID。 将光标定位到您的账号头像上，选择**AccessKey管理**，进入安全信息管理页，可创建或查看您的AccessKey。 |
    |accessKeySecret|您的阿里云账号的AccessKey Secret。查看方法同上AccessKey ID。|
    |regionId|您的物联网设备所属地域ID。地域ID的表达方法，请参见[地域和可用区]()。|


[网关接入物联网平台](/intl.zh-CN/最佳实践/设备管理/子设备接入物联网平台/网关接入物联网平台.md)

[子设备接入物联网平台](/intl.zh-CN/最佳实践/设备管理/子设备接入物联网平台/子设备接入物联网平台.md)


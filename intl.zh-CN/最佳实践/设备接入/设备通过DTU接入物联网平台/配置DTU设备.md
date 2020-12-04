---
keyword: [IoT, 物联网平台, 串口传输协议, DTU设备]
---

# 配置DTU设备

本文介绍使用DTU配置工具，配置DTU串口和设备证书信息（ProductKey、DeviceName和DeviceSecret），实现DTU代理设备接入物联网平台。

本示例使用F2x16 DTU设备，并使用电脑模拟DTU设备端进行开发配置。通过USB转串口将电脑与DTU设备连接。

**说明：** 请确保DTU可以正确连接Internet。

1.  连接DTU设备与电脑USB接口。

    ![连接DTU设备](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4431649951/p71154.png)

2.  在电脑上，打开DTU配置工具。本示例使用F2x16配置工具。

3.  配置正确的串口号，设置波特率，并打开串口。

    ![配置串口](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4431649951/p71155.png)

4.  登录配置（如图①），使DTU进入配置状后，单击**读取配置**（如图②），获取现有DTU的配置。

    ![获取DTU配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4431649951/p71156.png)

5.  在右侧**配置界面**下，单击**串口**，再进行本地串口配置。

    **说明：** 确保工作协议为**port**。

    配置信息如下图。

    ![配置信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4431649951/p71157.png)

6.  单击**IoT接入配置**，填入从物联网平台获取的设备证书信息和地域。

    ![配置接入信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6993707061/p71158.png)

7.  单击下方**下发配置**，使配置生效。

    如果配置下发失败，请单击退出登录的按钮![退出](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6993707061/p188432.png)，然后重新配置。

8.  完成配置后，请单击退出登录的按钮![退出](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6993707061/p188432.png)，才能使DTU进入正常工作模式。

9.  将DTU断电，再重新上电。DTU上online灯亮，即表示已连接上物联网平台。

    您还可以在物联网平台控制台上，查看设备的状态。

    ![查看状态](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5431649951/p71159.png)


[测试数据通信](/intl.zh-CN/最佳实践/设备接入/设备通过DTU接入物联网平台/测试数据通信.md)


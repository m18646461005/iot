---
keyword: [IoT, IoT, ioT Platform, access IoT devices, device SDKs, Link Kit, C language, ProductKey, DeviceName, DeviceSecret]
---

# Connect a device to IoT Platform

Alibaba Cloud IoT Platform provides device SDKs that you can use to connect devices to IoT Platform. This topic uses the sample program `linkkit-example-solo` to demonstrate how to connect a device to IoT Platform.

-   The following example uses a C SDK 3.0.1. We recommend that you use the SDK in a 64-bit Ubuntu 16.04 system.
-   The following software is required:

    make-4.1, git-2.7.4, gcc-5.4.0, gcov-5.4.0, lcov-1.12, bash-4.3.48, tar-1.28, and mingw-5.3.1.

    You can run the following command to install the software:

    `sudo apt-get install -y build-essential make git gcc`


1.  Log on to your Linux VM instance.

2.  Download the [Link Kit SDK](https://code.aliyun.com/linkkit/c-sdk/repository/archive.zip?ref=v3.0.1).

3.  Use the unzip command to extract files from the package.

4.  Before you call HAL to send device identity information to the SDK, you need to change the device certificate information in wrappers/os/ubuntu/HAL\_OS\_linux.c to the certificate information of the device added in [Create products and devices](/intl.en-US/Quick Start/Use IoT Platform/Create products and devices.md). Make sure to save your changes.

    Enter the ProductKey, DeviceName, and DeviceSecret as follows. Device certificate information is used for identity authentication when the device connects to IoT Platform.

    **Note:** In the quick start guide, the [Unique-certificate-per-device authentication](/intl.en-US/Device Access/Authenticate devices /Unique-certificate-per-device authentication.md) method is used and ProductSecret is optional.

    ```
    #ifdef DEVICE_MODEL_ENABLED
        char _product_key[IOTX_PRODUCT_KEY_LEN + 1]       = "a1zlu******";
        char _product_secret[IOTX_PRODUCT_SECRET_LEN + 1] = "";
        char _device_name[IOTX_DEVICE_NAME_LEN + 1]       = "device1";
        char _device_secret[IOTX_DEVICE_SECRET_LEN + 1]   = "ynNuxxxxxxxxxx7RMUJD9WZhEvd7****";
    ```

5.  If your product is not created in the public instance in the China \(Shanghai\) region, find the following position in src/dev\_model/examples/linkkit\_example\_solo.c.

    ```
        /* post reply doesn't need */
        post_reply_need = 1;
        IOT_Ioctl(IOTX_IOCTL_RECV_EVENT_REPLY, (void *)&post_reply_need);
    
        /* Create Master Device Resources */
        g_user_example_ctx.master_devid = IOT_Linkkit_Open(IOTX_LINKKIT_DEV_TYPE_MASTER, &master_meta_info);
        if (g_user_example_ctx.master_devid < 0) {
            EXAMPLE_TRACE("IOT_Linkkit_Open Failed\n");
            return -1;
        }
    ```

    Add your MQTT endpoint information as follows in that position . Make sure to save your changes.

    ```
        /* post reply doesn't need */
        post_reply_need = 1;
        IOT_Ioctl(IOTX_IOCTL_RECV_EVENT_REPLY, (void *)&post_reply_need);
    
        // Enter the MQTT endpoint of your instance. In the left-side navigation pane of the IoT Platform console, click Instances. On the page that appears, click View in the Actions column of the instance. On the Instance Details page, you can view the endpoint.
        char custom_domain[] = "${YourEndpoint}"; 
        IOT_Ioctl(IOTX_IOCTL_SET_MQTT_DOMAIN, (void *)custom_domain);
    
        /* Create Master Device Resources */
        g_user_example_ctx.master_devid = IOT_Linkkit_Open(IOTX_LINKKIT_DEV_TYPE_MASTER, &master_meta_info);
        if (g_user_example_ctx.master_devid < 0) {
            EXAMPLE_TRACE("IOT_Linkkit_Open Failed\n");
            return -1;
        }
    ```

6.  In the root directory, use the make command to compile the sample program.

    ```
    $ make distclean
    $ make
    ```

    The sample program `linkkit-example-solo` is saved under the directory ./output/release/bin.

7.  Run the sample program.

    ```
    ./output/release/bin/linkkit-example-solo
    ```

    In the IoT Platform console, the device status is **online**, the device is connected to IoT Platform.

    After the device is connected to IoT Platform, it automatically reports messages to IoT Platform. You can check log files for message details.


[Device messages subscribed by the server](/intl.en-US/Quick Start/Use IoT Platform/Subscribe to device messages from IoT Platform.md)


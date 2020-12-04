---
keyword: [MQTT, Internet of Things, communication protocol, IoT, IoT Platform, X.509]
---

# Use X.509 certificates to authenticate devices

An X.509 certificate is a digital certificate that is used to authenticate a communication entity. IoT Platform allows you to use X.509 certificates to authenticate devices that are directly connected to IoT Platform based on the MQTT protocol.

## Limits

-   X.509 certificates are only applicable to devices that are directly connected to IoT Platform based on the MQTT protocol.
-   X.509 certificates are supported only in the China \(Shanghai\) region.
-   X.509 certificates are not applicable to products that use LoRaWAN as the network connection mode.
-   After you specify an authentication mode for a device, you cannot modify the mode.

## Generate an X.509 certificate

The X.509 certificate of a device is issued by IoT Platform.

1.  Log on to the [IoT Platform console](http://iot.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Devices** \> **Products**. On the page that appears, create a product and set the Authentication Mode parameter to **X.509 Certificate**. For more information, see [Create a product](/intl.en-US/Device Access/Create a product.md).

    ![iot x509](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0248707061/p112906.png)

3.  In the left-side navigation pane, choose **Devices** \> **Devices**. On the page that appears, create a device in the product. For more information, see [Create a device](/intl.en-US/Device Access/Create devices/Create a device.md) and [Create multiple devices at a time](/intl.en-US/Device Access/Create devices/Create multiple devices at a time.md).

    When IoT Platform creates a device, IoT Platform issues an X.509 certificate and private key to the device.

    **Note:** If you use an X.509 certificate to authenticate a device, you must burn the X.509 certificate to the device. If a sub-device uses unique-certificate-per-product authentication, or the sub-device is connected to IoT Platform by using a gateway, you must burn the ProductSecret or DeviceSecret to the sub-device.

4.  Download the X.509 certificate and private key of the device.

    -   Download the X.509 certificates and private keys of multiple devices.
        1.  In the left-side navigation pane, choose **Devices** \> **Devices** \> **Batch Management**. On the page that appears, find the product to which the devices belong, and click **DownloadCSV** in the Actions column.
        2.  Download the X.509 certificates and private keys by using the CertUrl address in the Excel file.

            **Note:** The CertUrl address is valid for 30 days. We recommend that you download the X.509 certificates within 30 days after you create the devices.

    -   Download the X.509 certificate and private key of a single device. You can use one of the following methods:
        -   In the left-side navigation pane, choose **Devices** \> **Devices**. On the page that appears, find the device and click **View** in the Actions column. The Device Details page appears. Click **Download** next to the **X.509 certificate** information.

## Configure device authentication

Only device Link SDK for C supports X.509 certificate authentication. You can visit [SDK for C](https://help.aliyun.com/document_detail/96623.html) to download the SDK and code demo.

A device that uses X.509 certificate authentication can be connected to IoT Platform by using the following domain name and port:

-   Domain name: x509.itls.cn-shanghai.aliyuncs.com
-   Port: 1883

The following procedure shows how to configure device authentication. Device Link SDK for C is used in the examples.

1.  Download the [root certificate](http://aliyun-iot.oss-cn-hangzhou.aliyuncs.com/cert_pub/root.crt) to verify the server certificate during mutual authentication.

2.  Establish an MQTT connection for device authentication.

    If you use Link SDK demo for C, configure the connection in the mqtt\_example.c file under the \\src\\mqtt\\examples directory.

    -   Set the device certificate information \(ProductKey, DeviceName, and DeviceSecret\) to empty strings.

        If you use an X.509 certificate to authenticate a device, you do not need to specify the device certificate information \(ProductKey, DeviceName, and DeviceSecret\) when you establish the MQTT connection. After the device is connected to IoT Platform, IoT Platform issues a certificate to the device. The certificate includes the ProductKey and DeviceName.

        Example:

        ```
        char g_product_key[IOTX_PRODUCT_KEY_LEN + 1]       = "";
        char g_device_name[IOTX_DEVICE_NAME_LEN + 1]       = "";
        char g_device_secret[IOTX_DEVICE_SECRET_LEN + 1]   = "";
        ```

    -   Register the ITE\_IDENTITY\_RESPONSE event to receive the ProductKey and DeviceName from IoT Platform after the MQTT connection is established.

        Example:

        ```
        int identity_response_handle(const char *payload)
        {
            EXAMPLE_TRACE("identify: %s", payload);
        
            return 0;
        }
        
        IOT_RegisterCallback(ITE_IDENTITY_RESPONSE, identity_response_handle);
        ```

        **Note:** You can also configure the device to ensure that the received ProductKey and DeviceName are persisted on the device. Otherwise, the device obtains a ProductKey and a DeviceName each time it is connected to IoT Platform.

3.  Configure the X.509 certificate and private key to authenticate the connection.

    If you use Link SDK demo for C, replace the following information in the HAL\_TLS\_mbedtls.c file under the \\wrappers\\tls directory.

    -   Replace the value of the g\_cli\_crt parameter with the X.509 certificate of your device.
    -   Replace the value of the g\_cli\_key parameter with the private key of the X.509 certificate.
    Example:

    ```
    const char *g_cli_crt = \
    {
        \
        "-----BEGIN CERTIFICATE-----\r\n"
        "Your X.509 certificate"
        "-----END CERTIFICATE-----\r\n"
    };
    
    const char *g_cli_key = \
    {
        \
        "-----BEGIN RSA PRIVATE KEY-----\r\n"
        "Your X.509 PrivateKey"
        "-----END RSA PRIVATE KEY-----\r\n"
    };
    ```


**Note:** If you develop your own device SDK instead of using the device Link SDK provided by Alibaba Cloud, you must perform the following operations:

-   Store the X.509 certificate of the device and the private key of the certificate in the security library.
-   Set the device certificate information \(ProductKey, DeviceName, and DeviceSecret\) to empty strings. IoT Platform issues a ProductKey and DeviceName after the device passes the authentication.

    The device obtains the ProductKey and DeviceName from the `/ext/auth/identity/response` topic. You do not need to subscribe to the topic.

    The message payload is in the following format:

    ```
    {
        "productKey":"***",
        "deviceName":"***"
    }
    ```


## Re-establish a connection between the device and IoT Platform

After the device passes authentication, the device receives the ProductKey and DeviceName. If the ProductKey and DeviceName are persisted on the device, the device sends a CONNECT message to IoT Platform when the device re-establishes an MQTT connection with IoT Platform. The following table describes the parameters in the CONNECT message.

|Endpoint|`x509.itls.cn-shanghai.aliyuncs.com:1883`|
|Variable header: Keep Alive|The CONNECT message must include a keep-alive period. You must set the keep-alive period to a value between 30 seconds to 1,200 seconds. Otherwise, IoT Platform rejects the connection. We recommend that you set the keep-alive period to a value that is greater than 300 seconds. If the network connection is unstable, we recommend that you set the keep-alive period to a higher value.|
|Parameters in an MQTT CONNECT message|```
mqttClientId: clientId+"|securemode=2,signmethod=hmacsha1,timestamp=132323232|"
mqttUsername: deviceName+"&"+productKey
mqttPassword: ""
```

The mqttClientId includes the following parameters. The content included in `||` are extended parameters.

-   clientId: the ID of the client. We recommend that you use the MAC address or serial number \(SN\) of the device as the client ID. The client ID cannot exceed 64 characters in length.
-   timestamp: the timestamp of the current time. Unit: milliseconds. This parameter is optional.
-   signmethod: the signature algorithm. Valid values: hmacmd5, hmacsha1, and hmacsha256.
-   securemode: the secure mode. Set the value to 2 because the TLS direct connection mode is used.

**Note:** If you use an X.509 certificate to authenticate a device, IoT Platform no longer verifies the signature value. Therefore, you can set the mqttpassword parameter to an empty string. |


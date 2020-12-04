---
keyword: [Internet of Things, IoT, IoT Platform, MQTT, unique-certificate-per-product, dynamic registration, ClientID, DeviceToken, DeviceSecret]
---

# MQTT-based dynamic registration

If a device is directly connected to IoT Platform, you can dynamically register the device by using the MQTT protocol. That is, you can use the unique-certificate-per-product authentication method to connect the device to IoT Platform. The device establishes a connection with IoT Platform based on Transport Layer Security \(TLS\) to obtain the information that is required for the TCP connection. Then, the device ends the connection and establishes a TCP connection for communication. This article describes the dynamic registration process.

The following steps in [Unique-certificate-per-product authentication](/intl.en-US/Device Access/Authenticate devices /Unique-certificate-per-product authentication.md) are performed:

1.  Create a product.
2.  Enable dynamic registration.
3.  Add a device.
4.  Burn the device SDK on the production line.

## Dynamic registration process

![Process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1054788951/p146803.png)

1.  The device sends a CONNECT message that includes dynamic registration parameters to establish a connection.

    **Note:** Dynamic registration supports only TLS-based connections. It does not support direct TCP connections. During dynamic registration, IoT Platform does not verify the keep-alive time of the MQTT connection. Therefore, you do not need to set the keep-alive time.

    -   MQTT endpoint:
        -   To view the endpoints of your purchased instance, perform the following steps: Log on to the IoT Platform console. In the left-side navigation pane, click Instances. On the Instances page, find the instance and click **View** in the Actions column. On the Instance Details page, you can view the endpoints.
        -   The endpoint for the public instances is `${YourProductKey}.iot-as-mqtt. ${YourRegionId}.aliyuncs.com:1883`.
            -   $\{YourProductKey\}: Replace this variable with the key of the product to which the device belongs. You can obtain the product key on the Device Details page of the IoT Platform console.
            -   $\{YourRegionId\}: Replace this variable with the region ID of your product. For more information, see[Regions and zones](https://www.alibabacloud.com/help/doc-detail/40654.htm).
    -   Dynamic registration parameters of the CONNECT message:

        -   If the device belongs to a purchased instance and uses the preregistration-free [Unique-certificate-per-product authentication](/intl.en-US/Device Access/Authenticate devices /Unique-certificate-per-product authentication.md) method, the dynamic registration parameters in the following example are used:

            ```
            mqttClientId: clientId+"|securemode=2,authType=xxxx,random=xxxx,signmethod=xxxx,instanceId=xxxx|"
            mqttUserName: deviceName+"&"+productKey
            mqttPassword: sign_hmac(productSecret,content) 
            ```

        -   If the device belongs to the public instance and uses the pre-registration [Unique-certificate-per-product authentication](/intl.en-US/Device Access/Authenticate devices /Unique-certificate-per-product authentication.md) method, the dynamic registration parameters in the following example are used:

            ```
            mqttClientId: clientId+"|securemode=2,authType=xxxx,random=xxxx,signmethod=xxxx|"
            mqttUserName: deviceName+"&"+productKey
            mqttPassword: sign_hmac(productSecret,content) 
            ```

        Parameters:

        -   mqttClientId

            The following table lists the parameters that are included in the mqttClientId parameter.

            |Parameter|Description|
            |---------|-----------|
            |clientId|The client ID. It must be 1 to 64 characters in length. We recommend that you use the MAC address or serial number \(SN\) of the device as the client ID.|
            |securemode|The mode of security. Dynamic registration supports only TLS-based connections. It does not support direct TCP connections. Therefore, you must set the value to 2.|
            |authType|The authentication method. Different parameters are returned based on the authentication method. Valid values:            -   register: the pre-registration unique-certificate-per-product authentication method. For more information, see [Unique-certificate-per-product authentication](/intl.en-US/Device Access/Authenticate devices /Unique-certificate-per-product authentication.md). If you set the parameter to this value, DeviceSecret is returned.
            -   regnwl: the preregistration-free unique-certificate-per-product authentication method. For more information, see [Unique-certificate-per-product authentication](/intl.en-US/Device Access/Authenticate devices /Unique-certificate-per-product authentication.md). If you set the parameter to this value, DeviceToken and ClientID are returned. |
            |random|The random number. You can specify a random number.|
            |signMethod|The signature algorithm. Valid values: hmacmd5, hmacsha1, and hmacsha256.|
            |instanceId|The instance ID. You can view the instance ID on the Instances page of the IoT Platform console.|

        -   mqttUserName

            Format: `deviceName+"&"+productKey`

            Example: `device1&al123456789`

        -   mqttPassword

            Calculation method: `sign_hmac(productSecret,content)`

            The value of the content parameter is a concatenated string of the parameters and their values that must be submitted to IoT Platform. These parameters include the deviceName, productKey, and random. These parameters are sorted in alphabetical order and concatenated without using concatenation operators. Then, the value of the content parameter is encrypted based on the algorithm that is specified by the signMethod in the mqttClientId parameter. The ProductSecret parameter of the product is used as the secret key of the algorithm.

            Example: `hmac_sha1(h1nQFYPZS0mW****, deviceNamedevice1productKeyal123456789random123)`

2.  IoT Platform returns a CONNECT ACK message.

    If 0 is returned, the connection is established and the dynamic registration is successful.

    If the connection fails, you must locate the cause based on the error code that is returned in the ACK packet.

    The following table lists the response codes that may be returned after the device sends a connection request to IoT Platform.

    |Response code|Message|Description|
    |-------------|-------|-----------|
    |0|CONNECTION\_ACCEPTED|The dynamic registration is successful.|
    |2|IDENTIFIER\_REJECTED|One or more parameters are invalid. This error may occur due to one of the following causes:    -   One or more required parameters are not specified or are in invalid formats.
    -   You have established a direct TCP connection for registration. Dynamic registration supports only TLS-based connections. |
    |3|SERVER\_UNAVAILABLE|An error has occurred in IoT Platform. Try again later.|
    |4|BAD\_USERNAME\_OR\_PASSWORD|Dynamic registration has failed. The device is not authenticated.Check whether the values of the mqttUserName and mqttPassword input parameters are valid. |

3.  After the connection is established, IoT Platform uses the `/ext/register` topic to return different authentication parameters based on the authType parameter specified in the CONNECT message.

    **Note:** The device does not need to subscribe to the topic that is used to push the certificate.

    -   If you set the authType parameter to register, the DeviceSecret is returned.

        The message payload that is pushed by IoT Platform is in the following format:

        ```
        {
          "productKey" : "xxx",
          "deviceName" : "xxx",
          "deviceSecret" : "xxx"
        }
        ```

    -   If you set the authType parameter to regnwl, the client ID and device token are returned.

        The message payload that is pushed by IoT Platform is in the following format:

        ```
        {
          "productKey" : "xxx",
          "deviceName" : "xxx",
          "clientId" : "xxx",
          "deviceToken" : "xxx"
        }
        ```

4.  The device receives and saves the device secret or a combination of the client ID and device token, and ends the current MQTT connection.

    The device can end the current connection by sending a DISCONNECT message or ending the TCP connection.

    If the device does not end the connection, IoT Platform disconnects the device after 15 seconds.

    If you are using the Eclipse Paho MQTT client, use the `MqttConnectOptions.setAutomaticReconnect(false)` function to turn off automatic reconnection. Otherwise, after the registration succeeds and the TCP connection is ended, the dynamic registration request is generated again based on the reconnection function.

5.  The device uses the device secret or a combination of the client ID and device token to re-initiate a request to establish an MQTT connection between the device and IoT Platform for message communication. For more information, see [Establish MQTT connections over TCP](/intl.en-US/Device Access/Protocols for connecting devices/Use MQTT protocol/Establish MQTT connections over TCP.md).



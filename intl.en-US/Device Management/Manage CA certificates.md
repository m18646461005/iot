---
keyword: [IoT, IoT Platform, CA certificate]
---

# Manage CA certificates

IoT Platform allows you to use a digital certificate to authenticate the devices that are connected to IoT Platform. To use a digital certificate, you must apply for a certificate from a certificate authority \(CA\) and register the certificate on IoT Platform. Then, you can issue a device certificate to a device and associate the device certificate with the device. This topic describes how to register a CA certificate and associate the certificate with a device on IoT Platform.

To use a private CA certificate for device authentication, you must create a product and set **Authentication Mode** to **X.509 Certificate** and **Use Private CA Certificate** to **Yes**.

![Create a product](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9907707061/p162333.png)

## Limits

-   Private CA certificates are applicable only to devices that are directly connected to IoT Platform based on the MQTT protocol.
-   Private CA certificates are supported only in the China \(Shanghai\) region.
-   Private CA certificates are not applicable to products that use LoRaWAN as the network connection mode.
-   Private CA certificates support only device certificates that are signed by using the RSA algorithm.
-   Each Alibaba Cloud account can register up to 10 CA certificates.

## Register a CA certificate

1.  Log on to the [IoT Platform console](http://iot.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Devices** \> **CA Certificates**.

3.  On the Manage CA Certificates page, click **Register CA Certificate**.

4.  In the Register CA Certificate dialog box, enter a certificate name, upload a CA certificate and a validation certificate, and then click **OK**.

    |Parameter|Description|
    |---------|-----------|
    |CA Certificate Name|Enter a certificate name. The name must be 4 to 30 characters in length and can contain letters, digits, and underscores \(\_\).|
    |Upload CA Certificate|Upload a CA certificate. Only `.cer`, `.crt`, and `.pem` files are supported. |
    |Upload Validation Certificate|Upload a validation certificate that is created by using the private key of the CA certificate. Only `.cer`, `.crt`, and `.pem` files are supported.

For example, to create a validation certificate by using OpenSSL, perform the following steps:

    1.  Generate the key pair of the validation certificate.

Run the following command to generate the key pair:

        ```
openssl genrsa -out verificationCert.key 2048
        ```

    2.  Create a Certificate Signing Request \(CSR\) file by using the **Registration Code** at the top of the Register CA Certificate dialog box.

Run the following command to create the CSR file:

        ```
openssl req -new -key verificationCert.key -out verificationCert.csr
        ```

Copy the registration code from the Register CA Certificate dialog box and paste the code as the value of the `Common Name` field.

        ```
……
Common Name (e.g. server FQDN or YOUR name) []: c7cdfde6775c4b408b69d7e3c865f21bafe67937dc9a483ebbf7e6997b7b****
……
        ```

    3.  Create a validation certificate by using the CSR file that is signed by the private key of the CA certificate.

Run the following command to create a validation certificate:

        ```
openssl x509 -req -in verificationCert.csr -CA yourCA.cer -CAkey yourPrivateKey.key -CAcreateserial -out verificationCert.crt -days 300 -sha512
        ``` |

    After the certificate is registered, it is displayed in the list of CA certificates on the Manage CA Certificates page.

    Click **View** in the Actions column. On the CA Certificate Details page, you can view the certificate information and associate the device certificate with the device.


## Obtain the serial number \(SN\) of a device certificate

You must issue a device certificate to each device and obtain the SN of each device certificate.

**Note:**

-   Each SN of the device certificate must be unique among the SNs of the device certificates that are issued by the same user.
-   After a device certificate is issued, you must record the SN of the device certificate. The SN is required when you associate the device certificate with the device that is connected to IoT Platform.

The following table describes the format requirements of the device certificate.

|Device certificate|Each device certificate file must meet the following format requirements:

-   File name extension: `.cer`
-   File name format: `[ProductKey]_[DeviceName]_[CA_SN].cer`
-   Content format:

    ```
-----BEGIN CERTIFICATE-----
Certificate content: an ASCII string
-----END CERTIFICATE-----
    ``` |
|Private key of the device certificate|The private key of each device certificate must meet the following format requirements:

-   File name extension: `.key`
-   File name format: `[ProductKey]_[DeviceName]_[CA_SN].key`
-   Content format:

    ```
-----BEGIN RSA PRIVATE KEY-----
Private key content: a binary string
-----END RSA PRIVATE KEY-----
    ``` |

## Associate the SN of the device certificate with the device

After you register a CA certificate, you must associate the SN of the device certificate with the device information on the IoT Platform. The device information includes the ProductKey and DeviceName.

1.  On the Mange CA certificates page, click **View** in the Actions column.

2.  On the CA Certificate Details page, choose **Device Association** \> **Associate Certificate to Devices**.

3.  Click **Download .csv Template**.

4.  Open the downloaded template file, enter the device certificate information, including the ProductKey, DeviceName, and CertSN \(the SN of the device certificate\). Save the file, and click **Click Upload**.

    The SN of the device certificate is a hexadecimal string that you obtain and record after you issue the device certificate. You can also obtain the SN from the SerialNumber field of your device certificate.

    **Note:**

    -   Each file can contain up to 10,000 association records.
    -   All devices that are listed in the file must belong to the same product.
5.  Click **Save**. The file is uploaded.

    IoT Platform parses and verifies the uploaded file. After the file passes the verification, the certificate can be associated with the device.


## Connect a device to IoT Platform

When you develop a device that uses a private CA certificate for device authentication, you do not need to specify the ProductKey or DeviceName of the device. You need to specify only the subject of the CA certificate and the SN of the device certificate. If the device is connected to IoT Platform, IoT Platform authenticates the connection based on the subject of the CA certificate and the SN of the device certificate. If the connection is authenticated, IoT Platform sends a ProductKey and DeviceName to the device. For more information about how to configure a device, see [Configure device authentication](/intl.en-US/Device Access/Authenticate devices /Use X.509 certificates to authenticate devices.md).


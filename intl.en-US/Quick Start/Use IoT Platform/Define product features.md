# Define product features

IoT Platform allows you to define features for products. You can use a TSL model to describe product features, including properties, services, and events. The TSL model makes it easy to manage products and data transmission. After you create a product, you can define a TSL model to describe product features. Devices under this product automatically inherit its features.

1.  In the product list, select the product and click **View**.

2.  On the Product Details page, click **Define Feature**.

3.  In the **Self-Defined Feature** section, click **Add Self-defined Feature**.

4.  As shown below, add a property to define a switch.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0447749951/p46341.png)

5.  As shown below, add a property to define a counter.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0447749951/p46359.png)

6.  As shown below, add a service to support numerical calculations.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1447749951/p46375.png)

    -   Value A is defined as follows:

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1447749951/p46372.png)

    -   Value B is defined as follows:

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1447749951/p46373.png)

    -   The output parameter indicates the calculation result.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1447749951/p46374.png)

7.  As shown below, add an event to define a hardware error.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1447749951/p46415.png)

    -   The output parameter indicates the error code.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1447749951/p46414.png)

8.  Click **View TSL** and choose Full TSL to view the TSL definitions in JSON format.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1447749951/p46464.png)

9.  Release the TSL model.

    1.  On the Edit Draft page, click **Release Online**. The Release model online? dialog box appears.

    2.  Optional. Click **+Add post notes**, and enter a version number and note.

        |Parameter|Description|
        |---------|-----------|
        |Version Number|The version number of the TSL model. You can manage the TSL model based on the version number. The version number must be 1 to 16 characters in length, and can contain letters, digits, and periods \(.\). |
        |Note|The description of the TSL model. The description must be 1 to 100 characters in length, and can contain letters, digits, and special characters.|

    3.  If an online version is available, you must check the differences between the current version and the online version.

        Click **View differences**. In the View Differences dialog box, you can view the differences. If the current version is configured as normal, click **Confirm**. In the Release model online? dialog box, the checkbox is automatically selected.

    4.  Click **OK** to release the TSL model.

        **Note:**

        -   A TSL model is applied to the product only after it is released.
        -   IoT Platform can save the latest 10 versions of a TSL model. Earlier versions are overwritten.

[Connect a device to IoT Platform](/intl.en-US/Quick Start/Use IoT Platform/Establish a connection between a device and IoT Platform.md)


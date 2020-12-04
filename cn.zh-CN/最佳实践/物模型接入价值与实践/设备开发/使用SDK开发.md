使用SDK开发 
============================

物联网平台提供各类设备端SDK，支持您使用SDK开发设备。

实际开发中，请根据开发时使用的语言、平台，选用合适的设备端SDK。更多信息，请参见[下载设备端SDK](/cn.zh-CN/设备接入/下载设备端SDK.md)。

本示例使用Java SDK开发设备。

准备工作 
-------------------------

* 准备开发环境，具体操作，请参见[工程配置]()。

  

* 开发Java语言物模型，具体操作，请参见[物模型开发]()。

  




示例代码 
-------------------------

示例代码如下所示。将示例代码中的 *your_ProductKey* 、 *your_DeviceName* 、 *your_DeviceSecret* 替换为您自己的设备证书信息，即充电桩设备（device-1）的设备证书，其余代码可直接运行。
**说明**

为了避免初始化时订阅大量Alink协议中系统Topic带来的性能开销，平台提供了免订阅能力，即物联网平台帮设备进行Topic订阅。Topic相关说明，请参见[什么是Topic](/cn.zh-CN/设备接入/消息通信Topic/什么是Topic.md)。

    public class Demo {
    
        public static void main(String[] args) throws Exception {
    
            String pk = " 
    your_ProductKey 
    ";
            String dn = " 
    your_DeviceName 
    ";
            String ds = " 
    your_DeviceSecret 
    ";
    
            /**
             * 连接 & 认证
             */
            LinkKitInitParams params = new LinkKitInitParams();
    
            // 设置 Mqtt 初始化参数
            IoTMqttClientConfig config = new IoTMqttClientConfig();
            config.productKey = pk;
            config.deviceName = dn;
            config.deviceSecret = ds;
            config.receiveOfflineMsg = false;
            params.mqttClientConfig = config;
    
            // 设置初始化设备证书信息，用户传入
            DeviceInfo deviceInfo = new DeviceInfo();
            deviceInfo.productKey = pk;
            deviceInfo.deviceName = dn;
            deviceInfo.deviceSecret = ds;
    
            params.deviceInfo = deviceInfo;
    
            LinkKit.getInstance().init(params, new ILinkKitConnectListener() {
                public void onError(AError aError) {
                    System.out.println("===============FAILURE===============");
                    ALog.e(TAG, "Init Error error=" + aError);
                    System.out.println("===============FAILURE===============");
                }
    
                public void onInitDone(InitResult initResult) {
                    System.out.println("===============SUCCESS===============");
                    ALog.i(TAG, "onInitDone result=" + initResult);
                    System.out.println("===============SUCCESS===============");
                }
    
            });
    
            //此处sleep 5S，由于上面init是异步流程
            Thread.sleep(5000);
    
            /**
             * 物模型开发
             */
    
            /**
             * 上报属性
             */
            Map<String, ValueWrapper> properties = new HashMap<>();
    
            // key为物模型中属性标识符"acOutMeterIty"，value需要遵循属性值规范：int类型，取值范围在0~200之间；
            properties.put("acOutMeterIty", new ValueWrapper(10));
    
            LinkKit.getInstance().getDeviceThing().thingPropertyPost(properties, new IPublishResourceListener() {
    
                @Override
                public void onSuccess(String s, Object o) {
                    System.out.println("=====thingPropertyPost success=======");
                    System.out.println(s);
                    System.out.println(JSON.toJSONString(o));
                }
    
                @Override
                public void onError(String s, AError aError) {
                    System.out.println("=====thingPropertyPost failure=======");
                }
            });
    
            // 上报属性之后，云端会返回响应结果，此处是监听云端返回的属性reply
            LinkKit.getInstance().registerOnNotifyListener(new IConnectNotifyListener() {
    
                @Override
                public void onNotify(String s, String s1, AMessage aMessage) {
                    System.out.println("===PROPERTY REPLY===");
                    System.out.println("TOPIC：" + s1);
                    System.out.println("Payload：" + JSON.toJSONString(aMessage));
                }
    
                @Override
                public boolean shouldHandle(String s, String s1) {
                    return false;
                }
    
                @Override
                public void onConnectStateChange(String s, ConnectState connectState) {
                }
            });
    
            /**
             * 上报事件
             */
            HashMap<String, ValueWrapper> eventMap = new HashMap<>();
    
            // key为物模型中事件参数的标识符"gunNum", value为事件参数值需要遵循数值规范：int类型，取值范围0~100之间；
            eventMap.put("gunNum", new ValueWrapper.IntValueWrapper(50));
    
            OutputParams eventOutput = new OutputParams(eventMap);
    
            // 参数identity为"startChaResEvt"属于物模型事件标识符。
            LinkKit.getInstance().getDeviceThing().thingEventPost("startChaResEvt", eventOutput, new IPublishResourceListener() {
                public void onSuccess(String resId, Object o) {
                    System.out.println("=====thingEventPost success=======");
                    System.out.println(resId);
                    System.out.println(JSON.toJSONString(o));
                }
    
                public void onError(String resId, AError aError) {
                    System.out.println("=====thingEventPost failure=======");
                }
            });
    
            /**
             * 监听并执行下行服务
             */
            // 获取设备支持的所有服务
            LinkKit.getInstance().getDeviceThing().getServices();
    
            // 用户可以根据实际情况注册自己需要的服务的监听器
            List<Service> srviceList = LinkKit.getInstance().getDeviceThing().getServices();
    
            for (int i = 0; srviceList != null && i < srviceList.size(); i++) {
                Service service = srviceList.get(i);
    
                LinkKit.getInstance().getDeviceThing().setServiceHandler(service.getIdentifier(), new ITResRequestHandler() {
    
                    public void onProcess(String identify, Object result, ITResResponseCallback itResResponseCallback) {
    
                        System.out.println("onProcess() called with: s = [" + identify + "], o = [" + result + "], itResResponseCallback = [" + itResResponseCallback + "]");
                        System.out.println("收到云端异步服务调用 " + identify);
                        try {
                            /**
                             * 设置属性(property)的模式
                             */
                            // "set"为设置属性默认的标识符
                            if ("set".equals(identify)) {
                                // TODO 用户需要设置真实设备的属性
                                /**
                                 * 向云端同步设置好的属性值
                                 */
                                Map<String, ValueWrapper> desiredProperty = (Map<String, ValueWrapper>) ((InputParams) result).getData();
    
                                LinkKit.getInstance().getDeviceThing().thingPropertyPost(desiredProperty, new IPublishResourceListener() {
    
                                    @Override
                                    public void onSuccess(String s, Object o) {
                                        if (result instanceof InputParams) {
                                            Map<String, ValueWrapper> data = (Map<String, ValueWrapper>) ((InputParams) result).getData();
                                            //                        data.get()
                                            ALog.d(TAG, "收到异步下行数据 " + data);
                                            // 响应云端 接收数据成功
                                            itResResponseCallback.onComplete(identify, null, null);
                                        } else {
                                            itResResponseCallback.onComplete(identify, null, null);
                                        }
                                    }
    
                                    @Override
                                    public void onError(String s, AError aError) {
                                        AError error = new AError();
                                        error.setCode(100);
                                        error.setMsg("setPropertyFailed.");
                                        itResResponseCallback.onComplete(identify, new ErrorInfo(error), null);
                                    }
                                });
    
                                /**
                                 * 服务(service)的模式
                                 */
                                // "startChaResService"为服务的标识符
                            } else if ("startChaResService".equals(identify)) {
    
                                Map<String, ValueWrapper> inputParams = (Map<String, ValueWrapper>) ((InputParams) result).getData();
                                // TODO 根据服务入参inputParams执行设备逻辑，比如启动充电
                                // 充电完成后，向云端返回输出参数
                                OutputParams outputParams = new OutputParams();
                                // key为"charm"属于物模型中"startChaResService"服务出参标识符，value为出参值遵循数据规范：int类型，数据范围1~100之间；
                                outputParams.put("charm", new ValueWrapper.IntValueWrapper(20));
    
                                itResResponseCallback.onComplete(identify, null, outputParams);
    
                            } else {
                                // 根据不同的服务做不同的处理，跟具体的服务有关系
                                OutputParams outputParams = new OutputParams();
                                // 根据特定服务，按照服务规范返回服务的出参。
                                itResResponseCallback.onComplete(identify, null, outputParams);
                            }
                        } catch (Exception e) {
                            e.printStackTrace();
                            ALog.d(TAG, "云端返回数据格式异常");
                        }
                    }
                    public void onSuccess(Object o, OutputParams outputParams) {
                        ALog.d(TAG, "onSuccess() called with: o = [" + o + "], outputParams = [" + outputParams + "]");
                        ALog.d(TAG, "注册服务成功");
                    }
                    public void onFail(Object o, ErrorInfo errorInfo) {
                        ALog.d(TAG, "onFail() called with: o = [" + o + "], errorInfo = [" + errorInfo + "]");
                        ALog.d(TAG, "注册服务失败");
                    }
                });
            }
        }
    }



代码运行成功后：

* 上报属性成功，云端返回如下REPLY信息，表示设备与物联网平台成功进行通信。

  ![云端返回的REPLY信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5931649951/p140227.png)
  

* 设备收到属性设置指令，在物理设备上修改属性完成后，建议将最新属性同步上报到云端。

  




后续步骤 
-------------------------

[设备调试](/cn.zh-CN/最佳实践/物模型接入价值与实践/设备调试.md)

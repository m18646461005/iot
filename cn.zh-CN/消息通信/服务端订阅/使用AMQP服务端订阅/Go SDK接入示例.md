---
keyword: [IoT, 物联网平台, AMQP, 服务端订阅设备消息, Go]
---

# Go SDK接入示例

本文介绍使用AMQP协议的Go客户端接入阿里云物联网平台，接收服务端订阅消息的示例。

## 开发环境

本示例的测试环境为Go 1.12.7。

## 下载SDK

可使用以下命令导入Go语言AMQP SDK。

```
import "pack.ag/amqp"
```

SDK使用说明，请参见[package amqp](https://godoc.org/pack.ag/amqp)。

## 代码示例

以下Demo中涉及的参数说明，请参见[AMQP客户端接入说明](/cn.zh-CN/消息通信/服务端订阅/使用AMQP服务端订阅/AMQP客户端接入说明.md)。

```
package main

import (
    "context"
    "crypto/hmac"
    "crypto/sha1"
    "encoding/base64"
    "fmt"
    "pack.ag/amqp"
    "time"
)
//参数说明，请参见AMQP客户端接入说明文档。
const accessKey = "${YourAccessKey}"
const accessSecret = "${YourAccessSecret}"
const consumerGroupId = "${YourConsumerGroupId}"
const clientId = "${YourClientId}"
//iotInstanceId：企业版实例请填写实例ID，公共实例请填空字符串""。
const iotInstanceId = "${YourIotInstanceId}"
//接入域名，请参见AMQP客户端接入说明文档。
const host = "${YourHost}"

func main() {
    address := "amqps://" + host + ":5671"
    timestamp := time.Now().Nanosecond() / 1000000
    //userName组装方法，请参见AMQP客户端接入说明文档。
    userName := fmt.Sprintf("%s|authMode=aksign,signMethod=Hmacsha1,consumerGroupId=%s,authId=%s,iotInstanceId=%s,timestamp=%d|", 
        clientId, consumerGroupId, accessKey, iotInstanceId, timestamp)
    stringToSign := fmt.Sprintf("authId=%s&timestamp=%d", accessKey, timestamp)
    hmacKey := hmac.New(sha1.New, []byte(accessSecret))
    hmacKey.Write([]byte(stringToSign))
    //计算签名，password组装方法，请参见AMQP客户端接入说明文档。
    password := base64.StdEncoding.EncodeToString(hmacKey.Sum(nil))

    amqpManager := &AmqpManager{
        address:address,
        userName:userName,
        password:password,
    }

    //如果需要做接受消息通信或者取消操作，从Background衍生context。
    ctx := context.Background()

    amqpManager.startReceiveMessage(ctx)
}

//业务函数。用户自定义实现，该函数被异步执行，请考虑系统资源消耗情况。
func (am *AmqpManager) processMessage(message *amqp.Message) {
    fmt.Println("data received:", string(message.GetData()), " properties:", message.ApplicationProperties)
}

type AmqpManager struct {
    address     string
    userName     string
    password     string
    client       *amqp.Client
    session     *amqp.Session
    receiver     *amqp.Receiver
}

func (am *AmqpManager) startReceiveMessage(ctx context.Context)  {

    childCtx, _ := context.WithCancel(ctx)
    err := am.generateReceiverWithRetry(childCtx)
    if nil != err {
        return
    }
    defer func() {
        am.receiver.Close(childCtx)
        am.session.Close(childCtx)
        am.client.Close()
    }()

    for {
        //阻塞接受消息，如果ctx是background则不会被打断。
        message, err := am.receiver.Receive(ctx)

        if nil == err {
            go am.processMessage(message)
            message.Accept()
        } else {
            fmt.Println("amqp receive data error:", err)

            //如果是主动取消，则退出程序。
            select {
            case <- childCtx.Done(): return
            default:
            }

            //非主动取消，则重新建立连接。
            err := am.generateReceiverWithRetry(childCtx)
            if nil != err {
                return
            }
        }
    }
}

func (am *AmqpManager) generateReceiverWithRetry(ctx context.Context) error {
    //退避重连，从10ms依次x2，直到20s。
    duration := 10 * time.Millisecond
    maxDuration := 20000 * time.Millisecond
    times := 1

    //异常情况，退避重连。
    for {
        select {
        case <- ctx.Done(): return amqp.ErrConnClosed
        default:
        }

        err := am.generateReceiver()
        if nil != err {
            time.Sleep(duration)
            if duration < maxDuration {
                duration *= 2
            }
            fmt.Println("amqp connect retry,times:", times, ",duration:", duration)
            times ++
        } else {
            fmt.Println("amqp connect init success")
            return nil
        }
    }
}

//由于包不可见，无法判断Connection和Session状态，重启连接获取。
func (am *AmqpManager) generateReceiver() error {

    if am.session != nil {
        receiver, err := am.session.NewReceiver(
            amqp.LinkSourceAddress("/queue-name"),
            amqp.LinkCredit(20),
        )
        //如果断网等行为发生，Connection会关闭导致Session建立失败，未关闭连接则建立成功。
        if err == nil {
            am.receiver = receiver
            return nil
        }
    }

    //清理上一个连接。
    if am.client != nil {
        am.client.Close()
    }

    client, err := amqp.Dial(am.address, amqp.ConnSASLPlain(am.userName, am.password), )
    if err != nil {
        return err
    }
    am.client = client

    session, err := client.NewSession()
    if err != nil {
        return err
    }
    am.session = session

    receiver, err := am.session.NewReceiver(
        amqp.LinkSourceAddress("/queue-name"),
        amqp.LinkCredit(20),
    )
    if err != nil {
        return err
    }
    am.receiver = receiver

    return nil
}
```


---
keyword: [CoAP, RFC 7252, Internet of Things, DTLS v1.2, UDP, IoT, IoT Platform, device connection]
---

# CoAP standard

This article describes Constrained Application Protocol \(CoAP\) that is supported by IoT Platform.

## Protocol version

IoT Platform supports RFC 7252 Constrained Application Protocol. For more information, see [RFC 7252](http://tools.ietf.org/html/rfc7252).

## Channel security

IoT Platform uses Datagram Transport Layer Security \(DTLS\) Version 1.2 to ensure channel security. For more information, see [DTLS v1.2](https://tools.ietf.org/html/rfc6347).

## Open-source clients

For more information, see [https://coap.technology/impls.html](https://coap.technology/impls.html).

**Note:** Alibaba Cloud does not provide technical support for third-party code.

## Limits

-   The communication over CoAP feature is available only in the China \(Shanghai\) regions.
-   Resource discovery is not supported.
-   Only UDP is supported. DTLS and symmetric encryption are used to ensure data security.

## Description

-   You can use the Uniform Resource Identifier \(URI\) resources of CoAP in the same way as that for the URI resources of Message Queuing Telemetry Transport \(MQTT\). For more information, see [MQTT standard](/intl.en-US/Device Access/Protocols for connecting devices/Use MQTT protocol/MQTT standard.md).
-   You can use CoAP topics in the same way as that for MQTT topics. Replace`${topic}` in the `coap://host:port/topic/${topic}` topic syntax with a real topic name. This topic name can also be used for message communication over MQTT.
-   If a client passes authentication, IoT Platform returns a token. The client caches the token and uses the token to make requests.
-   The size of transmitted data changes based on the specified maximum transmission unit \(MTU\). We recommend that set the MTU to a maximum of 1 KB.
-   If IoT Platform identifies that a device reports data once or more over CoAP in the last 10 minutes, the device is in the Online state. The status appears in the IoT Platform console.


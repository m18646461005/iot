---
keyword: [物联网, IoT, 物联网平台, 数据解析, 转换, 脚本, 透传数据, 自定义格式, JSON]
---

# PHP脚本示例

本文提供PHP语言的物模型数据解析脚本模板和示例。

## 脚本模板

您可以基于以下PHP脚本模版编写数据解析脚本。

**说明：** 本模板仅适用于**数据格式**为**透传/自定义**的产品。

```
<?php
/**
 *  将Alink协议的数据转换为设备能识别的格式数据，物联网平台给设备下发数据时调用。
 *  入参：$jsonObj，关联数组。
 *  出参：$rawData，普通数组，数组元素为整数，取值范围为0~255，不能为空。
 */
function protocolToRawData($jsonObj)
{
    $rawData = array();
    return $rawData;
}

/**
 * 将设备的自定义格式数据转换为Alink协议的数据，设备上报数据到物联网平台时调用。
 * 入参：$rawData，普通数组，数组元素为整数。
 * 出参：$jsonObj，关联数组，数组key取值为英文字符串，不能是字符类型的数字，如"10"，不能为空。
 */
function rawDataToProtocol($rawData)
{
    $jsonObj = array();
    return $jsonObj;
}

/**
 * 将设备自定义Topic数据转换为JSON格式数据，设备上报数据到物联网平台时调用。
 * 入参：$topic，字符串，设备上报消息的Topic。
 * 入参：$rawData，普通数组，数组元素为整数。
 * 出参：$jsonObj，关联数组，数组key取值为英文字符串，不能是字符类型的数字，如"10"，不能为空。
 */
function transformPayload($topic, $rawData)
{
    $jsonObj = array();
    return $jsonObj;
}
```

## 脚本编写注意事项

-   请避免使用全局变量或者static变量，否则会造成执行结果不一致。
-   脚本中，处理数据采用补码的方式，\[-128, 127\]补码范围为\[0, 255\]。例如，-1对应的补码为255（10进制表示）。
-   解析设备上报数据的函数（rawDataToProtocol）的入参为整型数组。需要通过`0xFF`进行与操作，获取其对应的补码。返回结果为关联数组，要求key取值包含非数组字符（如数组key为“10”，PHP数组中会获取到整数10）。
-   解析物联网平台下发数据的函数（protocolToRawData）的返回结果为数组，要求为PHP普通数组。数组元素为整型，取值范围为0~255。
-   自定义协议解析的函数（transformPayload）的入参为整型数组。需要通过`0xFF`进行与操作，获取其对应的补码。返回结果为关联数组，要求key取值包含非数组字符（如数组key为“10”，PHP数组中会获取到整数10）。
-   PHP执行环境对于异常处理会很严格，如发生错误会直接抛出异常，后续代码不会执行。保证代码的健壮性，对于异常需要捕获并进行处理。

## 脚本示例

以下是基于[物模型数据解析使用示例](/intl.zh-CN/设备管理/数据解析/物模型数据解析/物模型数据解析使用示例.md)中定义的属性和通信协议编写的脚本。

```
<?php
/*
示例数据：
设备上报数据：
传入参数：
    0x0000000001003201
输出结果：
    {"method":"thing.event.property.post","id":"1","params":{"prop_int16":50,"prop_bool":1},"version":"1.0"}

属性设置的返回结果：
传入参数：
    0x0300223344c8
输出结果：
    {"code":"200","id":"2241348","version":"1.0"}
*/
function rawDataToProtocol($bytes)
{
    $data = [];
    $length = count($bytes);
    for ($i = 0; $i < $length; $i++) {
        $data[$i] = $bytes[$i] & 0xff;
    }

    $jsonMap = [];
    $fHead = $data[0]; //command字段。
    if ($fHead == 0x00) {
        $jsonMap['method'] = 'thing.event.property.post'; //ALink JSON格式，属性上报topic。
        $jsonMap['version'] = '1.0'; //ALink JSON格式，协议版本号固定字段。
        $jsonMap['id'] = '' . getInt32($data, 1); //ALink JSON格式，标示该次请求id值。
        $params = [];
        $params['prop_int16'] = getInt16($data, 5); //对应产品属性中prop_int16。
        $params['prop_bool'] = $data[7]; //对应产品属性中prop_bool。
        $jsonMap['params'] = $params; //ALink JSON格式，params标准字段。
    } else if ($fHead == 0x03) {
        $jsonMap['version'] = '1.0'; //ALink JSON格式，协议版本号固定字段。
        $jsonMap['id'] = '' . getInt32($data, 1); //ALink JSON格式，标示该次请求id值。
        $jsonMap['code'] = getInt8($data, 5);
    }

    return $jsonMap;
}

/*
示例数据：
属性设置：
传入参数：
    {"method":"thing.service.property.set","id":"12345","version":"1.0","params":{"prop_int16":333, "prop_bool":1}}
输出结果：
    0x013039014d01

设备上报的返回结果：
传入数据：
    {"method":"thing.event.property.post","id":"12345","version":"1.0","code":200,"data":{}}
输出结果：
    0x023039c8
*/
function protocolToRawData($json)
{
    $method = $json['method'];
    $id = $json['id'];
    $version = $json['version'];
    $payloadArray = [];
    if ($method == 'thing.service.property.set') //属性设置。
    {
        $params = $json['params'];
        $prop_int16 = $params['prop_int16'];
        $prop_bool = $params['prop_bool'];
        //按照自定义协议格式拼接rawData。
        $payloadArray = concat($payloadArray, hexStringToByteArray(toHex(0x01))); //command字段。
        $payloadArray = concat($payloadArray, hexStringToByteArray(toHex(intval($id)))); //ALink JSON格式'id'。
        $payloadArray = concat($payloadArray, hexStringToByteArray(toHex($prop_int16))); //属性'prop_int16'的值。
        $payloadArray = concat($payloadArray, hexStringToByteArray(toHex($prop_bool))); //属性'prop_bool'的值。
    } else if ($method == 'thing.event.property.post') { //设备上报数据返回结果。
        $code = $json['code'];
        $payloadArray = concat($payloadArray, hexStringToByteArray(toHex(0x02))); //command字段。
        $payloadArray = concat($payloadArray, hexStringToByteArray(toHex(intval($id)))); //ALink JSON格式'id'。
        $payloadArray = concat($payloadArray, hexStringToByteArray(toHex($code)));
    } else { //未知命令，对于这些命令不做处理。
        $code = $json['code'];
        $payloadArray = concat($payloadArray, hexStringToByteArray(toHex(0xff))); //command字段。
        $payloadArray = concat($payloadArray, hexStringToByteArray(toHex(intval($id)))); //ALink JSON格式'id'。
        $payloadArray = concat($payloadArray, hexStringToByteArray(toHex($code)));
    }
    return $payloadArray;
}

/*
  示例数据：
  自定义Topic：
     /user/update，上报数据。
  输入参数：
     topic: /{productKey}/{deviceName}/user/update
     bytes: 0x000000000100320100000000
  输出参数：
  {
     "prop_float": 0,
     "prop_int16": 50,
     "prop_bool": 1,
     "topic": "/{productKey}/{deviceName}/user/update"
   }
 */
function transformPayload($topic, $bytes)
{
    $data = array();
    $length = count($bytes);
    for ($i = 0; $i < $length; $i++) {
        $data[$i] = $bytes[$i] & 0xff;
    }

    $jsonMap = array();

    if (strpos($topic, '/user/update/error') !== false) {
        $jsonMap['topic'] = $topic;
        $jsonMap['errorCode'] = getInt8($data, 0);
    } else if (strpos($topic, '/user/update') !== false) {
        $jsonMap['topic'] = $topic;
        $jsonMap['prop_int16'] = getInt16($data, 5);
        $jsonMap['prop_bool'] = $data[7];
    }

    return $jsonMap;
}

function getInt32($bytes, $index)
{
    $array = array($bytes[$index], $bytes[$index + 1], $bytes[$index + 2], $bytes[$index + 3]);

    return hexdec(byteArrayToHexString($array));
}

function getInt16($bytes, $index)
{
    $array = array($bytes[$index], $bytes[$index + 1]);

    return hexdec(byteArrayToHexString($array));
}

function getInt8($bytes, $index)
{
    $array = array($bytes[$index]);
    return hexdec(byteArrayToHexString($array));
}

function byteArrayToHexString($data)
{
    $hexStr = '';
    for ($i = 0; $i < count($data); $i++) {
        $hexValue = dechex($data[$i]);

        $tempHexStr = strval($hexValue);

        if (strlen($tempHexStr) === 1) {
            $hexStr = $hexStr . '0' . $tempHexStr;
        } else {
            $hexStr = $hexStr . $tempHexStr;
        }
    }

    return $hexStr;
}

function hexStringToByteArray($hex)
{
    $result = array();
    $index = 0;
    for ($i = 0; $i < strlen($hex) - 1; $i += 2) {
        $result[$index++] = hexdec($hex[$i] . $hex[$i + 1]);
    }
    return $result;
}


function concat($array, $data)
{
    return array_merge($array, $data);
}

function toHex($data)
{
    $var = dechex($data);
    $length = strlen($var);
    if ($length % 2 == 1) {
        $var = '0' . $var;
    }
    return $var;
}
```


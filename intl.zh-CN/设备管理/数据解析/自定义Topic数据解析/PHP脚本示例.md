---
keyword: [物联网, IoT, 物联网平台, 数据解析, 转换, 脚本, 透传数据, 自定义格式, JSON]
---

# PHP脚本示例

本文提供PHP语言的自定义Topic数据解析脚本模板和示例。

## 脚本模板

PHP脚本模版，您可以基于以下模版编写数据解析脚本。

```
<?php
/**
 * 将设备自定义Topic数据转换为JSON格式数据，设备上报数据到物联网平台时调用。
 * 入参：$topic，字符串，设备上报消息的Topic。
 * 入参：$rawData，普通数组，数组元素为整数。
 * 出参：$jsonObj，关联数组，关联数组key取值为英文字符串不能是字符的数字如"10"，不能为空。
 */
function transformPayload($topic, $rawData)
{
    $jsonObj = array();
    return $jsonObj;
}
```

## 脚本编写注意事项

-   请避免使用全局变量或者static变量，否则会造成执行结果不一致。
-   脚本中，处理数据采用补码的方式， \[-128, 127\]补码范围为\[0, 255\]。例如，-1对应的补码为255（10进制表示）。
-   自定义协议解析的函数（transformPayload）的入参为整型数组。需要通过`0xFF`进行与操作，获取其对应的补码。返回结果为关联数组，要求key取值包含非数组字符（如数组key为“10”，PHP数组中会获取到整数10）。
-   PHP执行环境对于异常处理会很严格，如发生错误会直接抛出异常，后续代码不会执行。保证代码的健壮性，对于异常需要捕获并进行处理。

## 示例脚本

**说明：** 以下示例脚本仅用于解析自定义Topic数据。如果产品的**数据格式**为**透传/自定义**，还需编写物模型数据解析脚本。物模型数据解析脚本编写指导，请参见[物模型数据解析使用示例](/intl.zh-CN/设备管理/数据解析/物模型数据解析/物模型数据解析使用示例.md)。

```
<?php
/*
  示例数据
  自定义Topic：
     /user/update，上报数据。
  输入参数：
     topic: /{productKey}/{deviceName}/user/update
     bytes: 0x000000000100320100000000。
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


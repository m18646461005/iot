---
keyword: [物联网, IoT, 物联网平台, 数据解析, 转换, 脚本, 透传数据, 自定义格式, Alink JSON]
---

# Python脚本示例

本文提供Python语言的物模型数据解析脚本模板和示例。

## 脚本模板

您可以基于以下Python脚本模版编写数据解析脚本。

**说明：** 本模板仅适用于**数据格式**为**透传/自定义**的产品。

```
# 将设备的自定义格式数据转换为Alink协议的数据，设备上报数据到物联网平台时调用。
# 入参: rawData，列表，列表元素取值为int类型，不能为空。
# 出参: jsonObj，字典，不能为空。
def raw_data_to_protocol(rawData):
    jsonObj = {}
    return jsonObj

# 将Alink协议的数据转换为设备能识别的格式数据，物联网平台给设备下发数据时调用。
# 入参: jsonData，字典，不能为空。
# 出参: rawdata，列表，列表元素取值为int类型且大小为[0, 255]之间，不能为空。
def protocol_to_raw_data(jsonData):
    rawData = []
    return rawData
```

## 脚本编写注意事项

-   请避免使用全局变量，否则会造成执行结果不一致。
-   脚本中，处理数据采用补码的方式， \[-128, 127\]补码范围为\[0, 255\]。例如，-1对应的补码为255（10进制表示）。
-   解析设备上报数据的函数（raw\_data\_to\_protocol）的入参为整型数组。需要通过`0xFF`进行与操作，获取其对应的补码。
-   解析物联网平台下发数据的函数（protocol\_to\_raw\_data）的返回结果为数组。数组元素为整型，取值为\[0, 255\]。

## 脚本示例

以下是基于[物模型数据解析使用示例](/cn.zh-CN/设备管理/数据解析/物模型数据解析/物模型数据解析使用示例.md)中定义的属性和通信协议编写的脚本。

```
# coding=UTF-8
import struct
import common_util

COMMAND_REPORT = 0x00  # 属性上报。
COMMAND_SET = 0x01  # 属性设置。
COMMAND_REPORT_REPLY = 0x02  # 上报数据返回结果。
COMMAND_SET_REPLY = 0x03  # 属性设置设备返回结果。
COMMAD_UNKOWN = 0xff  # 未知的命令。
ALINK_PROP_REPORT_METHOD = 'thing.event.property.post'  # 物联网平台Topic，设备上传属性数据到云端。
ALINK_PROP_SET_METHOD = 'thing.service.property.set'  # 物联网平台Topic，云端下发属性控制指令到设备端。
ALINK_PROP_SET_REPLY_METHOD = 'thing.service.property.set'  # 物联网平台Topic，设备上报属性设置的结果到云端。
SELF_DEFINE_TOPIC_UPDATE_FLAG = '/user/update'  # 自定义Topic：/user/update。
SELF_DEFINE_TOPIC_ERROR_FLAG = '/user/update/error' # 自定义Topic：/user/update/error。


# 示例数据：
# 设备上报属性数据：
# 传入参数：
#    0x000000000100320100000000
# 输出结果：
#    {"method":"thing.event.property.post","id":"1","params":{"prop_float":0,"prop_int16":50,"prop_bool":1},"version":"1.0"}
# 属性设置的返回结果：
# 传入参数：
#    0x0300223344c8
# 输出结果：
#    {"code":"200","data":{},"id":"2241348","version":"1.0"}

def raw_data_to_protocol(bytes):
    uint8Array = []
    for byteValue in bytes:
        uint8Array.append(byteValue & 0xff)

    fHead = uint8Array[0]
    jsonMap = {}
    if fHead == COMMAND_REPORT:
        jsonMap['method'] = ALINK_PROP_REPORT_METHOD
        jsonMap['version'] = '1.0'
        jsonMap['id'] = str(bytes_to_int(uint8Array[1:5]))
        params = {}
        params['prop_int16'] = bytes_to_int(uint8Array[5:7])
        params['prop_bool'] = bytes_to_int(uint8Array[7: 8])
        params['prop_float'] = bytes_to_int(uint8Array[8:])
        jsonMap['params'] = params
    elif fHead == COMMAND_SET_REPLY:
        jsonMap['version'] = '1.0'
        jsonMap['id'] = str(bytes_to_int(uint8Array[1:5]))
        jsonMap['code'] = str(bytes_to_int(uint8Array[5:]))
        jsonMap['data'] = {}

    return jsonMap


# 示例数据：
# 云端下发属性设置指令：
# 传入参数：
#    {"method":"thing.service.property.set","id":"12345","version":"1.0",
#    "params":{"prop_float":123.452, "prop_int16":333, "prop_bool":1}}
# 输出结果：
#    0x0100003039014d0142f6e76d
# 设备上报的返回结果：
# 传入数据：
#    {"method":"thing.event.property.post","id":"12345","version":"1.0","code":200,"data":{}}
# 输出结果 ->
#    0x0200003039c8
def protocol_to_raw_data(json):
    method = json.get('method', None)
    id = json.get('id', None)
    version = json.get('version', None)
    payload_array = []

    if method == ALINK_PROP_SET_METHOD:
        params = json.get('params')
        prop_float = params.get('prop_float', None)
        prop_int16 = params.get('prop_int16', None)
        prop_bool = params.get('prop_bool', None)

        payload_array = payload_array + int_8_to_byte(COMMAND_SET)
        payload_array = payload_array + int_32_to_byte(int(id))
        payload_array = payload_array + int_16_to_byte(prop_int16)
        payload_array = payload_array + int_8_to_byte(prop_bool)
        payload_array = payload_array + float_to_byte(prop_float)

    elif method == ALINK_PROP_REPORT_METHOD:
        code = json.get('code', None)
        payload_array = payload_array + int_8_to_byte(COMMAND_REPORT_REPLY)
        payload_array = payload_array + int_32_to_byte(int(id))
        payload_array = payload_array + int_8_to_byte(code)
    else:
        code = json.get('code')
        payload_array = payload_array + int_8_to_byte(COMMAD_UNKOWN)
        payload_array = payload_array + int_32_to_byte(int(id))
        payload_array = payload_array + int_8_to_byte(code)

    return payload_array



#  示例数据：
#  自定义Topic：
#      /user/update，上报数据。
#  输入参数：
#      topic:/{productKey}/{deviceName}/user/update
#      bytes: 0x000000000100320100000000
#  输出参数：
#  {
#     "prop_float": 0,
#     "prop_int16": 50,
#     "prop_bool": 1,
#     "topic": "/{productKey}/{deviceName}/user/update"
#   }
def transform_payload(topic, bytes):
    uint8Array = []
    for byteValue in bytes:
        uint8Array.append(byteValue & 0xff)

    jsonMap = {}
    if SELF_DEFINE_TOPIC_ERROR_FLAG in topic:
        jsonMap['topic'] = topic
        jsonMap['errorCode'] = bytes_to_int(uint8Array[0:1])

    elif SELF_DEFINE_TOPIC_UPDATE_FLAG in topic:
        jsonMap['topic'] = topic
        jsonMap['prop_int16'] = bytes_to_int(uint8Array[5:7])
        jsonMap['prop_bool'] = bytes_to_int(uint8Array[7: 8])
        jsonMap['prop_float'] = bytes_to_int(uint8Array[8:])

    return jsonMap


# byte转成int。
def bytes_to_int(bytes):
    data = ['%02X' % i for i in bytes]
    return int(''.join(data), 16)


# byte转成float，不带精度。
def bytes_to_float(bytes):
    data = []
    for i in bytes:
        t_value = '%02X' % i
        if t_value % 2 != 0:
            t_value += 0
        data.append(t_value)
    hex_str = ''.join(data)
    return struct.unpack('!f', hex_str.decode('hex'))[0]


# 8位整型转成byte数组。
def int_8_to_byte(value):
    t_value = '%02X' % value
    if len(t_value) % 2 != 0:
        t_value += '0'

    return hex_string_to_byte_array(t_value)


# 32位整型转成byte数组。
def int_32_to_byte(value):
    t_value = '%08X' % value
    if len(t_value) % 2 != 0:
        t_value += '0'

    return hex_string_to_byte_array(t_value)


# 16位整型转成byte数组。
def int_16_to_byte(value):
    t_value = '%04X' % value
    if len(t_value) % 2 != 0:
        t_value += '0'

    return hex_string_to_byte_array(t_value)


# float转成整型数组。
def float_to_byte(param):
    return hex_string_to_byte_array(struct.pack(">f", param).encode('hex'))


# 16进制字符串转成byte数组。
def hex_string_to_byte_array(str_value):
    if len(str_value) % 2 != 0:
        return None

    cycle = len(str_value) / 2

    pos = 0
    result = []
    for i in range(0, cycle, 1):
        temp_str_value = str_value[pos:pos + 2]
        temp_int_value = int(temp_str_value, base=16)

        result.append(temp_int_value)
        pos += 2
    return result
```


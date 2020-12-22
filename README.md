# virupaksa

数据采集的统一调度平台

## 更新日志

### 2020.12.22

1. 常量文档添加海康威视的设备类型
2. 系统与命令对应表文档
   1. 安防系统部分添加海康威视及其支持的命令
   2. 视频服务部分添加海康威视及其支持的命令
3. 命令文档中
   1. 控制云台, 在请求中添加deviceId, deviceCode参数
   2. 控制镜头, 在请求中添加deviceId, deviceCode参数
   3. 云台快速定位,, 在请求中添加deviceId, deviceCode参数
   4. 锁定云台, 在请求中添加deviceId, deviceCode参数
   5. 云台灯光控制, 在请求中添加deviceId, deviceCode参数
   6. 云台雨刷控制, 在请求中添加deviceId, deviceCode参数
   7. 相机红外控制, 在请求中添加deviceId, deviceCode参数

## 特别说明

### 关于设备定位的问题

1. 有通道号 使用 平台+通道号
2. 有设备编号 使用 平台 + 设备编号
3. 有设备ID 使用 平台 + 设备ID 


三个定位方式的优先级是： 通道号 > 设备编号 > 设备ID

### 关于频道主题的问题

在MQTT规范中，主题分割符为“/”。但在实践过程中，[nodejs mqtt](https://github.com/mqttjs/MQTT.js) 库以及 [.net mqtt](https://github.com/chkr1011/MQTTnet) 库都支持以“.“为主题分割符，但是 Java 上的一些库是不支持的，必须要使用“/”作为主题分割符，这点请对接人员根据自己使用的MQTT库的规范来。文档中使用“.“作为主题分割符。		 在MQTT规范中，主题分割符为“/”。但在实践过程中，[nodejs mqtt](https://github.com/mqttjs/MQTT.js) 库以及 [.net mqtt](https://github.com/chkr1011/MQTTnet) 库都支持以“.“为主题分割符，但是 Java 上的一些库是不支持的，必须要使用“/”作为主题分割符，这点请对接人员根据自己使用的MQTT库的规范来。文档中使用“.“作为主题分割符。

## 系统与命令对应表

参考[系统与命令对应表](SYSTEM_COMMAND_EVENT_LIST.md)

## 命令接口

参考[命令接口文档](COMMAND_README.md)

## 事件部分

参考[事件文档](EVENT_README.md)

## 常量定义说明
参考[常量的说明](CONSTANTS_README.md)

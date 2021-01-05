# virupaksa

数据采集的统一调度平台

## 更新日志

### 2021.01.05 15:09:59

1. 常量文档
   1. bacPresentValue添加目标温度、 电池电量、用电量、门状态、电压、打开百分比、目标打开百分比、空调模式、空调风量
   2. bacPresentValue修改原表示电量的power 为功率
   3. lifesmart系统设备大类与设备类型添加智慧中心与区域
2. 事件文档
   1. bacPresentValue添加deviceCode
   2. bacAlarm添加deviceCode
3. 系统与命令对应表添加新的系统: { sdk: { manufacturer: 'lifesmart', platform: 'lgc'} }

### 2020.12.22

1. 常量文档添加海康威视的设备类型
2. 系统与命令对应表文档
   1. 安防系统部分添加海康威视及其支持的命令
   2. 视频服务部分添加海康威视及其支持的命令
3. 命令文档中
   1. 视频流和回放流, 在请求中添加deviceCode参数, 现在本参数暂时还不是强制性的
   2. 控制云台, 在请求中添加deviceId, deviceCode参数
   3. 控制镜头, 在请求中添加deviceId, deviceCode参数
   4. 云台快速定位,, 在请求中添加deviceId, deviceCode参数
   5. 锁定云台, 在请求中添加deviceId, deviceCode参数
   6. 云台灯光控制, 在请求中添加deviceId, deviceCode参数
   7. 云台雨刷控制, 在请求中添加deviceId, deviceCode参数
   8. 相机红外控制, 在请求中添加deviceId, deviceCode参数
4. 去除 设备定位的问题中 平台+通道号 规则

## 特别说明

### 关于设备定位的问题

2. 有设备编号 使用 平台 + 设备编号
3. 有设备ID 使用 平台 + 设备ID 


三个定位方式的优先级是： 设备编号 > 设备ID

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

# 系统与命令对应表
本文档解释了现有个采集系统实现的命令列表, 供对接参考使用

## 会议系统
### 命令列表
1. getAllMeetingRoom 
2. getMeetings
### 事件列表
1. newMeeting
2. meetingUpdate
3. chechinUpdate

## 智能窗帘系统
### 命令列表
1. getAllDevices 得到当前智能窗帘控制器设备列表
2. getAllBACPresentValue 得到所有窗帘控制器设备的当前状态, 1:打开、0.5:半开、0:关闭、-1:未知
3. openCurtain
4. closeCurtain

### 事件列表
1. bacPresentValue 窗帘控制器设备的当前状态

## 暖通系统
### 命令列表
1. getAllDevices
2. getAllBACPresentValue 得到暖通设备的当前值, 根据不同设备有不同的值, 比如温度、转速等, 只要直接显示就可以了

### 事件列表
1. bacPresentValue 暖通设备的当前值
2. bacAlarm 暖通设备的报警信息

## 食堂消费系统
### 命令列表
1. getConsumeTurnover 得到消费流水

### 命令列表
1. consumeTurnover 消费流水推送



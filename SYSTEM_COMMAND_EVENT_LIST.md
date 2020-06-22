# 系统与命令对应表
本文档解释了现有个采集系统实现的命令列表, 供对接参考使用

## 会议系统
### 现有的平台
```javascript
[
    { sdk: { manufacturer: 'itc', platform: 'cloud' } },
]
```
### 命令列表
1. getAllMeetingRoom 
2. getMeetings
3. getAllDevices
4. turnOnLight
5. turnOffLight
### 事件列表
1. newMeeting
2. meetingUpdate
3. chechinUpdate
4. meetingAgenda 会议议程通知, 当某个会议进行到一个新的议程的时间点前发出

## 智能窗帘系统
### 现有平台
```javascript
[
    { sdk: { manufacturer: 'lifesmart', platform: 'ToB' } },
]
```
### 命令列表
1. getAllDevices 得到当前智能窗帘控制器设备列表
2. getAllBACPresentValue 得到所有窗帘控制器设备的当前状态, 1:打开、0.5:半开、0:关闭、-1:未知
3. openCurtain
4. closeCurtain

### 事件列表
1. bacPresentValue 窗帘控制器设备的当前状态

## 暖通系统
### 现有平台
```javascript
[
    { sdk: { manufacturer: 'metasys', platform: 'metasys' } },
]
```
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

## 安防系统
### 现有平台
```javascript
[
    { sdk: { manufacturer: 'dahua', platform: 'H8900' } },
]
```
### 命令列表
1. getAllDevices 得到所有安防设备, 包括摄像头、报警器、门禁、道闸等
2. alarmQueryHistoryRecord 查询整个安防系统的报警历史记录
3. faceDetectionHistoryRecord 人脸检测记录查询
4. faceRecognitionRecord 人脸识别记录查询
5. facePersonFeatureecord 人体特征记录查询
6. carFeatureRecord 车辆特征记录查询
7. nonmotoFeatureRecord 非机动车特征记录查询
8. faceSearch 以图搜图, 非常的慢, 非必要不要调用

### 事件列表
1. faceDetect
2. faceRecognition
3. personFeature
4. carFeature
5. nonmotorFeature
6. deviceOnlineStatusChange 
7. deviceAlarm 设备报警, 推荐直接显示 alarmTypeStr 的内容

## 门禁系统
### 现有平台
```javascript
[
    { sdk: { manufacturer: 'dahua', platform: 'H8900' } },
]
```
### 命令列表
1. getAllDevices 得到所有门禁、包括普通门禁、人脸门禁
2. openDoor 
3. closeDoor
4. doorStayOpen
5. doorStayClose
6. accessControlQuerySwipeCardRecord 门禁刷卡记录
7. accessControlQueryAuthorizeRecord 门禁认证记录

### 事件列表
1. swipeCard 刷卡事件
2. authorRecord 认证记录

## 可视对讲系统管理
### 现有平台
```javascript
[
    { sdk: { manufacturer: 'dahua', platform: 'H8900' } },
]
```
### 命令列表
1. getAllDevices 得到所有可视对讲设备
2. openDoor
3. vimsQueryAlarmRecord 可视对讲报警记录
4. vimsQueryOpenDoorRecord 可视对讲开门记录

### 事件列表
暂时没有

## 访客系统
访客系统的设备现在阶段和门禁系统公用一个设备, 所以设备列表通过门禁系统就可以得到<br>访客记录和访客刷卡记录通过访客姓名进行对应
### 命令列表
1. getVisitorRecords
2. getVisitorSwipeCardRecords

### 事件列表
1. swipeCard 刷卡事件与门禁系统的刷卡事件共享, 通过cardType来进行区分

## 客流统计系统
### 现有平台
```javascript
[
    { sdk: { manufacturer: 'dahua', platform: 'H8900' } },
]
```
客流统计系统返回不同区域的实时客流情况
### 命令列表
1. getPassengeFlowRegions 得到客流区域的数据中就有当前客流的数据, 但不推荐使用者频繁刷新这个, 系统有提供事件让使用者得到实时客流数据

### 事件列表
1. passengerFlow 发送客流统计区域的客流数据



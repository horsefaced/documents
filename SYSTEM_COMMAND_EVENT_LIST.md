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
  	{ sdk: { manufacturer: 'lifesmart', platform: 'lgc'} },
]
```
### 命令列表
1. getAllDevices 得到当前智能窗帘控制器设备列表
2. getAllBACPresentValue 窗帘控制器设备的当前状态中, name=switch的状态描述了窗帘的开关状态, 1:打开、0.5:半开、0:关闭、-1:未知, value为数值部分, description为中文说明部分
3. openCurtain
4. closeCurtain
5. setSceneInArea
6. getAllScenesInAreas

### 事件列表

1. bacPresentValue 窗帘控制器设备的当前状态

## 暖通系统
### 现有平台
```javascript
[
    { sdk: { manufacturer: 'metasys', platform: 'metasys' } },
    { sdk: { manufacturer: 'siemens', platform: 'bas-opc' }},
]
```
### 命令列表
1. getAllDevices
2. getAllBACPresentValue 得到暖通设备的当前值, 根据不同设备有不同的值, 参考常量文档中的bacPresentValue一节的说明
3. basControl

### 事件列表

1. bacPresentValue 暖通设备的当前值, 根据不同设备有不同的值, 参考常量文档中的bacPresentValue一节的说明
2. bacAlarm 暖通设备的报警信息
3. deviceOnlineStatusChange

## 食堂消费系统
### 现有平台

```javascript
[
  { sdk: {manufacturer: 'zytk', platform: 'zytk'}}
]
```



### 命令列表

1. getConsumeTurnover 得到消费流水

### 命令列表
1. consumeTurnover 消费流水推送

## 安防系统

### 大华H8900

```javascript
{ sdk: { manufacturer: 'dahua', platform: 'H8900' } }
```
##### 命令列表

1. getAllDevices 得到所有安防设备, 包括摄像头、报警器、门禁、道闸等
2. alarmQueryHistoryRecord 查询整个安防系统的报警历史记录
3. faceDetectionHistoryRecord 人脸检测记录查询
4. faceRecognitionRecord 人脸识别记录查询
5. facePersonFeatureecord 人体特征记录查询
6. carFeatureRecord 车辆特征记录查询
7. nonmotorFeatureRecord 非机动车特征记录查询
8. faceSearch 以图搜图, 非常的慢, 非必要不要调用

##### 事件列表
1. faceDetect
2. faceRecognition
3. personFeature
4. carFeature
5. nonmotorFeature
6. deviceOnlineStatusChange 
7. deviceAlarm 设备报警, 推荐直接显示 alarmTypeStr 的内容

### 海康威视

```javascript
{ sdk: {manufacturer: 'hikvision', platform: 'openapi'}}
```

##### 命令列表

1. getAllDevices 得到所有设备

### 精华隆8100

```javascript
{ sdk: { manufacturer: 'innopro', platform: '8100' } }
```

##### 命令列表

1. getAllDevices 得到所有设备

##### 事件列表

1. deviceAlarm
2. deviceOnlineStatusChange

### 安士安全（声音符合系统)

```javascript
{ sdk: { manufacturer: 'asrc', platform: 'asrc' } }
```

#### 事件列表

1. deviceAlarm

### 大华u8000

```javascript
{ sdk: { manufacturer: 'dahua', platform: 'u8000'}}
```

#### 命令列表

1. getAllDevices
2. tripodheadControl
3. lensOperation
4. tripodheadLocate
5. tripodheadLock

#### 事件列表

1. deviceAlarm
2. deviceOnlineStatusChange

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
3. deviceAlarm 设备报警, 会提供当前门禁的开关门报警之外还有正常的开关门事件, 请参考常量文档中的设备报警一节

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
2. visitorCheck 访客登记事件. 本事件没有对应于访客列表的记录ID, 需要通过访客名称, 以及预约时间、到访时间、是否离开等数据进行对比, 相应的对访客列表进行添加或更新.


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


## 消防系统
### 现有平台
```javascript
[
    { sdk: { manufacturer: 'dahua', platform: 'firefighting' }}
]
```
### 命令列表
暂时没有
### 事件列表
1. deviceAlarm

## 云台操作
### 现有平台
```javascript
[
    { sdk: { manufacturer: 'dahua', platform: 'dpsdk' } },
]
```
### 命令列表
1. tripodheadControl
2. lensOperation

## 视频服务
### 现有平台
```javascript
[
    { sdk: { manufacturer: 'dahua', platform: 'H8900'}},
    { sdk: { manufacturer: 'hikvision', platform: 'openapi'}},
]
```
### 命令列表
1. getRealVideoSource
2. getPlaybackVideoSource

## 单兵系统

### 现有平台

```javascript
[
  { sdk: { manufacturer: 'dahua', platform: 'x9000'}},
]
```

### 命令列表

1. getAllDevices

### 事件列表

1. devicePosition 单兵设备GIS位置
2. deviceAlarm 设备报警
3. deviceOnlineStatusChange 设备在离线

## 音乐广播系统

### 现在平台

```javascript
[
  { sdk: { manufacturer: 'dsppa', platform: 'mag6180' }},
]
```

### 命令列表

1. getAllDevices
2. getMusicList
3. playMusic
4. setVolume
5. stopMusic

### 事件列表

1. deviceOnlineStatusChange
2. deviceAlarm
3. bacPresentValue //用于更新设备音量

## 考勤系统

### 现有平台

```javascript
[
  { sdk: {manufacturer: 'dahua', platform: 'H8900'}},
]
```

### 命令列表

1. getAttendanceReport

### 事件列表

1. attendanceResult

## 无线管理系统

现在有平台

```javascript
[
  { sdk: { manufacturer: 'sangfor', platform: 'wac-snmp'}},
]
```

### 命令列表

1. getAllDevices

### 事件列表

1. wacInfo
2. apInfo
3. deviceOnlineStatusChange

## 智能厕所管理系统

现有平台

```javascript
[
  { sdk: { manufacturer: 'topbeyond', platform: 'toilet'},} //鼎臻智能厕所系统
]
```

### 命令列表

1. getAllDevices

### 事件列表

1. toiletInfo
2. deviceOnlineStatusChange
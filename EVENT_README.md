# 事件文档

事件以消息广播的方式, 通过[Apache Artemis](https://activemq.apache.org/components/artemis/)进行.
使用方需通过订阅事件频道来得到广播的消息. 具体的接入方式, 参考Artemis的官方网站, 选用自身合适的方式即可.

## 频道

### 日志频道

#### 频道名
    log

#### 承载数据
```javascript
{
    message?:string; //消息内容
    level?: string; //消息类型, 现有 info, warning, fatal, 其中warning为普通的错误信息, fatal表示发生了让采集系统无法继续运行的错误, 需要尽快排查
    from?: string; //表明消息来源于那个采集子系统
}
```

### 实时数据频道

#### 频道名
实时数据频道由很多个频道组成, 它们都以 **realData.** 为开头, 用户可以根据自身需要针对性的订阅需要的频道数据, 以减轻数据处理负担

#### 承载数据
承载的数据都为json格式, 其中都含有如下属性, 其余的内容参考下面的具体实时数据说明.
```javascript
{
    sdk: {
        manufacturer?: string, //厂商名称, 如“dahua”等
        platform?: string; //厂商SDK名称, 如“H8900”等
    },

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

## 实时数据

### 刷卡记录

#### 频道名

    realData.swipeCard

#### 承载数据
```javascript
{
    recordId?: number;  //记录ID
    cardNumber?: string;  //卡号
    cardStatus?: number;   //卡状态
    cardStatusStr?: string; //卡状态说明,   0: '激活',1: '空白',2: '冻结',3: '注销',
    cardType?: number;     //卡类型
    cardTypeStr?: string; //卡类型说明, 0: '普通卡',1: 'VIP卡',2: '来宾卡',3: '巡逻卡',5: '胁迫卡',6: '巡检卡', 11: '管理员卡',

    channelId?: string;    //刷卡设备通道号
    channelName?: string;   //刷卡设备通道名称

    videoChannelId?: string;  //门禁对应的视频设备通道号
    videoChannelName?: string; //门禁对应的视频设备的通道名称

    deviceCode?: string;  //设备编码
    deviceName?: string;  //设备名称

    enterOrExit?: number; //刷卡是出还是入, 1: 进门, 2:出门, 3: 进/出门, 0:全部
    openResult?: boolean;   //开门结果
    openType?: number; //开门类型
    openTypeStr?: string; //开门类型说明

    personId?: number; //人员ID
    personName?: string; //人员名称
    personCode?: string;    //人员编号
    personImage?: string; //人员照片

    paperNumber?: string; //人员证件号码
    departmentName?: string; //部门名称

    time?: number;  //刷卡时间
    image?: string; //刷卡时抓拍图

    otherImages: Array<string> = [];
}
```

### 访客登记记录
#### 频道名
    realData.visitorCheck
#### 承载数据
```javascript
{
    personName?:string; //访客名称
    sex?: string; //性别
    phone?: string; //电话号码
    department?: string; //访客单位

    plateNumber?: string; //访客车牌号

    paperNumber?: string;   //访客证件号码
    paperType?: string; //访客证件类型
    paperImage?: string; //证件照片

    reason?: string; //访问原因

    bookTime?: number;  //预约时间
    bookLeaveTime?: number; //预约离开时间
    realTime?: number;//实际到达时间 
    realLeaveTime?: number; //实际离开时间

    image?: string; //证件头像
    snapImage?: string; //抓拍图片

    cardNumber?: string; //访客卡号

    respondentId?: string; //被访人ID
    respondentName?: string; //被访人名称
    respondentCode?: string; //被访人编号

    numberOfVisitor?: number; //访问人数

    status?: number; //访客状态
    statusStr?: string; //访客状态说明,0: '待审批',1: '预约',2: '来访',3: '离访',4: '预约取消',

    appointmentCode?: string; //预约码
}
```

### 考勤记录
#### 频道名
    realData.attendanceResult
#### 承载数据
```javascript
{
    personId?: string; //用户ID
    personCode?: string;    //人员编号
    personName?: string; //人员名称

    checkInTime?: number; //签到时间
    checkInStatus?: string; //考勤签入签出状态, 具体内容参考常量文档
    checkOutTime?: number; //签出时间
    checkOutStatus?: string; //考勤签入签出状态, 具体内容参考常量文档

    siteId?: string; //考勤ID
    siteName?: string; //考勤点名称
}
```

### 巡更点记录
#### 频道名
    realData.patrolPoint
#### 承载数据
```javascript
{
    recordId?: string; //记录ID

    routeId?: string; //巡更路线ID
    routeName?: string; //巡更路线名称

    scheduleId?: string; //排班ID
    scheduleTime?: number; //排班时间

    personId?: string; //巡更人员ID
    personName?: string; //人员名称

    departmentId?: string; //部门ID
    departmentName?: string; //部门名称

    groupId?: string; //班组ID
    groupName?: string; //班组名称

    pointSeq?: string; //巡更点序号
    pointCode?: string; //巡更点编码
    pointName?: string; //巡更点名称

    planTime?: number; //计划时间
    realTime?: number;  //实际时间

    planIntervalTime?: number; //计划间隔时间
    realIntervalTime?: number; //实际间隔时间

    status?: string; //巡更点结果
    createTime?: number; //记录创建时间

    snapImages: Array<string> = []; //巡更点抓拍图

}
```

### 巡更路线
#### 频道名
    realData.patrolRouter
#### 承载数据
```javascript
{
    routeId?: number; //路线ID
    routeName?: string; //路线名称

    scheduleId?: number; //排班ID
    scheduleTime?: number; //排班时间

    groupId?:number; //班组ID
    groupName?: string; //班组名称

    status?: string; //巡更状态
    result?: string; //巡更结果

    planStartTime?: number; //计划开始时间
    realStartTime?: number; //实际开始时间
    planEndTime?: number; //计划完成时间
    realEndTime?: number; //实际完成时间

    planUseTime?: number; //计划巡更时长
    realUseTime?: number; //实际巡更时长

    personId?: number; //人员ID
    personName?: string; //人员名称

    departmentId?: number; //部门ID
    departmentName?: string; //部门名称
}
```

### 过车记录
#### 频道名
    realData.carCapture
#### 承载数据
```javascript
{
    direct?: string; //行车方向, 
    time?: number; //抓拍时间
    carColor?: string; //车辆颜色
    plateNumber?: string; //车牌号码
    plateImage?: string; //车牌图片
    wayCode?: string; //车道号
    channelId?: string; //通道号
    channelName?: string; //通道名
    deviceCode?: string; //设备编码
    deviceName?: string; //设备名
    snapImage?: string; //抓拍图片
    parkingLotName?: string; //停车场名称
    parkingLotCode?: string; //停车场编号

}
```

### 车辆出入记录
#### 频道名
    realData.carAccess
#### 承载数据
```javascript
{
     plateNumber?: string; //车牌号
    personId?: number; //人员ID
    carType?: string //车辆类型: 内部/外部
    
    cardNumber?: string; //停车卡号
    
    enterVideoChannelId?: string; //入口视频通道号
    enterVideoChannelName?: string; //入口视频通道名称
    enterMode?: string; //入场方式, 0刷卡, 1自动识别
    enterChannelId?: string; //入口通道号
    enterChannelName?: string; //入口通道名称
    enterDeviceCode?: string; //入口设备编码
    enterDeviceName?: string; //入口设备名称
    enterTime?: number; //进入时间
    enterWayCode?: string; //进入车道编码
    enterSnapImage?: string; //进入抓拍图片
    enterSnapMinImage?: string; //进入抓拍小图

    exitplateNumber?: string; //出时车牌号
    exitVideoChannelId?: string; //出口视频通道号
    exitVideoChannelName?: string; //出口视频通道名称
    exitChannelId?: string; //出口通道号
    exitChannelName?: string; //出口通道名称
	  exitDeviceCode?: string; //出口设备编号
    exitDeviceName?: string; //出口设备名称
    exitTime?: number; //出时间
    exitWayCode?: string; //出车道号
    exitSnapImage?: string; //出抓拍图片
    exitSnapMinImage?: string; //出抓拍小图

    parkingLotName?: string; //停车场名称
    parkingLotCode?: string; //停车场编号

    money?:number; //费用   
}
```

### 缴费记录
#### 频道名
    realData.payment
#### 承载数据
```javascript
{
        time?: number; //消费时间
    receivable?: number;//应收金额
    paid?:number; //实收金额

    serialNumber?: string; //流水号
    feeType?: number; //收款类型
    dealType?: number; //处理类型

    personName?: string; //姓名

    plateNumber?: string; //车牌号
    carType?: string; //车辆类型
    enterTime?: number; //进入时间
    exitTime?: number; //出时间
    parkTime?:number; //停车时长

    operatorName?: string; //操作员
    enterChannelName?: string; //入口设备通道名称
    exitChannelName?: string; //出口设备通道名称

     parkingLotCode?: string; //停车场编码
}
```

### 人脸检测记录
#### 频道名
    realData.faceDetect
#### 承载数据
```javascript
{
        recordId?: string; //记录ID
    time?: number; //记录时间
    channelId?: string;//通道号
    channelName?: string; //通道名
    deviceId?: string;//设备ID
    deviceName?: string;//设备名
    deviceCode?: string;//设备编号

    snapImage?: string; //人脸抓图
    sceneSnapImage?: string;//场景图片

    age?: number; //年龄
    sex?: string; //性别
    feature?: string; //特征值
    featureString?: string; //特征值
}
```

### 人脸识别记录
#### 频道名
    realData.faceRecognition
#### 承载数据
```javascript
{
    paperNumber?: string; //证件号
    paperType?: string;//证件类型

    channelId?: string; //通道号
    channelName?: string; //通道名称
  
	  deviceCode?: string; //设备编号
    deviceName?: string; //设备名称

    personName?: string; //姓名

    image?: string; //照片
    snapImage?: string; //人脸抓拍
    sceneSnapImage?: string;//场景抓拍

    personId?: string; //人员ID
    sex?: string; //性别
    province?: string; //省份
    city?: string; //城市

    groupId?: number; //人脸库ID
    groupName?: string; //人脸库名称
    groupType?: number; //人脸库类型
    groupTypeStr?: string; //人脸库类型说明

    similarity?: number; //相似度
    featureString?: string; //特征值

    time?: number; //识别时间
}
```

### 人体特征记录
#### 频道名
    realData.personFeature
#### 承载数据
```javascript
{
        recordId?: string; //记录ID
    image?: string; //人脸图片
    featureImages: Array<string> = []; //图片扩展

    time?: number; //识别时间

    deviceId?: string; //设备ID
    deviceName?: string; //设备名称
    deviceCode?: string; //设备编码

    channelId?: string; //通道号
    channelName?: string; //通道名

    coatColor?: string; //衣服颜色
    coatType?: string; //衣服类型

    trousersColor?: string; //裤子颜色
    trousersType?: string;  //裤子类型

    hasHat?: string;    //是否有帽子
    hasBag?: string;    //是否背包

    sex?: string; //性别
    age?: number; //年龄
    complexion?: string; //肤色
    eye?: string;   //眼睛状态
    mouth?: string; //嘴巴状态
    mask?: string;  //口罩状态
    beard?: string; //胡子状态
    featureString?: string; //特征值
}
```

### 机动车特征记录
#### 频道名
    realData.carFeature
#### 承载数据
```javascript
{
    plateNumber?: string; //车牌号
    plateImage?: string; //车牌图片
    plateType?: string; //车牌类型
    plateColor?: string; //车牌颜色

    image?: string; //抓拍图片
    featureImages: Array<string> = []; //图片扩展

    time?: number; //记录时间

    deviceId?: string; //设备Id
    deviceName?: string; //设备名称
    deviceCode?: string; //设备编码
    channelId?: string; //通道号
    channelName?: string; //通道名

    carColor?: string; //车辆颜色
    carType?: string; //车型
    carLogo?: string; //车标

}
```

### 非机动车特征记录
#### 频道名
    realData.nonmotorFeature
#### 承载数据
```javascript
{
    image?: string; //抓拍图片
    featureImages: Array<string> = []; //图片扩展

    time?: number; //时间

    deviceId?: string; //设备ID
    deviceName?: string; //设备名称
    deviceCode?: string; //设备编码
    channelId?: string; //通道号
    channelName?: string; //通道名

    numOfCycling?: number; //车上人数

    sex?: string; //性别
    age?: number; //年龄
    helmet?: string; //头盔状态
    isCall?: string; //是否在打电话
    hasHat?: string; //是否戴帽子
    hasBag?: string;    //是否有背包
    hasCarrierBag?: string; //是否有手提包
    hasUmbrella?: string;  //是否带雨伞
    hasGlasses?: string; //是否有眼镜
    hasMask?: string; //是否戴口罩
    emotion?: string; //表情

    upClothesType?: string; //上衣类型
    upClothesColor?: string; //上衣颜色
    downClothesType?: string; //下衣类型
    downClothesColor?: string; //下衣颜色

    carType?: string; //车类型
    carColor?: string; //车颜色

}
```

### 设备在线状态
#### 频道名
    realData.deviceOnlineStatusChange
#### 承载数据
```javascript
{
    deviceId?: string; //设备ID
    deviceCode?: string; //设备编号
    deviceName?: string; //设备名称
    isOnline: boolean; //设备是否在线
    time: number; //发生时间
}
```

### 设备报警
#### 频道名
    realData.deviceAlarm
#### 承载数据
```javascript
{
    deviceCode: string; //设备编号
    deviceName?: string; //设备名
    channelId?: string; //通道号
    channelName?: string; //通道名
    videoChannelId?: string; //视频通道号
    videoChannelName?: string; //视频通道名称
    alarmType: string; //报警类型
    alarmTypeStr: string; //报警类型说明
    time:number; //报警时间
    alarmCode?: string; //报警编码, 内部使用
    status: number; //报警状态, 1-报警产生, 2-报警消失
    images?: Array<string>; //现场抓拍图片
    message?: string; //报警的其他信息
}
```

### 认证记录
#### 频道名
    realData.authorRecord
#### 承载数据
```javascript
{
    personName?: string; //人员名称
    age?: number; //年龄
    sex?: string; //性别
    birthday?: string; //出生日期
    address?: string; //地址
    authority?: string; //发证机关
    image?: string; //照片
    ethnic?: string; //民族
    similarity?: number; //相似度
    startTime?: number; //证件开始时间
    endTime?: number; //证件结束时间
    paperNumber?: string; //证件号码
    deviceCode?: string; //设备编码
    deviceName?: string; //设备名称
    channelId?: string; //通道号
    channelName?: string; //通道名

    result?:boolean; //对比结果
    time?: number; //对比时间
}
```

### 环境检测
#### 频道名
    realData.envirMonitor
#### 承载数据
```javascript
{
    FSUDeviceCode?: string; //现场检测单元设备编码
    FSUChannelId?: string; //现场检测单元通道号

    deviceCode?: string; //对应的平台设备编码

    value?: string; //测量值
    signalCode?: string; //信号编码
    signalName?: string; //信号名称
    unit?: string; //单位
    status?: number; //状态
    time?: number; //上报时间
    type?: number; //数据类型, 3为实时数据
}
```

### 动环检测报警
#### 频道名

    realData.pessAlarm
#### 承载数据
```javascript
{
    deviceCode?: string; //设备编码
    deviceName?: string; //设备名称
    channelId?: string; //通道号
    channelName?: string; //通道名
    type?: string; //报警类型
    time?: number; //报警时间
    status?: number; //状态 1-产生, 2-消失
}
```

### 新的会议预约
#### 频道名
    realData.newMeeting
#### 承载数据
```javascript
{
    id?: number; //会议id
    subject?: string; //会议主题
    startTime?: number; //开始时间
    endTime?: number; //结束时间
    creator?: string; //会议建立人名称
    leaders: Array<{ name: string, avatar?: string }> = []; //主持人
    attenders: Array<{ name: string, avatar?: string }> = []; //参会人员
    createTime?: number; //建立时间
    updateTime?: number; //更新时间
    needCheckin: boolean = true; //是否需要签到
    checkinAheadTime?: number; //提前签到时间, 分钟数
    room?: MeetingRoom; //使用房间, 参考命令文档中得到会议室命令
    status?: number; //状态
    statusStr?: string; //状态文字
    checkinList: Array<MeetingCheckinData> = [{ //会议签到情况
        meetingId?: number; //会议id
        name?: string; //签到人名称
        avatar?: string; //头像
        checkinTime?: number; //签到时间
    }]; 
    agenda: [{
        meetingId?: number; //会议id
        subject?: string; //会议议程主题
        time?: number; //开始时间
        leader?: { name: string, avatar?: string }; //主持人
        attenders: Array<{ name: string, avatar?: string }> = []; //参会人员
    }];
}
```

### 会议内容更新
    如果会议内容有更新则触发
#### 频道名
    realData.meetingUpdate
#### 承载数据
```javascript
{
    id?: number; //会议id
    subject?: string; //会议主题
    startTime?: number; //开始时间
    endTime?: number; //结束时间
    creator?: string; //会议建立人名称
    leaders: Array<{ name: string, avatar?: string }> = []; //主持人
    attenders: Array<{ name: string, avatar?: string }> = []; //参会人员
    createTime?: number; //建立时间
    updateTime?: number; //更新时间
    needCheckin: boolean = true; //是否需要签到
    checkinAheadTime?: number; //提前签到时间, 分钟数
    room?: MeetingRoom; //使用房间, 参考命令文档中得到会议室命令
    status?: number; //状态
    statusStr?: string; //状态文字
    checkinList: Array<MeetingCheckinData> = [{ //会议签到情况
        meetingId?: number; //会议id
        name?: string; //签到人名称
        avatar?: string; //头像
        checkinTime?: number; //签到时间
    }]; 
    agenda: [{
        meetingId?: number; //会议id
        subject?: string; //会议议程主题
        time?: number; //开始时间
        leader?: { name: string, avatar?: string }; //主持人
        attenders: Array<{ name: string, avatar?: string }> = []; //参会人员
    }];
}
```

### 会议签到情况更新
#### 频道名
    realData.checkinUpdate
#### 承载数据
```javascript
{
    meetingId?: number; //会议id
    checkinList: [
        {
            meetingId?: number; //会议id
            name?: string; //签到人名称
            avatar?: string; //头像
            checkinTime?: number; //签到时间
        }
    ]
}
```

### 会议议程通知
#### 频道名
    realData.meetingAgenda
#### 承载数据
```javascript
{
    meetingId?: number; //会议id
    subject?: string; //会议议程主题
    time?: number; //开始时间
    leader?: { name: string, avatar?: string }; //主持人
    attenders: Array<{ name: string, avatar?: string }> = []; //参会人员    
}
```

### 智能楼宇设备的当前值
#### 频道名
    realData.bacPresentValue
#### 承载数据
```javascript
{
    deviceId?: string; //设备ID
    deviceCode: string; //设备编码
    value?: any;    //当前值   
    name?: string;  //值名称  名称参考常量文档中 bacPresentValue 描述 这一部分
    description?: string;   //说明
    time: number; //值的产生时间
}
```

### 智能楼宇报警信息
#### 频道名
    realData.bacAlarm
#### 承载数据

```javascript
{
    id?: string;
    deviceId?: string; //设备ID
  	deviceCode: string; //设备编码
    value?: any;    //报警值
    name?: string;  //报警值名称
    priority?: number;  //报警优先级
    type?: string; //报警类型  因metasys文案暂无说明, 这条需要实际对接后才能得到
    unit?: string; //报警值单位
    time?: number; //报警时间
    message?: string; //报警信息
    isSoluted: boolean = false; //报警是否解除
}
```

### 消费流水数据
#### 频道名
    realData.consumeTurnover
#### 承载数据
```javascript
{
    serialNumber?: string; //流水号

    cardNumber?: string; //交易卡号
    personName?: string; //姓名
    personDepartment?: string; //人员所在部门

    dealerID?: string; //商户号
    dealerName?: string; //商户名称

    terminalID?: string; //交易终端号

    dealType?: number; //交易类型 -1: '其它', 1: '消费', 2: '充值', 3: '补助',
    dealTypeStr?: string; //交易类型名称

    paid?: number; //交易金额    

    time?: number; //交易时间
    bookTime?: number; //入账时间 
}
```

### 客流数据
#### 频道名

    realData.passengerFlow
#### 承载数据
```javascript
{
    id?: string; //区域ID
    regionCode?: string; //区域编码
    regionName?: string; //区域名称
    toDayOutNumber?: number; //当天出去人数
    toDayEnterNumber?: number; //当天进入人数
    realTimeNumber?: number; //实时人数
    upperLimit?: number; //人数上限
    updateTime?: number; //数据更新时间
  
    sourceDeviceCode?: string; //客流数据来源设备编码
}
```

### 消防设备状态(废弃)

现在使用realData.deviceAlarm 代替

#### 频道名
    realData.firefightingDeviceStatus
#### 承载数据

```javascript
{
    deviceCode?: string; //设备编号, 暂时设备编码例如01-0001-0001, 系统地址-部件回路-部件地址, 待到实际中进行调整
    deviceType?: number; //消防设备类型
    deviceTypeStr?: string; //消防设备类型说明
    deviceStatus?: number; //消防设备状态, 对于消防设备, 不是正常的状态就是告警, 如果一个设备先有告警, 然后恢复正常状态, 则为解警
    deviceStatusStr?: string; //消防设备状态说明
    time?: number; //报警时间    
}
```

### 设备位置

#### 频道名

```
realData.devicePosition
```

#### 承载数据

```javascript
{
    public deviceCode: string, //设备编号
    public lon: number, //经度
    public lat: number, //纬度
    public time: number = new Date().getTime(), //上报时间
    public height: number = 0, //高度(米)
    public angle: number = 0, //方向角(正北为0，顺时针，单位度)
    public speed: number = 0, //速度
}
```

### 无线接入控制系统信息更新

#### 频道名

```
realData.wacInfo
```

#### 承载数据

```json
{
  "deviceCode": "string, //设备编号",
  "WACName": "string; //wac名称",
  "WACIP": "string; //IP地址",
  "WACMAC": "string; //MAC地址",
  "WACMask": "string; //子网掩码",
  "WACSysCpuCostRate": "number; //wac的cpu利用率(小数代表的百分比,45%表示为0.45)",
  "WACTotalMemory": "number; //wac总内存空间(bytes)",
  "WACSysMemoryCost": "number; //wac内存占用率(小数代表的百分比,45%表示为0.45)",
  "WACSysRunTime": "number; //wac运行时长(毫秒)",
  "WACAPOnlineNum": "number; //AP在线数目",
  "WACAPOfflineNum": "number; //AP离线数目",
  "WACAPDepositNum": "number; //AP托管数目",
  "WACAPTotalNum": "number; //AP总数",
  "WACAPMaxConnectNum": "number; //AP能连接的总数",
  "WACUserNum": "number; //wac当前在线用户总数",
  "WACMaxUserNum": "number; //wac允许最大用户数",
  "WACDiskSize": "number; //磁盘大小(bytes)",
  "WACDiskUsed": "number; //已使用空间(bytes)",
  "WACDiskAvail": "number; //可用空间(bytes)",
  "WACDiskUsedPercent": "number; //使用率(小数代表的百分比,45%表示为0.45)",
  "WACDiskTable": [{
    "FilesystemName": "string; //文件系统名",
    "DiskSize": "number; //磁盘大小(bytes)",
    "DiskUsed": "number; //已使用空间(bytes)",
    "DiskAvail": "number; //可用空间(bytes)",
    "DiskUsedPercent": "number; //使用率(小数代表的百分比,45%表示为0.45)"
  }],
  "WACDHCPTable": [{
    "Name": "string; //端口名称",
    "NumOfTotalIPAddresses": "number; //ip地址池大小",
    "NumOfLeftIP": "number; //未分配ip地址数",
    "NumOfOccupyIP": "number; //占用的ip地址数",
    "StartIP": "string; //起始的IP地址",
    "EndIP": "string; //终止的IP地址",
    "IPUsedRatio": "number; //IP地址使用率(小数代表的百分比,45%表示为0.45)"
  }],
  "SSIDTable": [{
    "Name": "string; //ssid名称",
    "Enabled": "string; //是否启用",
    "IsHided": "string; //是否隐藏",
    "IsolateUser": "string; //终端之间是否隔离",
    "SecurityType": "string; //安全类型",
    "AuthMode": "string; //认证模式",
    "EncryptType": "string; //加密模式",
    "VLANId": "string; //vlan id",
    "MaxUserNum": "number; //最大允许连接的用户数",
    "MaxSendRate": "string; //终端最大上行速率",
    "MaxReceiveRate": "string; //终端最大下午速率",
    "SendRate": "string; //当前上行速率",
    "ReceiveRate": "string; //当前下午速率",
    "UserNum": "number; //当前用户数"
  }]
}
```



### 无线访问接收点信息更新

#### 频道名

```
realData.apInfo
```

#### 承载数据

```json
{
  	"deviceCode": "string, //设备编号",
  "APInfoTable": {
    "Name": "string; //AP名称",
    "MAC": "string; //MAC地址",
    "Status": "string; //当前是否在线",
    "IP": "string; //IP地址",
    "Mask": "string; //掩码地址",
    "Model": "string; //型号",
    "SeriesNum": "string; //序列号",
    "HardVersion": "string; //硬件版本",
    "SoftwareVersion": "string; //软件版本",
    "CpuCost": "number; //CPU利用率(小数代表的百分比,45%表示为0.45)",
    "MemoryCost": "number; //内存利用率(小数代表的百分比,45%表示为0.45)",
    "FlashCost": "number; //内存利用率(小数代表的百分比,45%表示为0.45)",
    "OnlineTime": "number; //在线时长(毫秒)",
    "RunTime": "number; //运行时长(毫秒)",
    "InterfaceNum": "number; //物理接口数",
    "UserNum": "number; //用户数",
    "GroupName": "string; //所在组名",
    "SessionNum": "number; //会话数",
    "SendRate": "string; //发送速率",
    "ReceiveRate": "string; //接收速率"
  },
  "APRadioInfoTable": [{
    "Type": "string; //AP类型",
    "Name": "string; //AP名称",
    "MAC": "string; //MAC地址",
    "Mode": "string; //射频模式",
    "Status": "string; //射频状态",
    "BeaconCycle": "string; //射频信标周期",
    "DTIM": "string; //射频DTIM时间间隔",
    "RTS": "string; //射频RTS阈值",
    "Channel": "number; //射频信道",
    "MaxTranPower": "string; //射频最大发射功率",
    "MaxAcSta": "number; //射频最大关联终端数",
    "Frequence": "string; //射频频率",
    "SSID": "string; //加载的ssid",
    "VLAN": "number; //vlan",
    "WorkMode": "string; //工作模式",
    "UseRate": "string; //信道利用率",
    "TXPower": "string; //发射功率",
    "Noise": "string; //噪声",
    "IPAddress": "string; //IP地址"
  }],
  "APWirelessInfoTable": [{
    "Port": "string; //端口名称",
    "Name": "string; //AP名称",
    "MAC": "string; //MAC地址",
    "PortMAC": "string; //端口MAC地址",
    "PortBandwidth": "number; //端口带宽",
    "Status": "string; //端口状态",
    "ReceiveByte": "number; //端口接收流量(bytes)",
    "ReceiveErrorPacket": "number; //接收错误包数",
    "ReceivePacket": "number; //接收包数",
    "ReceiveUnicastPacket": "number; //接收单播包数",
    "ReceiveBroadcastPacket": "number; //接收广播包数",
    "DropReceivePacket": "number; //接收丢包数",
    "SendByte": "number; //端口发送流量(bytes)",
    "SendErrorPacket": "number; //发送错误包数",
    "SendBroadcastPacket": "number; //发送广播包数",
    "SendUnicastPacket": "number; //发送单播包数",
    "DropSendPacket": "number; //发送丢包数",
    "SendPacket": "number; //发送包数"
  }],
  "APWiredInfoTable": [{
    "Port": "string; //端口名称",
    "Name": "string; //AP名称",
    "MAC": "string; //MAC地址",
    "HardVersion": "string; //硬件版本",
    "PortMAC": "string; //端口MAC地址",
    "PortBandwidth": "number; //端口带宽",
    "Status": "string; //端口状态",
    "ReceiveByte": "number; //端口接收流量(bytes)",
    "ReceiveErrorPacket": "number; //接收错误包数",
    "ReceivePacket": "number; //接收包数",
    "ReceiveUnicastPacket": "number; //接收单播包数",
    "ReceiveBroadcastPacket": "number; //接收广播包数",
    "DropReceivePacket": "number; //接收丢包数",
    "SendByte": "number; //端口发送流量(bytes)",
    "SendErrorPacket": "number; //发送错误包数",
    "SendUnicastPacket": "number; //发送单播包数",
    "SendBroadcastPacket": "number; //发送广播包数",
    "DropSendPacket": "number; //发送丢包数",
    "SendPacket": "number; //发送包数"
  }]
}
```


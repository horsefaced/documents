# 命令接口

## 调用方法
用户通过命令接口向数据采集平台发送操作命令, 采集平台运行后返回结果.

#### Request
- Method: **POST**
- URL: ```http://ip:port/command```
- Headers: Content-Type: application/json
- Body: 
```javascript
    {
        id: string, //命令的唯一ID, 由调用者生成, 用于区别每次请求的命令
        name: string, //命令名, 本次需要执行的命令名称
        params: any, //本次命令的参数, 根据不同的命令, 需要提供的参数不同
    }
```

#### Response
- Body: 

```javascript
{
  id: string, //执行的命令id
  name: string, //执行的命令名
  success: boolean, //命令的执行是否成功
  //当success == true时, 可以从 data 中得到返回的数据, 具体返回数据格式和数量由各个命令不同
  //有一些命令不会返回数据, 这本数组为空数组
  data: [], 
  //当 success == false 时, 可以从这里得到失败的原因说明
  //这个消息和下面的 errMsgs 的第一个消息相同
  errMsg: string, 
  //在通常情况下, errMsg就足以使用, 但是在一个命令由多个子系统同时执行时, 可能有的子系统成功, 有的子系统失败, 
  //在这种情况下, 只要有一个子系统成功, 系统会认为命令是执行成功的, success 将会为 true,  成功的结果会放在 data 中, 
  //同时会把返回失败结果的子系统的失败信息记录在 errMsgs 中. 
  //但是如果所有子系统都失败了, 则 success 将为 false, errMsgs中也同样会保持各个子系统的失败信息.
  errMsgs: [{
      name: string, //子系统名称
      msg: string, //错误信息
  }]
}
```


## 命令列表

1. 没有返回值的命令, 直接通过 success 是否为 true 来表明命令执行结果
2. params中的时间格式都为:  yyyy-MM-dd HH:mm:ss
3. 返回结果中的时间都为时间戳
4. **返回结果中只是描述了 data 数组中的单个元素的类型**
5. 所有返回值都有 sdk 这个属性, 其内部结构为
```javascript
{
    manufacturer: 'dahua', //厂商名称, 表明数据提供厂商, 现有'dahua'
    platform: 'H8900', //厂商SDK的名称
}
```

### 得到实时监控视频地址

#### name
    'getRealVideoSource'

#### params
需要得到视频地址的设备列表, 下面只列出必要的参数
```javascript
{
  	mainStream: boolean; //是否取主流, 如果为false, 或者为空则是副流
    type: 'rtsp'; //支持rtsp和hls两种格式, 默认是rtsp
    devices: [{
        deviceId: string;   //设备ID
        deviceCode: string; //设备编码
        channels: [{                //设备通道号列表
            id?: string; //通道号
        }],

        dataSource: string; //子系统名称,
        raw: //保存着对应厂家系统回传的原始数据
    }],
}
```

#### 返回数据
```javascript
{
    deviceId: string; //设备ID
    deviceCode: string; //设备编码
    channelId: string; //通道号
    source: string; //视频流地址
    
    dataSource: string; //子系统名称
}
```

### 得到监控视频回放地址

#### name
    'getPlaybackVideoSource'

#### params
需要得到视频地址的设备列表, 下面只列出必要的参数
```javascript
{
    mainStream: boolean; //是否取主流, 如果为false, 或者为空则是副流
    type: 'rtsp'; //支持rtsp和hls两种格式, 默认是rtsp
    devices: [{
        deviceId: string;   //设备ID
        deviceCode: string; //设备编码
        channels: [{                //设备通道号列表
            id?: string; //通道号
        }],

        dataSource: string; //子系统名称,
        raw: //保存着对应厂家系统回传的原始数据
    }],
    start: string; //开始时间
    end: string; //结束时间
}
```
#### 返回数据
```javascript
[{
    deviceId: string; //设备ID
    deviceCode: string; //设备编码
    channelId: string; //通道号
    source: string; //视频流地址
    
    dataSource: string; //子系统名称
}]
```

### 得到所有设备

#### name
    'getAllDevices'

#### params
    无需参数

#### 返回数据
会返回得到的所有设备的数组
```javascript
{
    deviceId: String; //设备ID,
    deviceName: String; //设备名称, 
    deviceCode: String; //设备编码, 
    deviceIp?: String; //设备IP,
    deviceCategory?: number; ///设备大类, 现在先用大华的, 
    deviceCategoryStr?: string; //设备大类中文名
    deviceType: number; //设备类型, 大华的, 
    deviceTypeStr: string; //设备类型中文名
    deviceUnitType?: number; //设备单元类型, 不一定有
    deviceUnitTypeStr?: string; //设备单元类型中文名
    isDeviceOnline: boolean; //设备在线状态
    channels: [{                //设备通道号列表
        id?: string; //通道号
        name?: string; //通道名称
        seq?: number; //通道序列号
        unitType?: number; //通道对应的设备单元类型
        sn?: string; //通道对应设备的SN号
        type?: number; //通道类型, 其中 1 为视频通道, 0 为内部使用类型
    }],
    orgCode?: string; //设备组织编码, 不一定有,也不一定有用
    sn?: string; //设备sn号, 不一定有, 也不一定有用
    status?: number; //设备状态, 不一定有, 也不一有用
    statusStr?: string; //设备状态中文说明
  	//设备状态列表, 其中第一个就是设备的status与statusStr的值, 
  	//name参考常量文档中的bacPresentValue中的说明。
    statusList: Array<{ value: number, description: string, name: string }> = []; 

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

### 门禁开门

#### name
    'openDoor'

#### params
需要开门的设备数组, 以下只显示最必要的内容, 方便调用者在不方便提供其它内容时进行调用
```javascript
{
    Channels: [{                //设备通道号列表
        Id?: String; //通道号
    }],

    Datasource: String; //子系统名称,
    Raw: //保存着对应厂家系统回传的原始数据
}
```

#### 返回数据
没有返回值

### 门禁关门

#### name
    'closeDoor'

#### params
需要关门的设备数组, 以下只显示最必要的内容, 方便调用者在不方便提供其它内容时进行调用
```javascript
{
    channels: [{                //设备通道号列表
        id?: string; //通道号
    }],

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

#### 返回数据
没有返回值

### 门禁常开

#### name 
    'doorStayOpen'

#### params
需要常开的设备数组, 以下只显示最必要的内容, 方便调用者在不方便提供其它内容时进行调用
```javascript
{
    channels: [{                //设备通道号列表
        id?: string; //通道号
    }],

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

#### 返回数据
没有返回值

### 门禁常关

#### name
    'doorStayClose'

#### params
需要常关的设备数组, 以下只显示最必要的内容, 方便调用者在不方便提供其它内容时进行调用
```javascript
{
    channels: [{                //设备通道号列表
        id?: string; //通道号
    }],

    dataSource: string; //子系统名称,
    raw: {} //保存着对应厂家系统回传的原始数据
}
```

#### 返回数据
没有返回值

### 查询门禁刷卡记录

#### name
    'accessControlQuerySwipeCardRecord'

#### params
```javascript
{
    start: string; //查询的开始时间
    end: string; //查询结束时间
}
```

#### 返回数据
```javascript
{
    recordId?: number;  //记录ID
    cardNumber?: string;  //卡号
    cardStatus?: number;   //卡状态
    cardStatusStr?: string; //卡状态说明
    cardType?: number;     //卡类型
    cardTypeStr?: string; //卡类型说明

    channelId?: string;    //刷卡设备通道号
    channelName?: string;   //刷卡设备通道名称

    videoChannelId?: string;  //门禁对应的视频设备通道号
    videoChannelName?: string; //门禁对应的视频设备的通道名称

    deviceCode?: string;  //设备编码
    deviceName?: string;  //设备名称

    enterOrExit?:number; //刷卡是出还是入
    openResult?:boolean;   //开门结果
    openType?:number; //开门类型
    openTypeStr?: string; //开门类型说明

    personId?: number; //人员ID
    personName?:string; //人员名称
    personCode?: string;    //人员编号
    personImage?: string; //人员照片

    paperNumber?: string; //人员证件号码
    departmentName?: string; //部门名称

    time?: number;  //刷卡时间
    image?: string; //刷卡时抓拍图

    otherImages: Array<string> = [];

    dataSource: string; //子系统名称,
    raw: {} //保存着对应厂家系统回传的原始数据
}

```

### 查询门禁认证记录

#### name
    'accessControlQueryAuthorizeRecord'

#### params
```javascript
{
    start: string; //查询的开始时间
    end: string; //查询结束时间
}
```

#### 返回数据
```javascript
{
    recordId?: string;  //记录ID
    personName?: string; //人员名称
    age?: number;   //年龄
    address?: string;   //地址
    sex?: string;   //性别

    deviceName?: string;    //设备名称
    compareResult?: boolean; //认证结果
    time?: number;  //认证时间

    paperNumber?: string;   //证件号
    paperImage?: string;    //证件图
    snapImage?: string;     //认证时抓拍图

    dataSource: string; //子系统名称,
    raw: {}; //保存着对应厂家系统回传的原始数据
}
```


### 可视对讲开门
针对可视对讲设备的开门命令

#### name
    'openDoor'

#### params
需要开门的设备, 以下只显示最必要的内容, 方便调用者在不方便提供其它内容时进行调用
```javascript
{
    channels: [{                //设备通道号列表
        id?: string; //通道号
    }],

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

#### 返回数据
没有返回值

### 可视对讲设备报警记录

#### name
    'vimsQueryAlarmRecord'

#### params
```javascript
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```javascript
{
    recordId?: string;  //记录ID
    time?: number;  //报警时间
    grade?: number; //报警级别
    image?: string;   //报警图片

    status?: number; //报警状态
    type?: string; //报警类型
    callNumber?: string; //呼叫号码

    channelName?: string; //通道名称
    channelSeq?: number; //通道序号

    deviceCode?: string; //设备编码
    deviceName?: string; //设备名称

    handleStatus?: string; //处理状态

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

### 可视对讲设备开门记录

#### name
    'vimsQueryOpenDoorRecord'

#### params
```javascript
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```javascript
{
    recordId?: string; //记录ID
    cardNumber?: string; //卡号
    cardType?: number; //卡类型

    channelName?: string; //通道名称
    channelSeq?: number; //通道序号

    deviceCode?: string; //设备编码
    deviceName?: string; //设备名称

    openResult?: boolean; //开门结果
    openType?: number; //开门类型
    openTypStr?: string; //开门类型说明

    personId?: string; //刷卡人id
    personName?: string; //刷卡人名称

    time?: number; //刷卡时间
    
    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

### 报警历史记录查询

#### name
    'alarmQueryHistoryRecord'

#### params
```javascript
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```javascript
{    
    recordId?: string; //记录ID
    grade?: number; //报警级别

    time?: number; //报警时间
    image?: string; //报警图片
    status?: number; //报警状态

    type?: number; //报警类型
    typeStr?: string; //报警类型说明

    handleStatus?: number; //报警处理状态
    handleStatusStr?: string; //报警处理状态说明

    channelName?: string; //通道号
    deviceName?: string; //设备名

    unitType?: number; //设备单元类型
}
```

### 人脸检测记录查询

#### name
    'faceDetectionHistoryRecord'

#### params
```javascript
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```javascript
{
    recordId?:string; //记录ID
    time?: number; //记录时间
    channelId?: string;//通道号
    channelName?:string; //通道名
    deviceId?: string;//设备ID
    deviceName?: string;//设备名
    deviceCode?: string;//设备编号

    snapImage?: string; //人脸抓图
    sceneSnapImage?: string;//场景图片

    age?:number; //年龄
    sex?: string; //性别
    feature?: string; //特征值
    featureString?: string; //特征值

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

### 人脸识别记录

#### name
    'faceRecognitionRecord'

#### params
```javascript
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```javascript
{
    recordID?: string; //记录ID
    paperNumber?: string; //证件号
    paperType?: string;//证件类型

    channelId?: string; //通道号
    channelName?: string; //通道名称

    personName?:string; //姓名

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

    similarity?:number; //相似度
    featureString?: string; //特征值

    time?: number; //识别时间

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

### 人体特征记录

#### name
    'facePersonFeatureRecord',

#### params
```javascript
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```javascript
{
    recordId?: string; //记录ID
    image?: string; //人脸图片
    featureImages: Array<string> = []; //图片扩展

    time?: number; //识别时间

    deviceId?: string; //设备ID
    deviceName?:string; //设备名称
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
    age?:number; //年龄
    complexion?: string; //肤色
    eye?: string;   //眼睛状态
    mouth?: string; //嘴巴状态
    mask?: string;  //口罩状态
    beard?: string; //胡子状态
    featureString?: string; //特征值

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

### 车辆特征记录

#### name
    'carFeatureRecord'

#### params
```javascript
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```javascript
{
    recordId?: string; //记录ID

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

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

### 非机动车特征记录

#### name
    'nonmotorFeatureRecord'

#### params
```javascript
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```javascript
{
    recordId?: string; //记录ID

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
    age?:number; //年龄
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

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

### 以图搜图

#### name
    'faceSearch'

#### params
```javascript
{
    image: string, //base64格式的图片,
    threshold: number, //期望的阈值, 推荐不传, 系统会用默认的,
    start: string; //开始时间,
    end: string; //结束时间
}
```

#### 返回数据
```javascript
{
    paperNumber?: string; //证件号

    personName?: string; //姓名
    personCode?: string; //人员编码
    departmentName?: string; //部门名称

    sex?: string; //性别
    nation?: string; //国籍
    bornYear?: string; //出生年月
    age?:number; //年龄
    glasses?: string; //眼镜
    fringe?: string; //刘海
    similarity?: number; //相似度

    channelId?: string;//通道号
    channelName?: string;//通道名

    groupId?:string; //图片库ID
    groupType?: string; //人脸库类型

    libImage?:string; //库中图片
    image?: string; //用于对比的人脸图片
    hitImage?: string;//命中的图片

    featureString?: string; //特征值

    time?: number; //识别时间

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

### 得到所有的会议室

    本命令不但返回会议系统中所有的会议室, 而且还返回会议室下现有的设备

#### name
    'getAllMeetingRoom'

#### params
    无需参数

#### 返回数据

其中devices的具体字段意思可参考[得到所有设备](#得到所有设备)

```javascript
{
    id?: number; //系统内部id
    name?: string; //会议室名称
    floor?: string; // 会议室所在楼层
    buildingName: string; //会议室所在建筑名称
    parkName: string: //会议室所在园区
    seats?: number;  //会议室座位数
    department?: string; //会议室所属部门
    openStart?: string; //开放时间
    openEnd?: string; //开放时间
    forbiddenStart?: string; //禁止使用时间
    forbiddenEnd?: string; //禁止使用时间

    devices: Array<Device> = [ 
        {
            deviceId,
            deviceName,
            deviceType,
            deviceTypeStr            
        }
    ]; 
}
```

### 得到会议信息

#### name
    'getMeetings'

#### params
```javascript
{
    start: string,//查询的开始时间, 可选, 如果不填则为当天
    end: string, //查询的结束时间, 可选, 如果不填则为开始时间之后的一年
}
```

#### 返回数据
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
    room?: MeetingRoom; //使用房间, 参考得到会议室返回的数据
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

#### 返回数据说明

status 会议状态内容为: 
```javascript
    meetingStatus: {
        "1": "会议未开始",
        "2": "会议已取消",
        "3": "会议进行中",
        "4": "会议已结束",
        "5": "会议已结束",
    }
```

### 开灯
#### name
    'turnOnLight'
#### params
```javascript
[
    device: Device, //灯光设备数组
]
```
#### 返回数据
    没有返回值

### 关灯
#### name
    'turnOffLight'
#### params
```javascript
[
    device: Device, //灯光设备数组
]
```
#### 返回数据
    没有返回值


### 得到智能楼宇的当前值

#### name
    'getAllBACPresentValues'

#### params
    没有参数

#### 返回数据
```javascript
{
    deviceId?: string; //设备ID
    value?: any;    //当前值
    name?: string;  //值名称
    description?: string;   //说明 
    time: number; //生成值的时间
}
```

### 打开窗帘
#### name
    ‘openCurtain'
#### params
```javascript
[
    device: Device, //窗帘设备数组
]
```
#### 返回数据
    没有返回值

### 关闭窗帘
#### name
    ‘closeCurtain’
#### params
```javascript
[
    device: Device, //窗帘设备数组
]
```
#### 返回数据
    没有返回值

### 得到消费流水
#### name
    'getConsumeTurnover'
#### params
```javascript
{
    start: string,//查询的开始时间, 可选, 如果不填则为当天之前一年
    end: string, //查询的结束时间, 可选, 如果不填则为当天之后的一年
}
```
#### 返回数据
```javascript
    {
        serialNumber?: string; //流水号

        cardNumber?: string; //交易卡号
        personName?: string; //姓名
        personDepartment?: string; //人员所在部门

        dealerID?: string; //商户号
        dealerName?: string; //商户名称

        terminalID?: string; //交易终端号

        dealType?: number; //交易类型 1: '消费', 2: '充值', 3: '补助',
        dealTypeStr?: string; //交易类型名称

        paid?: number; //交易金额    

        time?: number; //交易时间
        bookTime?: number; //入账时间
    }
```

### 得到访客列表
#### name
getVisitorRecords
#### params
没有参数
#### 返回数据
```javascript
    {
        id?: string; //记录id
        personName?: string; //访客名称
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

### 得到访客刷卡记录
#### name
getVisitorSwipeCardRecords
#### params
```javascript
{
    start: string; //查询开始时间, 可选, 如果不填则为当天
    end: string; //结束时间, 可选, 如果不填则为当天
}
```
#### 返回数据
```javascript
    {
    cardNumber?: string;  //卡号
    cardStatus?: number;   //卡状态
    cardStatusStr?: string; //卡状态说明
    cardType?: number;     //卡类型
    cardTypeStr?: string; //卡类型说明

    channelId?: string;    //刷卡设备通道号
    channelName?: string;   //刷卡设备通道名称

    deviceCode?: string;  //设备编码
    deviceName?: string;  //设备名称

    personName?: string; // 访客姓名, 通过访客姓名, 用户可以与访客列表中的访客数据进行比对.

    enterOrExit?: number; //刷卡是出还是入, 1: 进门, 2:出门
    openResult?: boolean;   //开门结果
    openType?: number; //开门类型
    openTypeStr?: string; //开门类型说明

    time?: number;  //刷卡时间
    }
```

### 得到客流统计区域
#### name
getPassengerFlowRegions
#### params
没有参数
#### 返回数据
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
      
        sourceDeviceCode?: string; //区域人流数据来源设备编码
    }
```

### 控制云台
#### name

tripodheadControl
#### params
//其中需要控制的摄像头设备, 只显示最必要的内容, 方便调用者在不方便提供其它内容时进行调用
```javascript
{
    command: string; //云台控制命令, 参考常量文档
    footstep: number; //云台步长, 可选
    //需要控制的摄像头设备, 这里的数据说明为简化形式
    device: {
      	deviceId: string;  //设备ID
        deviceCode: string; //设备编码
        channels: [{               //设备通道号列表
            id?: string; //通道号
        }],

        dataSource: string; //子系统名称,
        raw: //保存着对应厂家系统回传的原始数据; 
        sdk: //保存着厂家信息
    }
}
```
#### 返回数据
没有返回数据

### 控制镜头
#### name
lensOperation
#### params
//其中需要控制的摄像头设备, 只显示最必要的内容, 方便调用者在不方便提供其它内容时进行调用
```javascript
{
    command: string; //镜头控制命令, 参考常量文档
    footstep: number; //云台步长, 可选
    //需要控制的摄像头设备, 这里的数据说明为简化形式
    device: {
       	deviceId: string;  //设备ID
        deviceCode: string; //设备编码
        channels: [{               //设备通道号列表
            id?: string; //通道号
        }],

        dataSource: string; //子系统名称,
        raw: //保存着对应厂家系统回传的原始数据; 
        sdk: //保存着厂家信息
    }
}
```
#### 返回数据
没有返回数据

### 云台快速定位
根据给出的x, y, z坐标轴快速将云台转向某个方向, 并放大或缩小
#### name
tripodheadLocate
#### params
```javascript
{
    x: number; 
    y: number;
    z: number;
    //需要控制的摄像头设备, 这里的数据说明为简化形式
    device: {
       	deviceId: string;  //设备ID
        deviceCode: string; //设备编码
        channels: [{               //设备通道号列表
            id?: string; //通道号
        }],

        dataSource: string; //子系统名称,
        raw: //保存着对应厂家系统回传的原始数据; 
        sdk: //保存着厂家信息
    }
}
```
#### 返回数据
没有返回数据

### 锁定云台
#### name
tripodheadLock
#### params
```javascript
{
    lock: boolean; //是否锁定
    //需要控制的摄像头设备, 这里的数据说明为简化形式
    device: {
       	deviceId: string;  //设备ID
        deviceCode: string; //设备编码
        channels: [{               //设备通道号列表
            id?: string; //通道号
        }],

        dataSource: string; //子系统名称,
        raw: //保存着对应厂家系统回传的原始数据; 
        sdk: //保存着厂家信息
    }
}
```
#### 返回数据
没有返回数据

### 云台灯光控制
#### name
tripodheadLight
#### params
```javascript
{
    open: boolean; //是否打开
    //需要控制的摄像头设备, 这里的数据说明为简化形式
    device: {
       	deviceId: string;  //设备ID
        deviceCode: string; //设备编码
        channels: [{               //设备通道号列表
            id?: string; //通道号
        }],

        dataSource: string; //子系统名称,
        raw: //保存着对应厂家系统回传的原始数据; 
        sdk: //保存着厂家信息
    }
}
```
#### 返回数据
没有返回数据

### 云台雨刷控制
#### name
tripodheadRainBrush
#### params
```javascript
{
    open: boolean; //是否打开
    //需要控制的摄像头设备, 这里的数据说明为简化形式
    device: {
       	deviceId: string;  //设备ID
        deviceCode: string; //设备编码
        channels: [{               //设备通道号列表
            id?: string; //通道号
        }],

        dataSource: string; //子系统名称,
        raw: //保存着对应厂家系统回传的原始数据; 
        sdk: //保存着厂家信息
    }
}
```
#### 返回数据
没有返回数据

### 相机红外控制
#### name

camearInfrared
#### params
```javascript
{
    open: boolean; //是否打开
    //需要控制的摄像头设备, 这里的数据说明为简化形式
    device: {
       	deviceId: string;  //设备ID
        deviceCode: string; //设备编码
        channels: [{               //设备通道号列表
            id?: string; //通道号
        }],

        dataSource: string; //子系统名称,
        raw: //保存着对应厂家系统回传的原始数据; 
        sdk: //保存着厂家信息
    }
}
```
#### 返回数据
没有返回数据

# 调试用接口

本章节下的接口用于调试使用

## 得到所有设备

url: /command/getAllDevices

method: GET

## 得到组织机构树

url: /command/getDGroupInfoXML

method: GET

## 得到日志文件

url: /log/:hostname/:time

method: GET

hostname: 子系统名称如：dh-h8900, dh-dpsdk 等

time：需要得到的日志日期，格式为 YYYYMMDD，如 20201120

### 得到设备流地址

url: /video/:hostname/:deviceId/:channelId/:isMain

method: GET

hostname: 子系统名称如：dh-h8900, hk-openapi等

isMain: 是否为主流, 1为是, 0为辅流

示例: /video/hk-openapi/ef8bf8bd36ab472c8bfae0c7dd99c17a/1/1, 表示得到 hk-openapi 下的设备id为ef8bf8bd36ab472c8bfae0c7dd99c17a的主流




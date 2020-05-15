[TOC]

# 命令接口

## 调用方法
用户通过命令接口向数据采集平台发送操作命令, 采集平台运行后返回结果.

#### Request
- Method: **POST**
- URL: ```http://ip:port/command```
- Headers: Content-Type: application/json
- Body: 
```json
    {
        id: string, //命令的唯一ID, 由调用者生成, 用于区别每次请求的命令
        name: string, //命令名, 本次需要执行的命令名称
        param: any, //本次命令的参数, 根据不同的命令, 需要提供的参数不同
    }
```

#### Response
- Body: 

```json
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
5. 除了**得到监控视频地址**之外的所有返回值都有 sdk 这个属性, 其内部结构为
```json
{
    manufacturer: 'dahua', //厂商名称, 表明数据提供厂商, 现有'dahua'
    platform: 'h8900', //厂商SDK的名称
}
```

### 得到实时监控视频地址

#### name
    'getRealVideoSource'

#### params
需要得到视频地址的设备列表, 下面只列出必要的参数
```json
{
    mainStream: boolean; //是否取主流, 如果为false, 或者为空, 则取副流
    type: 'rtsp'; //支持rtsp和hls两种格式, 默认是rtsp
    devices: [{
        channels: [{                //设备通道号列表
            id?: string; //通道号
        }],

        dataSource: string; //子系统名称,
        raw: //保存着对应厂家系统回传的原始数据
    }],
}
```

#### 返回数据
```json
{
    channelId: string; //通道号
    source: string; //视频流地址
    
    dataSource: string; //子系统名称
}
```

### 得到所有设备

#### name
    'getAllDevices'

#### params
    无需参数

#### 返回数据
会返回得到的所有设备的数组
```json
{
    deviceId?: String; //设备ID,
    deviceName?: String; //设备名称, 
    deviceCode?: String; //设备编码, 
    deviceIp?: String; //设备IP,
    deviceCategory?: number; ///设备大类, 现在先用大华的, 
    deviceCategoryStr?: string; //设备大类中文名
    deviceType?: number; //设备类型, 大华的, 
    deviceTypeStr?: string; //设备类型中文名
    deviceUnitType?: number; //设备单元类型, 不一定有
    deviceUnitTypeStr?: string; //设备单元类型中文名
    isDeviceOnline?: boolean; //设备在线状态
    channels: [{                //设备通道号列表
        id?: string; //通道号
        name?: string; //通道名称
        seq?: number; //通道序列号
        unitType?: number; //通道对应的设备单元类型
        sn?: string; //通道对应设备的SN号
    }],
    orgCode?: string; //设备组织编码, 不一定有,也不一定有用
    sn?: string; //设备sn号, 不一定有, 也不一定有用
    status?: number; //设备状态, 不一定有, 也不一有用

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

### 门禁开门

#### name
    'accessControlOpenDoor'

#### params
需要开门的设备数组, 以下只显示最必要的内容, 方便调用者在不方便提供其它内容时进行调用
```json
[{
    channels: [{                //设备通道号列表
        id?: string; //通道号
    }],

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}]
```

#### 返回数据
没有返回值

### 门禁关门

#### name
    'accessControlCloseDoor'

#### params
需要关门的设备数组, 以下只显示最必要的内容, 方便调用者在不方便提供其它内容时进行调用
```json
[{
    channels: [{                //设备通道号列表
        id?: string; //通道号
    }],

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}]
```

#### 返回数据
没有返回值

### 门禁常开

#### name 
    'accessControlStayOpen'

#### params
需要常开的设备数组, 以下只显示最必要的内容, 方便调用者在不方便提供其它内容时进行调用
```json
[{
    channels: [{                //设备通道号列表
        id?: string; //通道号
    }],

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}]
```

#### 返回数据
没有返回值

### 门禁常关

#### name
    'accessControlStayClose'

#### params
需要常关的设备数组, 以下只显示最必要的内容, 方便调用者在不方便提供其它内容时进行调用
```json
[{
    channels: [{                //设备通道号列表
        id?: string; //通道号
    }],

    dataSource: string; //子系统名称,
    raw: {} //保存着对应厂家系统回传的原始数据
}]
```

#### 返回数据
没有返回值

### 查询门禁刷卡记录

#### name
    'accessControlQuerySwipeCardRecord'

#### params
```json
{
    start: string; //查询的开始时间
    end: string; //查询结束时间
}
```

#### 返回数据
```json
{
    recordId?: number;  //设备ID
    cardNumber?: string;  //卡号
    cardStatus?: number;   //卡状态
    cardType?: string;     //卡类型

    channelId?: string;    //刷卡设备通道号
    channelName?: string;   //刷卡设备通道名称

    videoChannelId?: string;  //门禁对应的视频设备通道号
    videoChannelName?: string; //门禁对应的视频设备的通道名称

    deviceCode?: string;  //设备编码
    deviceName?: string;  //设备名称

    enterOrExit?:number; //刷卡是出还是入
    openResult?:boolean;   //开门结果
    openType?:string; //开门类型

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
```json
{
    start: string; //查询的开始时间
    end: string; //查询结束时间
}
```

#### 返回数据
```json
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
    'vimsOpenDoor'

#### params
需要开门的设备, 以下只显示最必要的内容, 方便调用者在不方便提供其它内容时进行调用
```json
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
```json
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```json
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
```json
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```json
{
    recordId?: string; //记录ID
    cardNumber?: string; //卡号
    cardType?: number; //卡类型

    channelName?: string; //通道名称
    channelSeq?: number; //通道序号

    deviceCode?: string; //设备编码
    deviceName?: string; //设备名称

    openResult?: boolean; //开门结果
    openType?: string; //开门类型

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
```json
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```json
{    
    recordId?: string; //记录ID
    grade?: number; //报警级别
    time?: number; //报警时间
    image?: string; //报警图片
    status?: number; //报警状态
    type?: string; //报警类型
    channelName?: string; //通道号
    deviceName?: string; //设备名

    unitType?: number; //设备单元类型

    dataSource: string; //子系统名称,
    raw: //保存着对应厂家系统回传的原始数据
}
```

### 人脸检测记录查询

#### name
    'faceDetectionHistoryRecord'

#### params
```json
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```json
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
```json
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```json
{
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

    groupId?: string; //人脸库ID
    groupName?: string; //人脸库名称

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
```json
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```json
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
```json
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```json
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
```json
{
    start: string; //开始时间
    end: string; //结束时间
}
```

#### 返回数据
```json
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
```json
{
    image: string, //base64格式的图片,
    threshold: number, //期望的阈值, 推荐不传, 系统会用默认的,
    start: string; //开始时间,
    end: string; //结束时间
}
```

#### 返回数据
```json
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

```json
{
    id?: number; //系统内部id
    name?: string; //会议室名称
    location?: string; //会议室地址
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
```json
{
    start: ‘2020-05-14’,//查询的开始时间, 可选, 如果不填则为当天
    end: '2020-05-14', //查询的结束时间, 可选, 如果不填则为开始时间之后的一年
}
```

#### 返回数据
```json
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
    room?: MeetingRoom; //使用房间
    status?: number; //状态
    statusStr?: string; //状态文字
    checkinList: Array<MeetingCheckinData> = [{ //会议签到情况
        meetingId?: number; //会议id
        name?: string; //签到人名称
        avatar?: string; //头像
        checkinTime?: number; //签到时间
    }]; 
}
```
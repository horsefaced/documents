# 常量的说明

## 设备大类(deviceCategory)和类型(deviceType)
### 会议系统
#### itc会议系统
itc会议系统的设备的大类与类型是一样的
```javascript
    [{
        "id": "1",
        "name": "温控器"
    },
    {
        "id": "2",
        "name": "灯光"
    },
    {
        "id": "3",
        "name": "音响"
    },
    {
        "id": "4",
        "name": "智能插座"
    },
    {
        "id": "5",
        "name": "电视机"
    },
    {
        "id": "6",
        "name": "空调"
    },
    {
        "id": "7",
        "name": "垂直帘"
    },
    {
        "id": "8",
        "name": "幕布"
    },
    {
        "id": "9",
        "name": "百叶窗"
    },
    {
        "id": "10",
        "name": "开合帘"
    },
    {
        "id": "11",
        "name": "话筒"
    },
    {
        "id": "12",
        "name": "线路"
    },
    {
        "id": "13",
        "name": "矩阵"
    },
    {
        "id": "14",
        "name": "门口屏"
    },
    {
        "id": "15",
        "name": "无纸化"
    },
    {
        "id": "16",
        "name": "摄像头"
    },
    {
        "id": "17",
        "name": "人脸识别"
    },
    {
        "id": "18",
        "name": "指纹识别"
    },
    {
        "id": "19",
        "name": "手机"
    }]
```

### 智能窗帘
#### lifesmart系统
##### 设备大类(deviceCategory)
其deviceCategory就是下面数组的序号
```javascript
    [
        '插座',
        '开关',
        '窗帘控制',
        '灯光',
        '超级碗',
        '感应器',
        '温控器',
        '⻔锁',
        '摄像头',
        '其它',
    ]
```
##### 设备类型(deviceType)
其deviceType为对象的字段名称, description为deviceTypeStr 
```javascript
    {
    'SL_OL': { description: '智慧插座', category: '插座', },
    'SL_OL_3C': { description: '智慧插座', category: '插座', },
    'SL_OL_DE': { description: '德标插座', category: '插座', },
    'SL_OL_UK': { description: '英标插座', category: '插座', },
    'SL_OL_UL': { description: '美标插座', category: '插座', },
    'OD_WE_OT1': { description: 'Wi-Fi插座', category: '插座', },
    'SL_OL_W': { description: '入墙插座', category: '插座', },
    'SL_OE_3C': { description: '计量插座', category: '插座', },
    'SL_OE_DE': { description: '计量插座德标', category: '插座', },
    'SL_SW_IF1': { description: '流光开关一键', category: '开关', },
    'SL_SW_IF2': { description: '流光开关二键', category: '开关', },
    'SL_SW_IF3': { description: '流光开关三键', category: '开关', },
    'SL_SF_IF1': { description: '单火流光开关一键', category: '开关', },
    'SL_SF_IF2': { description: '单火流光开关二键', category: '开关', },
    'SL_SF_IF3': { description: '单火流光开关三键', category: '开关', },
    'SL_SW_CP1': { description: '橙朴流光开关一键', category: '开关', },
    'SL_SW_CP2': { description: '橙朴流光开关二键', category: '开关', },
    'SL_SW_CP3': { description: '橙朴流光开关三键', category: '开关', },
    'SL_SW_FE1': { description: '塞纳/格致开关一键', category: '开关', },
    'SL_SW_FE2': { description: '塞纳/格致开关二键', category: '开关', },
    'SL_SW_RC': { description: '触摸开关', category: '开关', },
    'SL_SF_RC': { description: '单火触摸开关', category: '开关', },
    'SL_SW_RC1': { description: '白玉/墨玉流光开关一键', category: '开关', },
    'SL_SW_RC2': { description: '白玉/墨玉流光开关二键', category: '开关', },
    'SL_SW_RC3': { description: '白玉/墨玉流光开关三键', category: '开关', },
    'SL_SW_ND1': { description: '恒星/辰星开关一键', category: '开关', },
    'SL_SW_ND2': { description: '恒星/辰星开关二建', category: '开关', },
    'SL_SW_ND3': { description: '恒星/辰星开关三键', category: '开关', },
    'SL_MC_ND1': { description: '恒星/辰星开关伴侣一键', category: '开关', },
    'SL_MC_ND2': { description: '恒星/辰星开关伴侣二键', category: '开关', },
    'SL_MC_ND3': { description: '恒星/辰星开关伴侣三键', category: '开关', },
    'SL_S': { description: '开关智控器', category: '开关', },
    'SL_SPWM': { description: '可调亮度开关智控器', category: '开关', },
    'SL_SC_BB': { description: '随心开关', category: '开关', },
    'SL_P_SW': { description: '九路开关控制器', category: '开关', },
    'SL_SW_MJ1': { description: '奇点开关模块一键', category: '开关', },
    'SL_SW_MJ2': { description: '奇点开关模块二键', category: '开关', },
    'SL_SW_MJ3': { description: '奇点开关模块三键', category: '开关', },
    'SL_CN_IF': { description: '流光窗帘控制器', category: '窗帘控制', },
    'SL_CN_FE': { description: '格致/塞纳三键窗帘', category: '窗帘控制', },
    'SL_SW_WIN': { description: '窗帘控制器', category: '窗帘控制', },
    'SL_DOOYA': { description: '窗帘(杜亚)', category: '窗帘控制', },
    'SL_P_V2': { description: '智界窗帘电机智控器', category: '窗帘控制', },
    'SL_LI_RGBW': { description: '胶囊灯泡', category: '灯光', },
    'SL_CT_RGBW': { description: '幻彩灯带', category: '灯光', },
    'SL_SC_RGB': { description: '幻彩灯带（不带白光）', category: '灯光', },
    'OD_WE_QUAN': { description: '量子灯', category: '灯光', },
    'SL_LI_WW': { description: '白光智能灯泡', category: '灯光', },
    'SL_LI_GD1': { description: '调光壁灯', category: '灯光', },
    'SL_LI_UG1': { description: '花园地灯', category: '灯光', },
    'MSL_IRCTL': { description: '超级碗（基础版,蓝牙版）', category: '超级碗', },
    'OD_WE_IRCTL': { description: '超级碗（闪联版）', category: '超级碗', },
    'SL_SPOT': { description: '超级碗（CoSS版）', category: '超级碗', },
    'SL_P_IR': { description: '红外模块', category: '超级碗', },
    'SL_SC_G': { description: '⻔禁感应器', category: '感应器', },
    'SL_SC_BG': { description: '多功能(CUBE)⻔禁感应器', category: '感应器', },
    'SL_SC_MHW': { description: '动态感应器', category: '感应器', },
    'SL_SC_CM': { description: '动态感应器（7号电池版）', category: '感应器', },
    'SL_SC_BM': { description: '多功能(CUBE)动态感应器', category: '感应器', },
    'SL_P_RM': { description: '人体存在感应器', category: '感应器', },
    'SL_SC_THL': { description: '环境感应器', category: '感应器', },
    'SL_SC_BE': { description: '多功能(CUBE)环境感应器', category: '感应器', },
    'SL_SC_CQ': { description: '环境感应器(CO2+TVOC)', category: '感应器', },
    'SL_SC_CA': { description: '环境感应器(CO2)', category: '感应器', },
    'SL_SC_WA': { description: '水浸感应器', category: '感应器', },
    'SL_SC_CH': { description: '气体感应器(甲醛)', category: '感应器', },
    'SL_SC_CP': { description: '气体感应器(燃气)', category: '感应器', },
    'ELIQ_EM': { description: 'ELIQ电量计量器', category: '感应器', },
    'SL_SC_CV': { description: '语音小Q', category: '感应器', },
    'SL_P_A': { description: '烟雾感应器', category: '感应器', },
    'V_AIR_P': { description: '智控器空调面板', category: '温控器', },
    'SL_CP_DN': { description: '地暖温控器', category: '温控器', },
    'SL_CP_AIR': { description: '⻛机盘管', category: '温控器', },
    'SL_TR_ACIPM': { description: '新⻛系统', category: '温控器', },
    'SL_CP_VL': { description: '温控阀⻔', category: '温控器', },
    'SL_LK_LS': { description: '智能⻔锁', category: '⻔锁', },
    'SL_LK_GTM': { description: '智能⻔锁 耶鲁⻔锁', category: '⻔锁', },
    'SL_LK_AG': { description: '智能⻔锁 ⻄勒奇锁模块', category: '⻔锁', },
    'OD_JIUWANLI_LOCK1': { description: '九万里⻔锁', category: '⻔锁', },
    'SL_P_BDLK': { description: '必达⻔锁模块', category: '⻔锁', },
    'SL_LK_SG': { description: '思哥智能⻔锁', category: '⻔锁', },
    'SL_LK_YL': { description: 'Yale/Gateman⻔锁模块', category: '⻔锁', },
    'LSI_CAM_GOS1': { description: '高清摄像头', category: '摄像头', },
    'LSI_CAM_EZ1': { description: '户外摄像头', category: '摄像头', },
    'SL_CAM': { description: 'FRAME摄像头', category: '摄像头', },
    'SL_P': { description: '通用控制器', category: '其它', },
    'OD_MFRESH_M8088': { description: '空气净化器', category: '其它', },
    'LSSSMINIV1': { description: '多功能报警器', category: '其它', },
    'SL_ETDOOR': { description: '⻋库⻔', category: '其它', },
    'SL_ALM': { description: '智能报警器(CoSS版)', category: '其它', },
    }
```

### H8900
H8900系统包括了安防、人脸、门禁、考勤、停车等等系统
#### 设备大类
```javascript
 {
    1: '编码器',
    2: '解码器',
    3: '报警主机',
    4: '大屏',
    5: '卡口设备',
    6: '矩阵设备',
    7: '智能设备',
    8: '门禁设备',
    9: '动环设备',
    11: '转码器',
    14: '道闸设备',
    16: 'LED设备',
    21: '可视对讲设备',
}
```
#### 设备类型
第一层是设备类型所属的大类, 第二层是设备类型及说明
```javascript
{
    1: {
        1: 'DVR',
        2: 'IPC',
        3: 'NVS',
        5: 'MDVR',
        6: 'NVR',
        9: 'MPT',
        10: 'EVS',
        12: 'Smart IPC',
        14: 'Smart NVR',
        21: 'VTT',
        25: 'VTA',
        26: 'TPC',
        39: 'PSD',
    },
    2: {
        1: 'NVD',
        2: 'SVDS',
        5: 'UDS',
    },
    5: {
        1: '卡口设备',
        2: '测速设备',
        3: '闯红灯设备',
        4: '一体化设备',
        5: '智能识别设备',
        6: '违停检测设备',
        7: '违停检测设备',
        8: '车位探测设备',
        11: '超声波车位探测管理器',
        12: '人脸抓拍设备',
        14: '停车场区域抓拍设备',
    },
    7: {
        1: 'ISD',
        2: 'IVS-IP/IVS-B',
        4: 'IVS-F(人脸识别)',
        5: 'IVS-PC',
        6: 'IVS-M/J',
        7: 'IVS-PC盒子',
        8: 'IVS-B盒子',
        9: 'IVS-M盒子',
        15: 'IVSS',
        16: '8249人脸相机',
        17: 'AI-NVR',
        18: 'IVS-F(人脸检测)',
        20: 'SDT5A',
        22: 'HFS',
        28: 'AI鱼眼',
    },
    11: {
        1: 'TCS',
    },
    8: {
        1: 'DH-ASC1201A',
        2: 'DH-BSC1202B',
        3: 'DH-BSC1202C',
        4: 'DH-ASI1212A',
        5: 'DH-ASC1204B',
        6: 'DH-ASC1204C',
        7: 'VTA',
        8: 'RFID有源',
        14: 'VTO9241d人脸录入设备',
        15: 'ASH3001',
        16: '人脸识别闸机',
        17: 'DH-ASI4214F',
        18: '二代RFID设备',
        19: 'IVSS人脸提取设备',
        20: '第三方门禁设备',
        21: '门禁集中控制器',
        22: '人脸门禁',
        24: '安全帽人脸识别闸机',
        25: '围墙机',
    },
    21: {
        2: '数字门口机',
        3: '数字室内机',
        4: '模拟室内机',
        5: '围墙机',
        6: '室内机（支持门锁）',
        7: '半数字门口机',
        8: '管理机',
        9: '单元联网控制器',
        11: '数字门口机(白光)',
        12: '数字门口机(红外)',
        14: '围墙机(红外)',
        15: '围墙机(白光)',
        17: '虚拟室内机',
    },
}
```

### 人脸库类型
```javascript
{
    1: '白名单',
    2: '黑名单',
    3: '内部库',
    4: '访客库',
}
```

### 消防设备类型
```javascript
{
    0: '通用',
    1: '火灾报警控制器',
    2: '预留',
    3: '预留',
    4: '预留',
    5: '预留',
    6: '预留',
    7: '预留',
    8: '预留',
    9: '预留',
    10: '可燃气体探测器',
    11: '点型可燃气体探测器',
    12: '独立式可燃气体探测器',
    13: '线型可燃气体探测器',
    14: '预留',
    15: '预留',
    16: '电气火灾监控报警器',
    17: '剩余电流式电气火灾监控探测器',
    18: '测温式电气火灾监控探测器',
    19: '预留',
    20: '预留',
    21: '探测回路',
    22: '火灾显示盘',
    23: '手动火灾报警按钮',
    24: '消火栓按钮',
    25: '火灾探测器',
    26: '预留',
    27: '预留',
    28: '预留',
    29: '预留',
    30: '感温火灾探测器',
    31: '点型感温火灾探测器',
    32: '点型感温火灾探测器（S型）',
    33: '点型感温火灾探测器（R型）',
    34: '线型感温火灾探测器',
    35: '线型感温火灾探测器（S型）',
    36: '线型感温火灾探测器（R型）',
    37: '光纤感温火灾探测器',
    38: '预留',
    39: '预留',
    40: '感烟火灾探测器',
    41: '点型离子感烟火灾探测器',
    42: '点型光电感烟火灾探测器',
    43: '线型光束感烟火灾探测器',
    44: '吸气式感烟火灾探测器',
    45: '预留',
    46: '预留',
    47: '预留',
    48: '预留',
    49: '预留',
    50: '复合式火灾探测器',
    51: '复合式感烟感温火灾探测器',
    52: '复合式感光感温火灾探测器',
    53: '复合式感光感烟火灾探测器',
    54: '预留',
    55: '预留',
    56: '预留',
    57: '预留',
    58: '预留',
    59: '预留',
    60: '预留',
    61: '紫外火焰探测器',
    62: '红外火焰探测器',
    63: '预留',
    64: '预留',
    65: '预留',
    66: '预留',
    67: '预留',
    68: '预留',
    69: '感光火灾探测器',
    70: '预留',
    71: '预留',
    72: '预留',
    73: '预留',
    74: '气体探测器',
    75: '预留',
    76: '预留',
    77: '预留',
    78: '图像摄像方式火灾探测器',
    79: '感声火灾探测器',
    80: '预留',
    81: '气体灭火控制器',
    82: '消防电气控制装置',
    83: '消防控制室图形显示装置',
    84: '模块',
    85: '输入模块',
    86: '输出模块',
    87: '输入/输出模块',
    88: '中继模块',
    89: '预留',
    90: '预留',
    91: '消防水泵',
    92: '消防水箱',
    93: '预留',
    94: '预留',
    95: '喷淋泵',
    96: '水流指示器',
    97: '信号阀',
    98: '报警阀',
    99: '压力开关',
    100: '预留',
    101: '阀驱动装置',
    102: '防火门',
    103: '防火阀',
    104: '通风空调',
    105: '泡沫液泵',
    106: '管网电磁阀',
    107: '预留',
    108: '预留',
    109: '预留',
    110: '预留',
    111: '防烟排烟风机',
    112: '预留',
}
```

### 消防设备状态
```javascript
{
    32768: '升级故障',
    16384: '传感器故障',
    8192: '预留',
    4096: '设备被拆',
    2048: '短路',
    1024: '开路',
    512: '失联',
    256: '电源故障',
    128: '延时',
    64: '反馈',
    32: '启动',
    16: '监管',
    8: '屏蔽',
    4: '故障',
    2: '火警',
    1: '测试',
    0: '正常',
}
```
 
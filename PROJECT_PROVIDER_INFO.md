# 项目与标识对应表

## 杭州招商银行

| 子系统                     | 对应厂家                                                     |
| -------------------------- | ------------------------------------------------------------ |
| 楼宇自动控制               | { sdk: { manufacturer: 'siemens', platform: 'bas-opc'}},     |
| 食堂管理系统               | { sdk: {manufacturer: 'zytk', platform: 'zytk'}}             |
| 一卡通系统-门禁            | { sdk: { manufacturer: 'dahua', platform: 'H8900' } },       |
| 一卡能系统-人脸识别        | { sdk: { manufacturer: 'dahua', platform: 'H8900' } },       |
| 视频监控系统               | { sdk: { manufacturer: 'dahua', platform: 'H8900' } },       |
| 火灾自动报警及联动控制系统 | { sdk: { manufacturer: 'dahua', platform: 'firefighting' }}  |
| 入侵报警系统               | { sdk: { manufacturer: 'dahua', platform: 'H8900' } },       |
| 背景音乐系统               | { sdk: { manufacturer: 'dahua', platform: 'firefighting' }}  |
| 电动窗帘控制系统           | { sdk: { manufacturer: 'lifesmart', platform: 'lgc'} },      |
| 会议管理系统               | { sdk: { manufacturer: 'itc', platform: 'cloud' } },         |
| 智能停车管理系统           | { sdk: { manufacturer: 'dahua', platform: 'H8900' } },       |
| 空气质量                   | {sdk: { manufacturer: 'zgkon', platform: 'environment-control-system' }} |
| 移动端-考勤                | { sdk: { manufacturer: 'cmb', platform: 'cloud' }}           |
| 移动端-员工消费记录        | { sdk: { manufacturer: 'cmb', platform: 'cloud' }}           |
| 移动端-会议议程            | { sdk: { manufacturer: 'cmb', platform: 'cloud' }}           |
| 移动端-今日菜品            | { sdk: { manufacturer: 'cmb', platform: 'cloud' }}           |
| 移动端-空气质量概况        | {sdk: {manufacturer: 'cmb', platform: 'cloud'}}              |

## 武汉昙华林

| 子系统         | 对应厂家                                                  |
| -------------- | --------------------------------------------------------- |
| 视频监控系统   | { sdk: { manufacturer: 'dahua', platform: 'H8900' } }     |
| 广播系统       | { sdk: { manufacturer: 'dsppa', platform: 'mag6180' }}    |
| 无线AP管理系统 | { sdk: { manufacturer: 'sangfor', platform: 'wac-snmp'}}  |
| 消防系统       | 暂无提供                                                  |
| 智能厕所系统   | { sdk: { manufacturer: 'topbeyond', platform: 'toilet'},} |
| 车辆管理       | 暂无提供                                                  |
| 门禁管理       | 暂无提供                                                  |
| 环境监测系统   | {sdk: { manufacturer: 'zillion', platform: 'ecs'}}        |

## 深圳龙华观澜学校

| 子系统       | 对应厂家                                            |
| ------------ | --------------------------------------------------- |
| 视频监控系统 | { sdk: { manufacturer: 'dahua', platform: 'u8000'}} |

## 山东千佛山医院

1. 门禁管理由两家提供, 分别是大华H8900-2平台与海康的 openapi平台, 其中 H8900-2 平台使用常量与H8900一致, 只为区分来自不同H8900服务器的设备之用.
2. 消防系统以报警主机形式接入H8900平台, 其deviceUnitType: 4, deviceType: 1, 发出的报警类型为: 82: 火警
3. 一键报警以报警主机形式接入H8900平台, 其deviceUnitType: 4, deviceType: 1,发现的报警类型为: 81: 报警主机报警

| 子系统       | 对应厂家                                                     |
| ------------ | ------------------------------------------------------------ |
| 视频监控系统 | { sdk: { manufacturer: 'dahua', platform: 'H8900' } }        |
| 门禁管理     | { sdk: { manufacturer: 'dahua', platform: 'H8900-2' } }, { sdk: {manufacturer: 'hikvision', platform: 'openapi'}} |
| 一键报警     | { sdk: { manufacturer: 'dahua', platform: 'H8900' } }        |
| 出入口管理   | 暂无提供                                                     |
| 消防水压监控 | 暂无提供                                                     |
| 消防系统     | { sdk: { manufacturer: 'dahua', platform: 'H8900' } }        |
| 人脸识别     | { sdk: { manufacturer: 'dahua', platform: 'H8900' } }        |
| 巡更系统     | { sdk: { manufacturer: 'dahua', platform: 'icc'}}            |

## 宁夏核废料项目

1. 周界报警系统中, 设备的解警类型为:deviceAlarm事件中:  "alarmType":255,"alarmTypeStr":"设备故障恢复", 周界设备收到这个就认为是恢复正常状态.

| 子系统       | 对应厂家                                                |
| ------------ | ------------------------------------------------------- |
| 视频监控系统 | { sdk: { manufacturer: 'dahua', platform: 'H8900' } }   |
| 周界报警     | { sdk: { manufacturer: 'innopro', platform: '8100' } }, |
| 声音复合系统 | { sdk: { manufacturer: 'asrc', platform: 'asrc' } }     |

## 上海电力大学项目



| 子系统       | 对应厂家                                              |
| ------------ | ----------------------------------------------------- |
| 视频监控系统 | { sdk: { manufacturer: 'dahua', platform: 'H8900' } } |
| 单兵指挥系统 | { sdk: { manufacturer: 'dahua', platform: 'x9000'}}   |


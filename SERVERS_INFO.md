# virupaksa现有服务信息

## artemis

使用端口：8161，61616

启动命令：docker run -d -p 61616:61616 -p 8161:8161 -v artemis:/var/lib/artemis/etc --name artemis --restart=always vromero/activemq-artemis

## Keepalived

启动命令: docker run --cap-add=NET_ADMIN --cap-add=NET_BROADCAST --cap-add=NET_RAW --net=host -d -v keepalived:/container/service/keepalived/assets/ --name keepalived --restart=always osixia/keepalived

## videoserver

使用端口：58080

启动命令：docker run -d -p 58080:8090 -v videoserver:/etc -v videoserver-assets:/opt/changer/server/videoserver/assets --name videoserver --restart=always videoserver:latest

## virupaksa

使用端口：12000

启动命令：docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name virupaksa --hostname virupaksa --restart=always virupaksa

## mongodb

启动命令: docker run -d --restart=always --network="host" -v mongo-data:/data/db --name mongo mongo

## dh-h8900-server

使用端口： 12010

启动命令：docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name dh-h8900-server --hostname dh-h8900 --restart=always dh-h8900-server

## lifesmart-tob-server

使用端口： 12020

## itc-server

使用端口：12030

启动命令: docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name itc-server --hostname itc-server  --restart=always itc-server:latest

## metasys-server

使用端口：12040

## zytk-server

使用端口：12050

启动命令: docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name zytk-server --hostname zytk  --restart=always zytk-server:latest

## dh-dpsdk-server

使用端口：12060

启动命令：docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name dh-dpsdk-server --hostname dh-dpsdk --restart=always dh-dpsdk-server

## dh-firefighting-server

使用端口：12070, 12071

启动命令: docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name dh-firefighting-server --hostname dh-firefighting  --restart=always dh-firefighting-server:latest

其它操作: 需要把各个项目自己的消防设备列表形成的csv文件拷贝至配置目录中

额外文件:

| rawData.csv | 设备列表 | 第一列名称, 第二列deviceCode,第三列th_position |
| ----------- | -------- | ---------------------------------------------- |
|             |          |                                                |



## innopro-8100-server

使用端口：12080

事件上报监听端口：12081

启动命令：docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name innopro-8100-server --hostname innopro-8100 --restart=always innopro-8100-server

## asrc-server

使用端口：12090

事件上报监听端口：12091

启动命令：docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name asrc-server --hostname asrc-server --restart=always asrc-server

## hk-openapi-server

使用端口：12100

启动命令：docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name hk-openapi-server --hostname  hk-openapi --restart=always  hk-openapi-server

## dh-x9000-server

使用端口：12110

启动命令：docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name dh-x9000-server --hostname dh-x9000 --restart=always dh-x9000-server

## lifesmart-lgc-server

使用端口: 12120

启动命令: docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name lifesmart-lgc-server --hostname lifesmart-lgc  --restart=always lifesmart-lgc-server:latest

## cmb-cloud-server

使用端口: 12130

启动命令: docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name cmb-cloud-server --hostname cmb-cloud --restart=always cmb-cloud-server

监听停车场: IP:12130/cmbparking

## dsppa-mag6180-server

使用端口: 12140

启动命令: docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name dsppa-mag6180-server --hostname dsppa-mag6180  --restart=always dsppa-mag6180-server:latest

## dh-netsdk-server

使用端口: 12150

## dh-u8000-server

使用端口: 12160

启动命令: sudo docker run -d --network="host" -v virupaksa:/etc  -v virupaksa:/var/log --name dh-u8000-server --hostname dh-u8000 --restart=always dh-u8000-server:latest

## siemens-bas-opc-server

使用端口: 12170

启动命令: sudo docker run -d --network="host" -v virupaksa:/etc  -v virupaksa:/var/log --name siemens-bas-opc-server --hostname siemens-bas-opc --restart=always siemens-bas-opc-server:latest

额外文件:

| data.json | 直接可以通过getAllDevices返回的格式设备列表 | 通过processData.js针对BA系统OPC点位表.csv生成 |
| --------- | ------------------------------------------- | --------------------------------------------- |
|           |                                             |                                               |



## sangfor-wac-snmp-server

使用端口: 12180

启动命令: sudo docker run -d --network="host" -v virupaksa:/etc  -v virupaksa:/var/log --name sangfor-wac-snmp-server --hostname sangfor-wac-snmp --restart=always sangfor-wac-snmp-server:latest

额外文件: 

| deviceNames.csv | 配置设备名 | 第一列为deviceCode, 第二列为设备名称 |
| --------------- | ---------- | ------------------------------------ |
|                 |            |                                      |

## topbeyond-toilet-server

使用端口: 12190

启动命令: docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name topbeyond-toilet-server --hostname topbeyond-toilet topbeyond-toilet-server:latest

## zgkon-ecs-server

使用端口: 12200

启动命令: docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name zgkon-ecs-server --hostname zgkon-ecs zgkon-ecs-server:latest

## zillion-ecs-server

使用端口: 12210

启动命令: docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name zillion-ecs-server --hostname zillion-ecs zillion-ecs-server:latest

## hk-netsdk-acs-server

使用端口: 12220

## dh-icc-server

使用端口: 12230

## virupaksa-mock

使用端口：12990

启动命令: docker run -d -p 12000:12990 -v virupaksa-mock:/etc -v virupaksa-mock:/var/log --name virupaksa-mock --hostname virupaksa-mock --restart=always virupaksa-mock


# virupaksa现有服务信息

## artemis

使用端口：8161，61616

启动命令：docker run -d -p 61616:61616 -p 8161:8161 -v artemis:/var/lib/artemis/etc --name artemis --restart=always vromero/activemq-artemis

## videoserver

使用端口：58080

启动命令：docker run -d --network="host" -v videoserver:/etc -v videoserver-assets:/opt/changer/server/videoserver/assets --name videoserver --restart=always videoserver:latest

## virupaksa

使用端口：12000

启动命令：docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name virupaksa --hostname virupaksa --restart=always virupaksa

## dh-h8900-server

使用端口： 12010

启动命令：docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name dh-h8900-server --hostname dh-h8900 --restart=always dh-h8900-server

## lifesmart-tob-server

使用端口： 12020

## itc-server

使用端口：12030

启动命令: docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name itc-server --hostname itc-server itc-server:latest

## metasys-server

使用端口：12040

## zytk-server

使用端口：12050

启动命令: docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name zytk-server --hostname zytk zytk-server:latest

## dh-dpsdk-server

使用端口：12060

启动命令：docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name dh-dpsdk-server --hostname dh-dpsdk --restart=always dh-dpsdk-server

## dh-firefighting-server

使用端口：12070

启动命令: docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name dh-firefighting --hostname dh-firefighting dh-firefighting-server:latest

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

启动命令: docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name lifesmart-lgc --hostname lifesmart-lgc lifesmart-lgc-server:latest

## cmb-cloud-server

使用端口: 12130

## dsppa-mag6180-server

使用端口: 12140

## dh-netsdk-server

使用端口: 12150

## dh-u8000-server

使用端口: 12160

启动命令: sudo docker run -d -p 12160:12160 -v virupaksa:/etc --name dh-u8000 --hostname dh-u8000 dh-u8000-server:latest

## virupaksa-mock

使用端口：12990


# virupaksa现有服务信息

## artemis

使用端口：8161，61616

启动命令：docker run -d -p 61616:61616 -p 8161:8161 -v artemis:/var/lib/artemis/etc --name artemis --restart=always vromero/activemq-artemis

## videoserver

使用端口：58080

启动命令：docker run -d -p 58080:8090 -v videoserver:/etc --name videoserver --restart=always videoserver:latest

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

## metasys-server

使用端口：12040

## zytk-server

使用端口：12050

## dh-dpsdk-server

使用端口：12060

启动命令：docker run -d --network="host" -v virupaksa:/etc -v virupaksa:/var/log --name dh-dpsdk-server --hostname dh-dpsdk --restart=always dh-dpsdk-server

## dh-firefighting-server

使用端口：12070

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

## virupaksa-mock

使用端口：12990


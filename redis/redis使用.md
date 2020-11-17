# windows使用docker

1. 下载安装docker，https://www.docker.com/
2. 启动docker，下载redis镜像,powershell运行命令
```shell 
    docker pull redis
```
3. 运行镜像并发布端口6379
```shell 
    docker run --name first-docker -p 6393:6393 -d redis
```
4. 运行redis-cli（这是Redis的一个命令行管理工具）
```shell
docker exec -it first-docker redis-cli
```

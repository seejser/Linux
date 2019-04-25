## run MongoDB by Docker

### 下载MongoDB的官方镜像

```
docker pull mongo:4

```

### 查看下载镜像

```
docker images

```

### 启动MongoDB服务器容器

```
docker run --name mymongo -v /mymongo/data/db -d mongo:4

--name mymongo #指导容器名称为mymongo

```

### 查看docker容器状态

```
docker ps

```
### 查看MongoDB日志

```
docker logs mymongo

```



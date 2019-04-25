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


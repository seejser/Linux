# 使用pm2自动化部署node项目的方法步骤


## [目标主机安装nvm](https://github.com/creationix/nvm)

```

curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash

command -v nvm


```


## 目标安装Nodejs

```
nvm ls 

nvm ls-remote

nvm run node --version


nvm alias default node


node -v


npm -v


```



## [目标主机安装yarn](https://yarnpkg.com/en/docs/install#centos-stable)

```
curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo

sudo yum install yarn


yarn --version
```


## Quick Start PM2

```

yarn global add pm2

pm2 completion install

pm2 ls



```


## 首次部署


```

pm2 deploy deploy.yaml production setup 

```


## 再次部署

 ```
 pm2 deploy deploy.yaml production upddate
 ```






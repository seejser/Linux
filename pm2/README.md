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
## 目标主机安装git

```
yum install git 

git --version
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
## 生成秘钥


```
ssh-keygen -t rsa -C "xxx@xxx.com"

cat ~/.ssh/id_rsa.pub

```

在https://gitee.com/xx/xx.git项目的设置中填写Deploy keys setting


## 首次部署


```

pm2 deploy deploy.yaml production setup 



```

注意：fatal: could not read Username for 'https://gitee.com': No such device or address

把deploy.yaml的repo修改为：

```
https://[Username]:[password]@gitee.com/xx/xxx.git 
```


## 再次部署

 ```
 pm2 deploy deploy.yaml production upddate
 ```






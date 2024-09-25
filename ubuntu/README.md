# init ubuntu 

## nodejs
### nvm
[nvm](https://github.com/nvm-sh/nvm)

#### nodejs源
nvm安装node默认使用node官方仓库https://nodejs.org/dist，安装受阻的话可以通过设置NVM_NODEJS_ORG_MIRROR环境变量使用国内镜像源安装

export NVM_NODEJS_ORG_MIRROR=https://mirrors.aliyun.com/nodejs-release

#### nvm ls-remote

#### nvm install 18

### npm

 npm config set registry http://registry.npmmirror.com

http://npm.taobao.org => http://npmmirror.com
http://registry.npm.taobao.org => http://registry.npmmirror.com


### yarn
npm install --global yarn

### pm2
[ pm2](https://pm2.keymetrics.io/)
npm install pm2 -g

### pnmp
[pnpm](https://www.pnpm.cn/installation)
npm install -g pnpm



## docker
参考资料：https://blog.csdn.net/magic_ll/article/details/139985543
1. 安装一些依赖
sudo apt update
sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common -y

2. 添加docker官网 GPG 密钥、设置stable 仓库
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
3. 安装 Docker

sudo apt-get update
sudo apt install docker-ce docker-ce-cli containerd.io

测试：docker --version
sudo systemctl status docker
4. 设置开机启动：sudo systemctl enable docker

5. 阿里云镜像加速器的配置
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://txy2j5mb.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker

## nginx

1. apt install nginx
2. ningx -t
3. sudo systemctl enable nginx
4. 




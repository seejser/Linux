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
6. 通过access token登录docker hub
[access token]()
docker login -u hooperhu
dckr_XXXX

7. 解决docker问题
   sudo vim /etc/resolv.conf
nameserver 8.8.8.8
nameserver 8.8.4.4
nameserver 1.1.1.1
nameserver 114.114.114.114
vim /etc/docker/daemon.json
{
     "max-concurrent-downloads": 10,
     "max-concurrent-uploads": 5,
     "default-shm-size": "1G",
     "debug": true,
     "experimental": false,
     "registry-mirrors":[
                "https://x9r52uz5.mirror.aliyuncs.com",
                "https://dockerhub.icu",
                "https://docker.chenby.cn",
                "https://docker.1panel.live",
                "https://docker.awsl9527.cn",
                "https://docker.anyhub.us.kg",
                "http://hub-mirror.c.163.com",
                "https://docker.mirrors.ustc.edu.cn",
                "https://dhub.kubesre.xyz"
        ]
}


## nginx

1. apt install nginx
2. ningx -t
3. sudo systemctl enable nginx
### ssl
要使用 `Certbot` 在 Nginx 上配置 SSL 证书，你可以按照以下步骤操作：

### 1. 安装 Certbot 和 Nginx 插件
首先，确保你已安装了 Certbot 和 Nginx 插件。如果未安装，可以使用以下命令：

```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx
```

### 2. 配置 Nginx
确保你的 Nginx 配置文件中正确设置了域名和服务器块。你可以通过修改 `/etc/nginx/sites-available/` 中的文件来做到这一点。示例配置：

```nginx
server {
    listen 80;
    server_name example.com www.example.com;

    location / {
        proxy_pass http://localhost:3000;  # 如果你有反向代理服务
    }
}
```

保存并关闭文件后，使用以下命令检查配置是否正确：

```bash
sudo nginx -t
```

如果配置正确，重新加载 Nginx：

```bash
sudo systemctl reload nginx
```

### 3. 使用 Certbot 生成 SSL 证书
接下来，运行以下命令，Certbot 将自动为你的域名生成 SSL 证书并更新 Nginx 配置：

```bash
sudo certbot --nginx -d example.com -d www.example.com
```

按照提示操作，Certbot 将会：

- 验证域名所有权
- 获取 Let's Encrypt 的免费 SSL 证书
- 自动更新 Nginx 配置以使用 HTTPS

### 4. 设置自动续期
Certbot 会自动处理证书续期，但你可以手动测试一下是否成功：

```bash
sudo certbot renew --dry-run
```

### 5. 检查 HTTPS 是否工作
重新加载 Nginx 并确保 HTTPS 已成功启用：

```bash
sudo systemctl reload nginx
```

访问 `https://example.com` 以检查 SSL 是否已成功安装。




# README

## Install

```shell
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```

## HexoPlugin

```shell
# 服务器
npm install hexo-server --save
# 部署 git
npm install hexo-deployer-git --save
# 部署 rsync
npm install hexo-deployer-rsync --save
# 搜索
npm install hexo-generator-searchdb --save
# 迁移
npm install hexo-migrator-rss --save；hexo migrate rss “source”
# 包管理
npm install -g hexagon-cli
```

## rsync 部署

### 1. 本地配置

```shell
npm install hexo-deployer-rsync --save
```

_config.yml 配置

```json
deploy:
  type: rsync
  host: 111.230.170.109
  user: root
  root: /root/hexo
  port: 22
  delete: true
  verbose: true
  ignore_errors: false
```

### 2. 服务器配置

```shell
# 安装 rsync
sudo yum -y install rsync
# 安装 nginx
sudo yum install nginx
# 配置 nginx
vim /etc/nginx/nginx.conf
# 将 root /usr/share/nginx/html; 改为 root /root/hexo;
# 在 location 括号中添加 index index.html index.htm;
# 将 user nginx; 改为 user root root;
# 开启 nginx
sudo systemctl start nginx.service
# 重启 nginx
sudo systemctl reload nginx.service
# 开机启动 nginx
sudo systemctl enable nginx.service
```

### 3. 免密登陆

将本机的 ```.ssh/id_rsa.pub``` 文件内容，复制粘贴到服务器 ```.ssh/authorized_keys``` 文件中，可以免密登陆。

### 4. 部署到服务器

```shell
hexo g; hexo d;
```

### 5. 打开对应 ip 地址即可
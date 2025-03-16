# SSH、SCP、Rsync 和 Git 远程操作笔记

## 1. SSH (Secure Shell)

### 1.1 基本概念
- SSH是一种加密的网络传输协议
- 可以实现安全的远程登录和其他安全网络服务
- 默认端口号是22

### 1.2 常用命令
```bash
ssh username@hostname    # 基本连接格式
ssh -p port username@hostname    # 指定端口连接
```

### 1.3 SSH密钥配置
```bash
ssh-keygen -t rsa -C "your_email@example.com"    # 生成SSH密钥对
```
- 密钥存放位置:
  - Windows: `C:\Users\用户名\.ssh\`
  - Linux/Mac: `~/.ssh/`

## 2. SCP (Secure Copy)

### 2.1 基本概念
- 基于SSH的安全文件传输工具
- 可在本地和远程主机之间复制文件

### 2.2 常用命令
```bash
scp local_file username@hostname:remote_directory    # 上传文件
scp username@hostname:remote_file local_directory    # 下载文件
scp -r local_directory username@hostname:remote_directory    # 复制整个目录
```

## 3. Git Clone 和远程仓库

### 3.1 Git仓库地址解析
以 `git@github.com:userid/repo.git` 为例:
- `git@` - 表示使用SSH协议
- `github.com` - 远程仓库服务器地址
- `userid` - 用户名/组织名
- `repo.git` - 仓库名称

### 3.2 克隆命令
```bash
git clone git@github.com:userid/repo.git    # 使用SSH克隆
git clone https://github.com/userid/repo.git    # 使用HTTPS克隆
```

## 4. 搭建Git服务器

### 4.1 基础环境配置
```bash
sudo apt-get install git    # 安装Git
sudo adduser git    # 创建git用户
sudo passwd git    # 设置git用户密码
```

### 4.2 配置SSH访问
1. 创建SSH密钥目录:
```bash
sudo mkdir /home/git/.ssh
sudo touch /home/git/.ssh/authorized_keys
```

2. 设置权限:
```bash
sudo chown -R git:git /home/git/.ssh
sudo chmod 700 /home/git/.ssh
sudo chmod 600 /home/git/.ssh/authorized_keys
```

### 4.3 创建Git仓库
```bash
sudo mkdir /home/git/srv    # 创建仓库目录
cd /home/git/srv
sudo git init --bare project.git    # 初始化裸仓库
sudo chown -R git:git /home/git/srv    # 设置权限
```

### 4.4 安全配置
1. 禁用git用户shell登录:
```bash
# 编辑/etc/shells添加
/usr/bin/git-shell

# 修改git用户的shell
sudo chsh git -s $(which git-shell)
```

### 4.5 客户端使用
```bash
# 克隆远程仓库
git clone git@server_ip:/home/git/srv/project.git

# 或者使用简短格式
git clone git@server_ip:srv/project.git
```


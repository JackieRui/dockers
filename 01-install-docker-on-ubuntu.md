在Ubuntu上安装docker，从阿里云上申请的机器，安装docker-ce

#### 1.docker-ce

```
# 机器基本信息
$ uname -a
Linux iZ2zecpwkftd8945so3uykZ 5.4.0-108-generic #122-Ubuntu SMP Tue Mar 29 07:34:30 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
# 安装基本软件
$ sudo apt-get update
$ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common lrzsz -y
# 安装GPG证书
$ sudo curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
# 写入软件源信息
$ sudo add-apt-repository "deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
# 更新并安装
$ sudo apt-get update
$ sudo apt-get install docker-ce -y
# 查看docker版本
$ docker version
Client: Docker Engine - Community
 Version:           20.10.15
 API version:       1.41
 Go version:        go1.17.9
 Git commit:        fd82621
 Built:             Thu May  5 13:19:23 2022
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.15
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.17.9
  Git commit:       4433bf6
  Built:            Thu May  5 13:17:28 2022
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.6.4
  GitCommit:        212e8b6fa2f44b9c21b2798135fc6fb7c53efc16
 runc:
  Version:          1.1.1
  GitCommit:        v1.1.1-0-g52de29d
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```

#### 2.docker-mirrors

```
# 镜像加速器配置
$ sudo mkdir -p /etc/docker
$ sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://ojv4rqmr.mirror.aliyuncs.com"]
}
EOF
$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
```

#### 3.Nignx

```
# 安装nignx测试 拉取镜像
$ sudo docker pull nginx
# 运行nginx 并映射端口到80
$ sudo docker run --name mynginx -d -p 80:80 nginx
# 测试
$ curl 127.0.0.1:80
```


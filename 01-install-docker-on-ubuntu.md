在Ubuntu上安装docker，从阿里云上申请的机器，具体的安装步骤如下：

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
$ sudo add-apt-repository "deb [arch=amd64] https://mirrors.aliyun.com/dockerce/linux/ubuntu $(lsb_release -cs) stable"
# 更新并安装
$ sudo apt-get update
$ sudo apt-get install docker-ce -y



```


### 1.docker安装mysql

```
# 拉取镜像 指定mysql版本 mysql:5.7 默认拉取的mysql版本是8.0
$ docker pull mysql:5.7
# 命令行运行mysql
$ docker run -itd \
--name mysql0.1 \
-v /usr/local/docker/mysql/conf:/etc/mysql \
-v /usr/local/docker/mysql/logs:/var/log/mysql \
-v /usr/local/docker/mysql/data:/var/lib/mysql \
-p 3306:3306 \
-e MYSQL_ROOT_PASSWORD=123456 \
mysql

【错误1】
ERROR 2059 (HY000): Authentication plugin 'caching_sha2_password' cannot be loaded: dlopen(/usr/local/Cellar/mysql@5.6/5.6.51/lib/plugin/caching_sha2_password.so, 2): image not found
原因：mysql8 之前的版本中加密规则是mysql_native_password,而在mysql8之后,加密规则是caching_sha2_password, 
解决问题方法有两种,
一种是升级navicat驱动,
一种是把mysql用户登录密码加密规则还原成mysql_native_password. 
登陆容器 然后进入到mysql 执行如下命令：
ALTER  USER  'root'  IDENTIFIED  WITH  mysql_native_password  BY  '1234567';           
这样就可以在宿主机去连接mysql了
```


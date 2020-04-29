# Centos7安装gitlab服务

## 安装依赖软件

```shell
yum -y install policycoreutils openssh-server openssh-clients postfix
```

## 设置postfix开机自启，并启动，postfix支持gitlab发信功能

```shell
systemctl enable postfix && systemctl start postfix
```

## 下载gitlab安装包，然后安装

```shell
wget https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el7/gitlab-ce-10.0.0-ce.0.el7.x86_64.rpm
rpm -ihv gitlab-ce-10.0.0-ce.0.el7.x86_64.rpm
```

## 修改gitlab配置文件指定服务器ip和自定义端口

 vim /etc/gitlab/gitlab.rb 

```properties
#修改gitlab访问地址和端口，默认为80，改为8888
external_url 'http://192.168.0.108:8888'
#修改gitlab访问端口
nginx['listen_port'] = 8888
```

## 重载配置及启动gitlab

```shell
gitlab-ctl reconfigure
gitlab-ctl restart
```


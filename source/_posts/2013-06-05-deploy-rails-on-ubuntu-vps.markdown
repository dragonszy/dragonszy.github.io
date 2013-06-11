---
layout: post
title: "Ubuntu(12.04) VPS部署Rails环境"
date: 2013-06-05 20:42
comments: true
categories: [Rails, Ubuntu]
---

### 环境需求
1. Ubuntu12.04
2. Nginx
3. Unicorn
4. RVM - Ruby1.9.3 - Rails
5. MySQL

### 安装系统需要的包

```
$ sudo apt-get install -y build-essential openssl curl libcurl3-dev libreadline6 libreadline6-dev git zlib1g zlib1g-dev libssl-dev libyaml-dev libxml2-dev libxslt-dev autoconf automake libtool imagemagick libmagickwand-dev libpcre3-dev libsqlite3-dev libmysql-ruby libmysqlclient-dev
```

### 安装RVM
```
$ \curl -L https://get.rvm.io | bash -s stable
```
载入RVM环境，或重新开Terminal
```
$ source ~/.rvm/scripts/rvm
```
检测安装是否正确
```
$ rvm -v
rvm 1.20.13 (stable) by Wayne E. Seguin <wayneeseguin@gmail.com>, Michal Papis <mpapis@gmail.com> [https://rvm.io/]
```

### RVM安装Ruby
```
$ rvm install 1.9.3  # 如果需要1.9.3版
$ rvm install 2.0.0  # 如果需要2.0.0版
```

### 设置Ruby版本
```
$ rvm 1.9.3 --default
```
这时查看ruby的默认版本
```
$ ruby -v
ruby 1.9.3p429 (2013-05-15 revision 40747) [i686-linux]
$ gem -v
1.8.25
```

### 安装Rails
```
$ gem install bundler rails
```
查看测试安装是否正确
```
$ bundle -v
Bundler version 1.3.5
$ rails -v
Rails 3.2.13
```

### 安装Nginx
这里强烈推荐通过软件源的方式安装最新stable的Nginx。
默认Ubuntu自带的源通过apt-get install nginx时会装比较老的版本。
自己编译安装的话比较慢，还要写启动脚本，做服务设置等，没有特殊需求就不用这种方式。

[这篇](http://nginx.org/en/linux_packages.html)是Nginx官网关于通过包管理安装方法。
这里简要阐述Ubuntu12.04的安装过程。

 - 下载key文件，导入key文件
```
$ cd
$ wget http://nginx.org/keys/nginx_signing.key
$ sudo apt-key add nginx_signing.key
```

 - 增加源
```
$ sudo vim /etc/apt/sources.list
```
增加这两行
```
deb http://nginx.org/packages/ubuntu/ codename nginx
deb-src http://nginx.org/packages/ubuntu/ codename nginx
```
其中codename是你ubuntu的发行号，12.04是precise，上面给的网址也有详细列表。

 - 更新源
```
$ sudo apt-get update
```

 - 安装nginx
```
$ sudo apt-get install nginx
```

### 安装unicorn
```
$ gem install unicorn
```

### 安装nodejs
rails app需要一个javascript runtime，这里我们选择nodejs，[这篇](https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager)是官方的通过包安装方法。
这里也只列出Ubuntu安装方法。
```
$ sudo apt-get update
$ sudo apt-get install python-software-properties python g++ make
$ sudo add-apt-repository ppa:chris-lea/node.js
$ sudo apt-get update
$ sudo apt-get install nodejs
```

---
layout: post
title: "如何删除Rails的Migrations"
date: 2013-05-30 21:55
comments: true
categories: Rails
---

### 错误示范
直接删除db/migrate目录下的migration的rb文件，然后执行rake db:migrate

这样做以后会发现schema.rb中的内容还是老样子，比如删除了一个create_posts的migration，重新执行rake db:migrate之后schema.rb中仍然有create_table "posts"的代码，打开数据库，会发现还是生成了posts这张表。这样直接删除migration文件并未达到删除表或修改表的作用。

### 解决方法
打开数据库，打开project_development数据库，打开schema_migrations表，对应着现在的db/migrate目录下的migration时间戳，把多余的删除，然后删除schema.rb多余代码，重新执行rake db:migrate，可以发现schema.rb并没有变动。

### 正确做法
一般来说最好不要去编辑一个已经存在了的migration，即便里面有错误。
最好的做法是写一个新的migration来执行修复上一个写错了的migration的操作。

详细请参考：[Rails Migration Guides](http://guides.ruby-china.org/migrations.html)


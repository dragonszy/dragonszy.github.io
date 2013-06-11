---
layout: post
title: "如何使用Octopress博客"
date: 2013-05-28 10:58
comments: true
categories: Octopress
---

### 创建Post
``` ruby
rake new_post["My First Octopress Blog"]
```

### 修改category
``` ruby
categories: Octopress
# 一个categories
categories: [CSS3, HTML5]
# 多个categories
```

### 设置文章为草稿
``` ruby
published: false
```

### 创建Page
``` 
$ rake new_page[super-awesome]
# creates /source/super-awesome/index.markdown
$ rake new_page[super-awesome/page.html]
# creates /source/super-awesome/page.html
```
创建完新page后修改 source/_includes/custom/navigation.html 增加页面导航。

### 生成和预览
``` 
$ rake generate
$ rake watch
$ rake preview
```

### 部署到Github
``` 
$ rake setup_github_pages
$ rake generate
$ rake deploy
```

### 上传源代码到Github
```
$ git add .
$ git commit -m 'some changes'
$ git push origin source
```

### 推荐编辑器
1. Sublime Text
2. Mou

### 在新标签页打开超链接
1. 直接使用html `<a href="http://dragonszy.github.io">dragonszy's Blog</a>` 标签
2. 修改 source/_includes/custom/head.html ，增加javascript代码自动修改超链接
``` javascript
function addBlankTargetForLinks () {
  $('a[href^="http"]').each(function(){
  $(this).attr('target', '_blank');
  });
}

$(document).bind('DOMNodeInserted', function(event) {
  addBlankTargetForLinks();
});
```
记得要加上 `<script type="text/javascript"></script>` 标签哦!

### Latex公式支持
参考[雁起平沙博客](http://yanping.me/cn/blog/2012/03/10/octopress-with-latex/)介绍方法，使用 kramdown 渲染markdown文档，支持 Latex 。

### 常见问题 FAQ
1. 有序列表下嵌套内容列表序号不增加，可能是嵌套错误导致
2. rake generate 和 rake preview 之后draft(published: false)文章能在本地看到，这是有意为之，deploy时draft不参与，不用担心
3. Markdown语法的超链接不能在新窗口打开
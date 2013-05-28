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

### 创建Page
``` ruby
rake new_page[super-awesome]
# creates /source/super-awesome/index.markdown
rake new_page[super-awesome/page.html]
# creates /source/super-awesome/page.html
```

### 生成和预览
``` ruby
rake generate
rake watch
rake preview
```
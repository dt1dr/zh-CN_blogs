---
title: hexo+butterfly主题下美化笔记（一）
date: 2022-12-20 20:15:57
tags: 外观自定义
categories: hexo
cover: https://s2.loli.net/2022/12/20/krHvmQJnU48Kgz6.png
---

# hexo+butterfly 主题 博客装修笔记（一） 副标题、背景图和侧边栏

**hexo 6.3.0 + butterfly 4.5.1**

### 善用 VSCode 的 "Ctrl + F"查找功能快速定位对应设置

### 副标题（subtitle)

#### 若主题 config 中未定义副标题内容，可以直接在 hexo 原本的`_config.yml `中修改副标题内容。

```yml
# Site
title: # 网站标题
subtitle: # 副标题
description: # 描述
author: #站长名字
language: zh-CN
timezone: # 时区
```

##### 实现文字换行:

在如下实例中将字符串用`\<br>` 隔开。
在字符串中直接加 `\n `, `\`, `<<endl `**是不行的！(雾**

```yml
# Site
title: # 网站标题
subtitle: "Talk is cheap<br>Show me your code" # 副标题
description: # 描述
author: #站长
language: zh-CN
timezone:
```

#### 我该编辑哪个 config 来展示副标题？

在 `_config.butterfly.yml` 中自定义的副标题内容显示**优先级大于** `_config.yml`中定义的内容。处于管理方便，请保持其中一处为空以避免内容覆盖

如下所示，在`_config.yml`中定义了内容为
`"Talk is cheap<br>Show me your code"`的同时，在`_config.butterfly.yml`中定义
`source: 3  # 調用今日詩詞（簡體） https://www.jinrishici.com/`
返回网页如图：
![](https://s2.loli.net/2022/12/20/krHvmQJnU48Kgz6.png)

只会出现今日诗词网的返回内容

#### 在 `_config.butterfly.yml` 中自定义主页副标题设置:

**p.s. 请务必在主题 config**中将如下属性由`False`改为`True`启用,否则副标题不显示

```yml
subtitle:
enable: true
```

通过更改 source 属性的值，可以方便地调用名句~~装逼~~作为副标题。

### 主页图片

#### 在`_config.butterfly.yml` 中修改主页图片

找到`index_img`属性，将其值修改为图片路径 or URL

```yml
# The banner image of home page
index_img: https://s2.loli.net/2022/12/20/pJycIQgGdT7uKRS.jpg
```

在后面的`index_top_img_height`属性中更改该图高度。不填/空格则为全屏，~~方便展示 waifu~~。

```yml
# The height of top_img, eg: 300px/300em/300rem (主頁top_img高度)
index_top_img_height:
```

### 侧边栏 (aside)

在`_config.butterfly.yml` 中的`aside`属性中自定义，可以展示作者信息，最新文章，创作归档，网站资讯等。

```yml
aside:
  enable: true # 是否启用
  hide: false
  button: true
  mobile: true # 是否支持移动端显示
  position: right # 在页面左侧或右侧显示
  display:
    archive: true
    tag: true
    category: true
  card_author: # 作者信息
    enable: true
    description: "大一学生"
    button:
      enable: true
      icon: fab fa-github
      text: Follow Me
      link: https://github.com/dt1dr/dt1dr
  card_announcement:
  card_recent_post:
  card_categories:
  card_tags:
  card_archives:
  card_webinfo:
  ······
```

### 然后就可以安心上传文章啦~！

---
title: hexo添加标题打字机效果
comments: true
categories: hexo
tags: hexo
---

如果你喜欢 hexo 的主题没有配置打字机效果怎么办？ 下面教你如何自己添加~

## 一、创建.ejs 文件

在 themes/你的主题/layout 下添加一个.ejs 文件，举例文件名为 typewriter.ejs。

文件内容如下：

```js
<script src="//wow.techbrood.com/libs/jquery/jquery.min.js"></script>
<script type="text/javascript" src="https://cdn.bootcss.com/typed.js/2.0.5/typed.js"></script>
<script>
  var typed = new Typed("#subtitle", {
    // 注意：输出的可以是标签,将标签当节点运行.比如下面的h1
    // 这是一个字符串数组,可以填充多个值,使用引号修饰,使用逗号分割
    strings: ["<h1> <%= theme.subtitle || config.subtitle %> <h1>"],//_config.yml中subtitle配置项文字
    // 速度值越小打字速度越快
    typeSpeed: 80,
    // 用于在在输出字符结尾闪烁的符号
    cursorChar: ""
  });
  // 设置页面加载完成时再开始打字
  typed.stop();
  $(document).ready(function () {
    typed.start();
  });
</script>

```

注：#subtitle 为你需要显示文字的 dom 节点 id 或 classname;

## 二、引入自定义的.ejs 文件

在 themes/你的主题/layout/\_partial/header.ejs 中需要显示的节点下方添加 <%- partial('typewriter') %>。

```html
<a href="<%- url_for() %>" id="subtitle"></a>
<!-- 打字机效果 -->
<%- partial('typewriter') %>
```

## 三、更新博客

```bash
hexo clean && hexo deploy
```

这样就实现标题打字机动画效果啦~

![ ](https://cdn.jsdelivr.net/gh/Justlovesmile/CDN2/post/typejs4.gif)

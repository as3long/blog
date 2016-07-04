---
layout: post
title: "webcomponent（一）"
tags:
    -JavaScript
categories:
    javascript
---

webcomponent（一）
webcomponent是一个新的浏览器功能,为web提供了一个标准组件模型,包括以下几个部分:

- Shadow DOM
- Custom Elements
- HTML Imports
- HTML Templates

## Shadow DOM是什么
直接翻译是 影子文档对象模型。

定义：Shadow DOM 是一个 HTML 的新规范，其允许开发者封装自己的 HTML 标签、CSS 样式和 JavaScript 代码。Shadow DOM 以及我们以后将会讨论的一些技术，使得开发人员可以创建诸如 `<input type="range">` 这样自定义的一级标签。

用一个最简单的例子来解释Shadow DOM,我们看一下range组件
```
<input type="range">
```
打开Chrome的开发者工具，点击右上角的"Settings"按钮，
![设置按钮][img01]

勾选“Show user agent shadow DOM”，
![勾选“Show user agent shadow DOM”][img02]

你就可以看到range组件的DOM结构的细节。
![range shadow-root][img03]

看到标灰的 #shadow-root 了吗？这里就是所有视频播放器控制组件的所在之处。浏览器之所以将其置灰，是为了表明这部分是在 shadow DOM 里，对于页面的其他部分来说它是不可用的。这里的不可用意味着你写的 CSS 选择器和 JavaScript 代码都不会影响到这部分内容。

## 必须的HelloWorld

可以戳这里
[http://git.360rush.com/demo/shadowDom/helloworld.html](http://git.360rush.com/demo/shadowDom/helloworld.html)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Shadow DOM -- Hello World</title>
</head>
<body>
    <div class="hi">你好Shadow DOM!</div>
    <script>
        var hi = document.querySelector('.hi');
        var shadowRoot = hi.createShadowRoot();
        var dom = document.createElement('p');
        dom.innerHTML = '《<content></content>》';
        shadowRoot.appendChild(dom);
    </script>
</body>
</html>
```
结果是这样子的

![hello world][img04]

我们在helloworld中使用`<content>`标签,它的作用是在Shadow DOM中使用宿主的内容。
> 小明： 这有啥用啊？ 我能只显示其中一部分的内容吗？

答案是可以得，我们来看看下面的例子
[http://git.360rush.com/demo/shadowDom/contentSelector.html](http://git.360rush.com/demo/shadowDom/contentSelector.html)
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Shadow DOM -- Hello World</title>
</head>
<body>
    <helloworld>
        <span class="name">lonnyhuang</span>
        <span class="sex">男</span>
        <span class="city">深圳</span>
    </helloworld>
    <script type="tpl" class="sd-helloworld">
        <style>
            p {
                line-height: 20px;
                margin: 0;
            }
        </style>
        <p>姓名：<content select=".name"></content></p>
        <p>性别：<content select=".sex"></content></p>
        <p>所在城市：<content select=".city"></content></p>
    </script>
    <script>
        var host = document.querySelector('helloworld');
        var shadowRoot = host.createShadowRoot();
        shadowRoot.innerHTML = document.querySelector('.sd-helloworld').innerHTML;
    </script>
</body>
</html>
```
这里要用到`<content>`标签的`select`属性。为了方便这里直接用script标签做模板。可以看到对应的标签映射到了select选择器对应的位置

这里仅仅简单介绍了Shadow DOM的v0版本api。有人总结了v1版本和v0的不同点。其中可以用`slot`来做选择宿主的子节点的选择器
地址在这里：[http://hayato.io/2016/shadowdomv1/](http://hayato.io/2016/shadowdomv1/)

## 参考资料
- [Shadow DOM：简介](http://www.ituring.com.cn/article/177453)
- [Shadow DOM：基础](http://www.ituring.com.cn/article/177461)
- [译 - Shadow DOM第一课](http://www.toobug.net/article/shadow_dom_101.html)
- [webcomponents](https://github.com/w3c/webcomponents)

[img01]: ../assets/img/shadowDom/settings.png "设置按钮"
[img02]: ../assets/img/shadowDom/show-user-angent-shadow-DOM.png "Show user agent shadow DOM"
[img03]: ../assets/img/shadowDom/range-shadow-root.png "range shadow-root"
[img04]: ../assets/img/shadowDom/helloworld.png "hello world"
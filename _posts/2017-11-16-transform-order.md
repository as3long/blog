---
layout: post
title: "transform怎么控制层级"
tags:
    -CSS
categories:
    css
---

## 方法
给要控制层级的元素的父级设置`transform-style: preserve-3d`这个时候translateZ才有作用。
```html
<div class="xxx-box">
    <div class="b1"></div>
    <div class="b2"></div>
</div>
```
```scss
.xxx-box {
    transform-style: preserve-3d;
    .b1,.b2 {
        width: 80px;
        height: 80px;
        opacity: 0.7;
    }
    .b1 {
        transform: translateZ(-1px);
        background-color: red;
    }
    .b2 {
        transform: translate(20px, -60px) translateZ(-2px);
        background-color: green;
    }
}
```

## 参考文档
- [transform-style MDN文档](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform-style)
- [https://codepen.io/as3long/pen/bYoYPM](https://codepen.io/as3long/pen/bYoYPM)
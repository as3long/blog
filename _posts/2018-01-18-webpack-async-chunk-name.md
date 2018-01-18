---
layout: post
title: "webpack里面的0.js、1.js是哪儿来的？"
tags:
    -JavaScript
    -webpack
categories:
    javascript
---

## 设置了`chunkFilename`为`[name].js`，怎么还有`0.js`、`1.js`
原因是你使用了动态导入`import('xxx')`；

## 怎么让动态导入的模块有自己的名字
- 1. 是用注释 `webpackChunkName`

```js
import(/* webpackChunkName: "lodash" */ 'lodash');
```

- 2. 写了注释还不行就查一下bebel配置

`comments` 是不是配置成了`false`, 如果是`false`,改成`true`就行了
```js
{
    "comments": true
}
```

- 3. 如果发现还是不行，那检查一下你的webpack配置`chunkFilename`是`[id].js`还是`[name].js`
---
layout: post
title: "CSS3中transition-timing-function的24中常用动画效果"
tags:
    -CSS
categories:
   css
---

[24种cubic-bezier缓动效果来自](https://github.com/modeset/underoos/blob/e44607a67052840479af09cb678815fa551bc1ce/app/assets/stylesheets/mixins/_timing-equations.sass)

[动画效果,猛戳此处](http://underoos.modeset.com/styles.html#mixins-timing-equations)
<p style="color:red;font-size:12px;">注：需要注意的是在手机端有部分手机cubic-bezier的值范围只能在0-1之前。部分手机支持负数和大于1的数！</p>

- $ease-in-quad: cubic-bezier(0.55, 0.085, 0.68, 0.53)
- $ease-in-cubic: cubic-bezier(0.55, 0.055, 0.675, 0.19)
- $ease-in-quart: cubic-bezier(0.895, 0.03, 0.685, 0.22)
- $ease-in-quint: cubic-bezier(0.755, 0.05, 0.855, 0.06)
- $ease-in-sine: cubic-bezier(0.47, 0, 0.745, 0.715)
- $ease-in-expo: cubic-bezier(0.95, 0.05, 0.795, 0.035)
- $ease-in-circ: cubic-bezier(0.6, 0.04, 0.98, 0.335)
- $ease-in-back: cubic-bezier(0.600, -0.280, 0.735, 0.045)
- $ease-out-quad: cubic-bezier(0.25, 0.46, 0.45, 0.94)
- $ease-out-cubic: cubic-bezier(0.215, 0.61, 0.355, 1)
- $ease-out-quart: cubic-bezier(0.165, 0.84, 0.44, 1)
- $ease-out-quint: cubic-bezier(0.23, 1, 0.32, 1)
- $ease-out-sine: cubic-bezier(0.39, 0.575, 0.565, 1)
- $ease-out-expo: cubic-bezier(0.19, 1, 0.22, 1)
- $ease-out-circ: cubic-bezier(0.075, 0.82, 0.165, 1)
- $ease-out-back: cubic-bezier(0.175, 0.885, 0.320, 1.275)
- $ease-in-out-quad: cubic-bezier(0.455, 0.03, 0.515, 0.955)
- $ease-in-out-cubic: cubic-bezier(0.645, 0.045, 0.355, 1)
- $ease-in-out-quart: cubic-bezier(0.77, 0, 0.175, 1)
- $ease-in-out-quint: cubic-bezier(0.86, 0, 0.07, 1)
- $ease-in-out-sine: cubic-bezier(0.445, 0.05, 0.55, 0.95)
- $ease-in-out-expo: cubic-bezier(1, 0, 0, 1)
- $ease-in-out-circ: cubic-bezier(0.785, 0.135, 0.15, 0.86)
- $ease-in-out-back: cubic-bezier(0.680, -0.550, 0.265, 1.550)

可以用下面这种方式实现渐进兼容

```css
transition:all 2s cubic-bezier(1, 0, 0, 1);
-moz-transition:all 2s cubic-bezier(1, 0, 0, 1);	/* Firefox 4 */
-webkit-transition:all 2s cubic-bezier(1, 0, 0, 1);	/* Safari 和 Chrome */
-webkit-transition-timing-function:cubic-bezier(0.680, -0.550, 0.265, 1.550);/*单独写可以实现渐进兼容*/
transition-timing-function:cubic-bezier(0.680, -0.550, 0.265, 1.550);
```
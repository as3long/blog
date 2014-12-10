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

- $ease-in-quad: cubic-bezier(.55,.085,.68,.53)
- $ease-in-cubic: cubic-bezier(.55,.055,.675,.19)
- $ease-in-quart: cubic-bezier(.895,.03,.685,.22)
- $ease-in-quint: cubic-bezier(.755,.05,.855,.06)
- $ease-in-sine: cubic-bezier(.47, 0,.745,.715)
- $ease-in-expo: cubic-bezier(.95,.05,.795,.035)
- $ease-in-circ: cubic-bezier(.6,.04,.98,.335)
- $ease-in-back: cubic-bezier(.600, -.280,.735,.045)
- $ease-out-quad: cubic-bezier(.25,.46,.45,.94)
- $ease-out-cubic: cubic-bezier(.215,.61,.355, 1)
- $ease-out-quart: cubic-bezier(.165,.84,.44, 1)
- $ease-out-quint: cubic-bezier(.23, 1,.32, 1)
- $ease-out-sine: cubic-bezier(.39,.575,.565, 1)
- $ease-out-expo: cubic-bezier(.19, 1,.22, 1)
- $ease-out-circ: cubic-bezier(.075,.82,.165, 1)
- $ease-out-back: cubic-bezier(.175,.885,.320, 1.275)
- $ease-in-out-quad: cubic-bezier(.455,.03,.515,.955)
- $ease-in-out-cubic: cubic-bezier(.645,.045,.355, 1)
- $ease-in-out-quart: cubic-bezier(.77, 0,.175, 1)
- $ease-in-out-quint: cubic-bezier(.86, 0,.07, 1)
- $ease-in-out-sine: cubic-bezier(.445,.05,.55,.95)
- $ease-in-out-expo: cubic-bezier(1, 0, 0, 1)
- $ease-in-out-circ: cubic-bezier(.785,.135,.15,.86)
- $ease-in-out-back: cubic-bezier(.680, -.550,.265, 1.550)

可以用下面这种方式实现渐进兼容

```css
transition:all 2s cubic-bezier(1, 0, 0, 1);
-moz-transition:all 2s cubic-bezier(1, 0, 0, 1);	/* Firefox 4 */
-webkit-transition:all 2s cubic-bezier(1, 0, 0, 1);	/* Safari 和 Chrome */
-webkit-transition-timing-function:cubic-bezier(.680, -.550,.265, 1.550);/*单独写可以实现渐进兼容*/
transition-timing-function:cubic-bezier(.680, -.550,.265, 1.550);
```

复制到[http://cubic-bezier.com](http://cubic-bezier.com)
<<<<<<< HEAD
```javascript
=======
```json
>>>>>>> 32d0e3f2dff2c467771fc873c56d746c2f004a1d
{
"ease-in-quad":".55,.085,.68,.53",
"ease-in-cubic":".55,.055,.675,.19",
"ease-in-quart":".895,.03,.685,.22",
"ease-in-quint":".755,.05,.855,.06",
"ease-in-sine":".47,0,.745,.715",
"ease-in-expo":".95,.05,.795,.035",
"ease-in-circ":".6,.04,.98,.335",
"ease-in-back":".600, -.280,.735,.045",
"ease-out-quad":".25,.46,.45,.94",
"ease-out-cubic":".215,.61,.355, 1",
"ease-out-quart":".165,.84,.44, 1",
"ease-out-quint":".23, 1,.32, 1",
"ease-out-sine":".39,.575,.565, 1",
"ease-out-expo":".19, 1,.22, 1",
"ease-out-circ":".075,.82,.165, 1",
"ease-out-back":".175,.885,.320, 1.275",
"ease-in-out-quad":".455,.03,.515,.955",
"ease-in-out-cubic":".645,.045,.355, 1",
"ease-in-out-quart":".77, 0,.175, 1",
"ease-in-out-quint":".86, 0,.07, 1",
"ease-in-out-sine":".445,.05,.55,.95",
"ease-in-out-expo":"1, 0, 0, 1",
"ease-in-out-circ":".785,.135,.15,.86",
"ease-in-out-back":".680, -.550,.265, 1.550"
}
```
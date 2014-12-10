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

- $in-quad: cubic-bezier(.55,.085,.68,.53)
- $in-cubic: cubic-bezier(.55,.055,.675,.19)
- $in-quart: cubic-bezier(.895,.03,.685,.22)
- $in-quint: cubic-bezier(.755,.05,.855,.06)
- $in-sine: cubic-bezier(.47, 0,.745,.715)
- $in-expo: cubic-bezier(.95,.05,.795,.035)
- $in-circ: cubic-bezier(.6,.04,.98,.335)
- $in-back: cubic-bezier(.600, -.280,.735,.045)
- $out-quad: cubic-bezier(.25,.46,.45,.94)
- $out-cubic: cubic-bezier(.215,.61,.355, 1)
- $out-quart: cubic-bezier(.165,.84,.44, 1)
- $out-quint: cubic-bezier(.23, 1,.32, 1)
- $out-sine: cubic-bezier(.39,.575,.565, 1)
- $out-expo: cubic-bezier(.19, 1,.22, 1)
- $out-circ: cubic-bezier(.075,.82,.165, 1)
- $out-back: cubic-bezier(.175,.885,.320, 1.275)
- $in-out-quad: cubic-bezier(.455,.03,.515,.955)
- $in-out-cubic: cubic-bezier(.645,.045,.355, 1)
- $in-out-quart: cubic-bezier(.77, 0,.175, 1)
- $in-out-quint: cubic-bezier(.86, 0,.07, 1)
- $in-out-sine: cubic-bezier(.445,.05,.55,.95)
- $in-out-expo: cubic-bezier(1, 0, 0, 1)
- $in-out-circ: cubic-bezier(.785,.135,.15,.86)
- $in-out-back: cubic-bezier(.680, -.550,.265, 1.550)

可以用下面这种方式实现渐进兼容

```css
transition:all 2s cubic-bezier(1, 0, 0, 1);
-moz-transition:all 2s cubic-bezier(1, 0, 0, 1);	/* Firefox 4 */
-webkit-transition:all 2s cubic-bezier(1, 0, 0, 1);	/* Safari 和 Chrome */
-webkit-transition-timing-function:cubic-bezier(.680, -.550,.265, 1.550);/*单独写可以实现渐进兼容*/
transition-timing-function:cubic-bezier(.680, -.550,.265, 1.550);
```

复制到[http://cubic-bezier.com](http://cubic-bezier.com)

```
{
"in-quad":".55,.085,.68,.53",
"in-cubic":".55,.055,.675,.19",
"in-quart":".895,.03,.685,.22",
"in-quint":".755,.05,.855,.06",
"in-sine":".47,0,.745,.715",
"in-expo":".95,.05,.795,.035",
"in-circ":".6,.04,.98,.335",
"in-back":".600, -.280,.735,.045",
"out-quad":".25,.46,.45,.94",
"out-cubic":".215,.61,.355, 1",
"out-quart":".165,.84,.44, 1",
"out-quint":".23, 1,.32, 1",
"out-sine":".39,.575,.565, 1",
"out-expo":".19, 1,.22, 1",
"out-circ":".075,.82,.165, 1",
"out-back":".175,.885,.320, 1.275",
"in-out-quad":".455,.03,.515,.955",
"in-out-cubic":".645,.045,.355, 1",
"in-out-quart":".77, 0,.175, 1",
"in-out-quint":".86, 0,.07, 1",
"in-out-sine":".445,.05,.55,.95",
"in-out-expo":"1, 0, 0, 1",
"in-out-circ":".785,.135,.15,.86",
"in-out-back":".680, -.550,.265, 1.550"
}
```
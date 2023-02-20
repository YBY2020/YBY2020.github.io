---
title: css——持续更新遇到的问题
date: 2023-02-17 09:49:10
tags:
---

### 一、语法

### 二、布局

#### 1、text-align:center 失效

- [w3school 文档](https://www.w3schools.com/css/css_align.asp)

- 问题复现：

```html
<!-- 目的是让图片居中 -->
<img src="1.png" align="center" width="100px" />
```

官方文档解释：text-align: center --> To just center the text inside an element（使文字居中于元素内）

按照这里的解释该规则是用于外层容器，而不是用于需要居中的元素本身
但实际也可以用于需要居中的元素本身，不过需要该元素外层有一个 p 标签

- 解决方案：

```html
<p style="text-align: center;">
  <img src="1.png" width="100px" />
</p>

或

<p>
  <img src="1.png" align="center" width="100px" />
</p>

或

<!-- 
    最后这种方案是官方推荐的使图片居中的方案：
    To center an image, set left and right margin to auto and make it into a block element 
-->
<img src="1.png" style="display: block; margin: auto; width: 100px;" />
```

### 三、动画

### 四、元素样式

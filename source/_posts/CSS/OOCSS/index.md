---
title: CSS-面向对象
layout: page
comments: true
toc: true
categories: 
- CSS
tags:
- OOCSS
---

### 面向对象（Object Orientend简称OO）的CSS的概念解读
 `众多开发者忽视了CSS的表现（认为他太过简单，是一种机械的工作），而把更多经历关注在Javascript的性能上或者其他方面。OO CSS将页面可重用元素抽象成一个类，用Class加以描述，而与其对应的HTML即可看成是此类的一个实例。`

### OO CSS的作用和注意事项
<!--more-->
作用：
 * 加强代码复用方便维护 * 减小CSS体积 * 提升渲染效率 * 组件库思想，栅格布局可共用，减少选择器，方便扩展

注意事项：

 * 不要直接定义子节点，应把共性声明放到父类
 * 结构和皮肤相分离。
 * 容器和内容相分离。
 * 抽象出可重用的元素，建好组件库，在组件库内寻找可用的元素组装页面。
 * 往你想要扩展的对象本身增加class而不是他的父节点。
 * 对象应保持独立性。
 * 避免使用ID选择器，权重太高，无法重用。
 * 避免位置相关的样式。
 * 保证选择器相同的权重。
 * 类名 简短 清晰 语义化 OOCSS的名字并不影响HTML语义化。

### 示例
```css
代码示例： //不要直接定义子节点，应把共性声明放到父类
.mod .inner{……}       //.mod 下面的inner 建议
.inner{……}            //不是很建议的的声明
```

```css
代码示例：//结构和皮肤相分离
<div class=“container simpleExt”></div>   //html 结构
.container {……}    //控制结构的class
.simpleExt{……}      //控制皮肤的class
```

```css
代码示例：//容器和内容相分离。
<div class=“container”><ul><li>排行</li></ul></div>   //html 结构
.container ul{……}    //ul依赖了容器
<div class=“container”><ul class=“rankList ”><li>排行</li></ul></div>   
.rankList{……}    //解除与容器的依赖，可以从一个容器转移到其他容器

```

### OOCSS官网以及常用CSS库

- oocss.org //官网
- reset.css
- normalize.css
- Neat.css








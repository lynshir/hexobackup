---
title: 限制input智能输入数字且限制只能输入两位小数
layout: page
comments: true
categories: 
- jquery
tags:
- javascript
- jquery
- 笔记
---

>  chrome中的input不要加type="number",有问题,输入负号截取到第一个字符串是空，就默认text就行,若允许负数加上allowMinus类，正数只加limitNumber 


```js
    $(document).on('keyup', '.limitNumber,.allowMinus', function (e) {
      //修复第一个字符是小数点 的情况. 
      let fa = ''
      if (this.classList.contains('allowMinus')) {
        this.value.substring(0, 1) === '-' && (fa = '-')
      }
      if (this.value !== '' && this.value.substr(0, 1) === '.') {
        this.value = "";
      }
      this.value = this.value.replace(/^0*(0\.|[1-9])/, '$1');//解决 粘贴不生效
      console.log(this.value)
      this.value = this.value.replace(/[^\d.]/g, "");  //清除“数字”和“.”以外的字符
      this.value = this.value.replace(/\.{2,}/g, "."); //只保留第一个. 清除多余的
      this.value = this.value.replace(".", "$#$").replace(/\./g, "").replace("$#$", ".");
      this.value = this.value.replace(/^(\-)*(\d+)\.(\d\d).*$/, '$1$2.$3');//只能输入两个小数
      if (this.value.indexOf(".") < 0 && this.value !== "") {//以上已经过滤，此处控制的是如果没有小数点，首位不能为类似于 01、02的金额
        if (this.value.substr(0, 1) === '0' && this.value.length === 2) {
          this.value = this.value.substr(1, this.value.length);
        }
      }
      this.value = fa + this.value
    })
```
> 方法二：

```js
$(document).on('keydown', '.limitNumber,.allowMinus', function (e) {
    //8 = backspace;45=insert;46=delete;189 = '-';110小键盘.
      if(this.classList.contains('allowMinus')){
        if(e.keyCode === 189){
          return false
        }
      }
    if (e.keyCode !== 110 && e.keyCode !== 190 && e.keyCode !== 8 && e.keyCode !== 46 && e.keyCode !== 45 && (e.keyCode < 48
        || (e.keyCode > 57 && e.keyCode < 96) || e.keyCode > 110)) {
      return false
    }
  })
    .on('keyup', '.limitNumber', function (e) {
      let fa = ''
      if(this.classList.contains('allowMinus')){
        this.value.substring(0, 1) === '-' && (fa = '-')
      }
      this.value = this.value.replace(/[^\x00-\x80]/gi, '')
      //[^0-9.] 匹配不是数字和小数点的字符
      //[.][0-9]*[.] 匹配第一个小数点之后的数字，若多写小数点则归位到第一个小数点位置
      let str = (this.value.replace(/[^0-9.]/g, '')).replace(/.][0-9]*[.]/, '.').replace(/^(\-)*(\d+)\.(\d\d).*$/,'$1$2.$3')
      str.substring(0, 1) === '.' && (str = '0' + str)
      this.value = fa + str
    })
```

> **有什么好的办法记得评论哟！**
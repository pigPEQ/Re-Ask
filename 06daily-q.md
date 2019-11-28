## label的作用

`label`可以关联表单控件，可以和表单元素一起使用，让表单元素获取焦点。

```javascript
<label for="username">姓名：</label>
<input type="text" id="username">
```

- 属性1：`for`：关联表单
- 属性2：`accesskey`：设置快捷键



## 简述对BFC规范的理解

BFC（块级格式化上下文），相当于一个独立的容器，容器里的元素不会影响到外面的布局。

**形成BFC的条件：**

- `overflow：hidden/scoll/auto`  值不为`visible`
- `float`    值不为`none`
- `<html>`根元素
- `position`   值不为`static`或者`relative`
- `display`  值为`inline-block`、`inline-flex`、`table-cell`、`table-caption`

**应用场景：**

- 清除浮动，解决父元素高度塌陷
- 解决边距重叠
- 解决文字环绕在`float`的情况

[10分钟理解BFC](https://zhuanlan.zhihu.com/p/25321647 )



## 写一个去除制表符和换行符的方法

```javascript
/*
\f  匹配换页字符。
\n  匹配换行字符。
\r  匹配回车符字符。
\t  匹配制表字符。
\v  匹配垂直制表符。
*/
var deleteTest=(str)=>{
    return str.replace(/[\n|\t|\v\r\f]/g,"");  //注意：/s会匹配空格
}
```


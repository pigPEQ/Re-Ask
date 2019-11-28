## viewport有哪些属性

`viewport`是移动端的视区窗口，在pc端上基本等于显示区域，在移动端上会显示超出显示区域的部分，即出现横向移动滚动条，在`meta`属性中控制。

- `maximum-scale`：定义最大缩放比例，可以为小数

- `minimum-scale`：定义最小缩放比例，可以为小数

- `user-scale`：`yes`或`no`，是否支持用户缩放视图
- `intital-scale`：初始缩放比例
- `width`：设置layout viewport的宽度， 为一个正整数，或字符串"width-device" 

## px、em、rem

- `px`：固定长度单位，相对于显示器的屏幕分辨率而言的
- `em`：相对长度单位，相对于当前字体的大小，数值为倍数
- `rem`：相对长度单位，相对于根元素字体的大小，数值为倍数

## 写一个判断数据类型的方法

```javascript
var istype=(obj)=>{
    return Object.prototype.toString.call(obj).replace(/\[object\s|\]/g,'');// \[匹配"["，\s匹配空字符串，整体就是全局匹配"[object "或者"]"
}
console.log(istype([]))  //Array
```
-  如果`toString()`方法在自定义对象中未被覆盖，`toString()` 返回 "`[object type]`"，其中 `type` 是对象的类型。
```javascript
var o = new Object();
o.toString(); // returns [object Object]
```
- `typeof`只能判断基本类型：`string`、`boolean`、`number`、`undefined`、`object`

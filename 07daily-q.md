## iframe框架有哪些优缺点？

**优点：**

- 重载页面时无需重载整个页面，只需重载框架页
- 可实现跨域，每一个`iframe`的都可以不相同
- 技术容易掌握，使用方便
- 如果遇到加载缓慢的第三方内容如广告、图标，可以使用`iframe`解决

**缺点：**

- 每一个`iframe`意味着一个页面，会产生多个页面，不方便管理，并且引入多余的`css`与`js`文件，会增加请求的开销
- 对浏览器搜索引擎不友好
- `winodw.onload`事件会在所有的`iframe`加载完成后触发，所以会导致页面阻塞

## 清除浮动的方式及其优点

- `overflow:hidden`    会改变父元素的样式

- `clear:both`     在浮动的元素后新增一个块级元素，并设定`clear:both`,增加无意义的标签，不推荐使用

  `:after`、`:before`   在浮动的元素后新增一个块级元素，设定元素的宽高为0，`visibility：hidden`

- `position:absolute`
- 为包裹浮动元素的父元素设置`clearfix`属性

小结：其实就是两种，一种是触发`BFC`，另一种就是设定`clear:both`

## 统计一个字符或者字符串在另一个字符串中出现的次数

```javascript
var subStrCount=(target,str,count=0)=>{
    while(str.includes(target)){
        count++;
        str.replace(target,'');
    }
   return count;
}

var subStrCount=(target,str)=>{
    return str.spilt(str).length-1;  //spilt从指定位置分割字符串，用逗号隔开的数组的长度减1
}
console,log(subStrCount('a','asdhahdak'));// ['','sdh','hd','k']=>3个a
```


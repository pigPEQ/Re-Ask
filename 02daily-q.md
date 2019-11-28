## HTML的元素有哪些（包含H5）？

- 行内元素：

  `a`   `span`  `strong`  `img`  `input`  `em`   `radio`  `button`  `br`  `select`  `b`

- 块级元素：

  `p`  `h1-h6`  `div`  `ol`  `ul`  `li`  `table`  `td`  `tr`  `dl`  `dd`  `dt`  `textarea`

- H5新增元素：

  `header`   `footer`  `section`  `email`  `progress`  `canvas`  `vedio`  `audio`  `nav`

## 在页面上隐藏元素的方法？

- 占位

  `opacity：0`：设置透明度，完全透明，但占据空间  

  `z-index：-999`：设置堆放顺序，放入最底层

  `visibility:hidden`：页面渲染但不显示

  `transform:scale(0)`：设置缩放

  `margin-left：-100%`：文档流向左移动,移动到窗口之外

- 不占位

  `display：none`:页面不渲染不显示  

  `width：0  height：0  overflow：hidden`

## 写一个方法去除掉字符串中的空格？

```javascript
var str ="   a b c d  "
function trim(str){
    console.log(str.replace(/\s*/g,""));
}

----------------------------------------------
str.replace(/^\s*/g,"");  //去除左边的空格
str.replace(/\s*$/g,"");  //去除右边的空格
str.replace(/^\s*|\s*$/g,"");  //去除两边的空格
str.replace(/\s*/g,"");   //去除全部空格
```


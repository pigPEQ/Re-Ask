## 为什么H5中只需要写<!DOCTYPE HTML>就可以了？
- H4基于SGML标准(一种标记语言合集，包含`xml`、`html`)，除了声明`DOCTYPE`以外还要去引入DTD去声明渲染的标准，DTD分为标准模式和怪异模式，如果没有去声明DTD的话，
浏览器会自由发挥，变为怪异模式。
- H5没有基于SBML，所以不需要去引入DTD，但是要去声明`DOCTYPE`规范渲染标准。

## `position:fixed`在ios下无效怎么处理？
当用`position:fixed`在做"吸顶"、"吸底"效果时，弹出键盘控件、时间控件、表单控件时`fixed`属性会失效从而破坏布局。当如键盘控件弹起时，`fixed`的元素将无法浮动或者说是变为了
`absolute`元素，当页面内容超过一页时，滑动屏幕，先前的`fixed`元素随之滚动。
```HTML
<body class="layout-fixed">
    <!-- fixed定位的头部 -->
    <header>
        
    </header>
    
    <!-- 可以滚动的区域 -->
    <main>
        <!-- 内容在这里... -->
    </main>
    
    <!-- fixed定位的底部 -->
    <footer>
        <input type="text" placeholder="Footer..."/>
        <button class="submit">提交</button>
    </footer>
</body>
```
```css
//css部分
header, footer, main {
    display: block;
}

header {
    position: fixed;
    height: 50px;
    left: 0;
    right: 0;
    top: 0;
}

footer {
    position: fixed;
    height: 34px;
    left: 0;
    right: 0;
    bottom: 0;
}

main {
    margin-top: 50px;
    margin-bottom: 34px;
    height: 2000px
}
```
解决方法：
- 使用第三方库`isScroll.js` 不提倡，尽量不要用第三方的库
- 仅内部内容部分滚动
```HTML
<body class="layout-fixed">
    <!-- fixed定位的头部 -->
    <header>
        
    </header>
    
    <!-- 可以滚动的区域 -->
    <main>
        <div class="content">
        <!-- 内容在这里... -->
        </div>
    </main>
    
    <!-- fixed定位的底部 -->
    <footer>
        <input type="text" placeholder="Footer..."/>
        <button class="submit">提交</button>
    </footer>
</body>
```
```css
//css部分
header, footer, main {
    display: block;
}

header {
    position: fixed;
    height: 50px;
    left: 0;
    right: 0;
    top: 0;
}

footer {
    position: fixed;
    height: 34px;
    left: 0;
    right: 0;
    bottom: 0;
}

main {
    position:absolute;  // 变为绝对定位，实现内部滚动
    margin-top: 50px;
    margin-bottom: 34px;
    overflow-y:scroll;  // 使之可以滚动
    -webkit-overflow-scrolling: touch; //增加滚动的弹性，不加的话，手指松开后会立即停止滑动，会显得不流畅
}
.content{
    height: 2000px
}
```
## 什么是闭包以及闭包的缺点是什么？
闭包就是内部函数能够调用外部函数的变量或方法。当外部函数执行结束后，其调用栈释放后，其变量常驻内存,供内部函数读取调用。有人会疑惑，变量不应该随着调用栈的释放进GC了吗，实际上这里的变量并不是存在栈中，而是存在了内存堆中。  

**优点：**
- 隐藏变量，防止变量的篡改
- 防止变量污染作用域

**缺点：**
- 常驻内存，增加内存的开销
- 不释放容易造成内存的泄露

**常见的闭包：**
- 一个函数作为实参穿入另一个函数
- 一个函数作为另一个函数的返回值

**闭包的应用:**  
定义一个包含多个功能的js模块，只向外暴露一个包含n个方法的对象或者函数，模块使用者直接通过调用暴露对象的方法来实现各种功能。

## HTTP的状态码有哪些及其含义
- 200：成功
- 3xx：换种方式  301：重定向  304：未修改
- 4xx：前端问题
- 5xx：后端问题

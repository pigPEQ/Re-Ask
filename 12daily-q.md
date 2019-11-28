## H5中的form是怎么关闭自动完成的

- `autocomplete：off`  默认为`on`状态

 **解释：** 在部分浏览器上，foucs输入框可以把之前输入过的值自动填入，如果不想自动填入，可以关掉它。

## ::before和:after中单冒号和双冒号有什么区别，这个两个伪元素有什么用？

`CSS3`中定义了双冒号，单冒号表示伪类，双冒号表示伪元素。

- `:before`和`:after`表示一种样式，比如`:hover`、`:active`
- `::before`双冒号表示具体的内容，比如`::before`表示在元素之前插入的内容，不过需要`content`配合，并且插入的内容是行内样式。

## 算法实现一个9*9的乘法口诀，如下图所示：
<h2 align="center">
    <img src="./Imgs/11-img01.png">
</h2>

- **js部分：**
```javascript
 document.write("<div class='box'>");
    for(i=1;i<=9;i++){
        document.write("<div>")
        for(j=1;j<=i;j++){
            document.write("<span id='column'>"+i+'*'+j+'='+i*j+"</span>")
        }
        document.write("</div>")
    }
    document.write("</div>")
```

- **css部分：**
```CSS
       .box{
            text-align: center;
        }
        #column{
            display: inline-block;
            width: 50px;
            height: 15px;
            border: 1px solid #000;
            padding: 3px 10px;
            font-size: 10px;
            margin-right: -1px;
            margin-top: -1px;
        }
 ```

## 网页应用从服务器主动推送消息到客户端有哪些方式？
- `websocket`
- [SSE](https://www.cnblogs.com/goloving/p/9196066.html)(`Server-sent Events`,`websocket`的轻量替代方案)
- [EventSource](https://developer.mozilla.org/zh-CN/docs/Server-sent_events/EventSource/EventSource)     `pc=new EventSource(URL,Configuration)`

## 超链接属性target的取值与作用

<a>标签的`target`属性规定了打开链接的方式。  

- **语法**：`<a target="value">`

- **属性**：

|           值           |                             描述                             |
| :--------------------: | :----------------------------------------------------------: |
|        `_self`         |           默认属性，在当前窗口或框架中打开链接文档           |
|        `_blank`        |                   在新的窗口中打开链接文档                   |
|       `_parent`        |                  在父框架中集中打开链接文档                  |
|         `_top`         |                 在顶层框架中集中打开链接文档                 |
|      `framename`       |                  在指定的窗口中打开链接文档                  |
| 非上述值的**任意字符** | 相当于半个`_blank`，如果当前未打开该链接，则在新窗口中打开，否则，刷新已打开的窗口链接 |

## CSS画三角形及其原理

三角形是利用`border`属性制作的，很多人都不清楚`boder`的样式是什么样的，可能认为`border`是由矩形边框拼接的，其实`border`是由三角形拼接的，看看下面这个例子，你就一目了然了。

```css
.test{
        width: 200px;
        height: 200px;
        border: 200px solid;
        margin: 100px auto;
        border-color: orange red blue greenyellow;
    }
```
<h3 align="center">
<img src="Imgs/05-img1.png" alt="image-01" width="100px" height="100px"/>
</h3>

现在能看出一些效果了，我们继续将中间内容部分隐藏，只保留边框。

```css
.test{
        width: 0;
        height: 0;
        border: 200px solid;
        margin: 100px auto;
        border-color: orange red blue greenyellow;
    }
```

<h3 align="center">
<img src="Imgs/05-img2.png" alt="image-02" width="100px" height="100px"/>
</h3>

现在可以看到，`border`是由一个个三角形组成的，下面我们继续画三角形，可以直接将部分的`border`设为透明。

```css
 .test{
        width: 0px;
        height: 0px;
        border: 200px solid;
        margin: 100px auto;
        border-color: transparent transparent transparent greenyellow;
    }
```

看下效果：
<h3 align="center">
<img src="Imgs/05-img3.png" alt="image-03" width="100px" height="100px"/>
</h3>

如果想设置直角三角形，还可以将部分的`border`设为0，比如我们想画一个下直角三角形，设置`border-top`为0。

```css
 .test{
        width: 0px;
        height: 0px;
        border: 200px solid;
        border-top:0;
        margin: 100px auto;
        border-color: transparent transparent transparent greenyellow;
    }
```

<h3 align="center">
<img src="Imgs/05-img4.png" alt="image-04" width="100px" height="100px"/>
</h3>

## 写一个字符串大小写切换的方法

```javascript
//法1
var strChange=(str)=>{
            return [...str].map((code)=>{     //map方法对数组中的值进行遍历并返回一个新值
                return code.toUpperCase() === code?   
                code.toLowerCase():code.toUpperCase();
                }).join("");           //将map返回的新数组转化为字符串
        }


//法2
var strChange=(str)=>{
    return str.replace('/([a-z]*)([A-Z]*)/g',(a,s1,s2)=>{
        return `${s1.toUpperCase()}${s2.toLowerCase()}`   //这里用到了ES6的模板字符串
    })
}



console.log(strChange("abcDeFh"));
```


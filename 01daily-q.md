## 页面导入样式时，使用`link`与`@import`有什么区别？  

  `link`是`HTML`标签，`@import`是`css`提供的；

  `link`在引入样式加载时同时加载`，`@import`引入样式加载完成后加载；

  `link`没有兼容性问题，`@import`不兼容IE5以下；

  `link`可以操作`DOM`动态引入样式表改变样式，而`@import`不可以。

## 圣杯布局与双飞翼布局的理解与区别，并用代码实现

- 圣杯布局实现：

```javascript
<style>
    .container{
        padding: 0 300px 0 200px;
    }
    .main,.left,.right{
        float: left;
        position: relative;
        height: 30px;
    }
    .main{
        background:aqua;
        width: 100%;
    }
    .left{
        background: red;
        width: 200px;
        margin-left:-100%;//负的margin-left会让元素沿着文档流左移，当距离过大时会直接移到上一行
        left: -200px;//将覆盖部分让出来
        }
    .right{
        background: yellow;
        width: 300px;
        margin-left:-300px;
        right:-300px
    }
</style>

<div class="container">
        　　<div class="main">main</div>
        　　<div class="left">left</div>
        　　<div class="right">right</div>
    </div>
```

设置完`margin-left:-100%`后的样式如下图所示，你会发现`main`字符被覆盖了，说明`left`和`right`覆盖了部分的`main`，因此要将`left`左移200px，`right`右移300px。
<img src="/Imgs/layout01.png">



- 双飞翼布局

```javascript
<style>
    .main,.left,.right{
        float:left;
        height: 50px;
    }
    .main{
        background:aqua;
        width: 100%;
    }
    .left{
        background: red;
        width: 200px;
        margin-left: -100%;
        }
    .right{
        background: yellow;
        width: 300px;
        margin-left: -300px;
    }
    .content{
        margin: 0 300px 0 200px；
    }
 <div class="container">
        　　<div class="main">
            <div class="content">main</div>
            </div>
        　　<div class="left">left</div>
        　　<div class="right">right</div>
</div>
```

首先，在双飞翼布局里并没有设置`container`的位置，没有将`left`与`right`的宽度让出来，直接让`main`占据一整行，接下来`margin-left`设定与圣杯一样，与圣杯不一样的是，我们没有移动`left`和`right`，而是在`main`中新增了一个块级元素`content`，我们为`content`块级元素设定一个外边距，`margin-left`为`left`的宽度，`margin-right`为`right`的宽度。
<img src="./Imgs/layout02.png">

## 用递归算法实现，数组长度为5并且随机数在2-32间不重复的值
- 题目拆解：  
01.生成一个长度为5的数组；  
02.生成一个值在2-32之间的随机数；  
03.生成的随机数如果数组中没有，则放入数组中，已存在该随机数，则重新取随机数；  
04.控制递归的结束条件，数组的随机数个数大于或者等于数组的长度时，递归结束。
```javascript
  var arr = new Array(5);   //生成一个长度为5的数组
  var randomNumber=rdmNumber();   //取第一个随机数
  var i = 0;    //用于统计数组中的值的数目
  function insertRandom(){
      //如果数组中不存在这个随机数，则将该随机数放入数组，数组中元素个数加1
      if(arr.indexOf[randomNumber]==-1){
            arr.push(randomNumber);
            i++;
      }
      //如果数组中已存在该随机数，则重新调用rdmNumber()方法生成新的随机数
      else{
        rdmNumber();
      }
      //控制递归的结束
      //如果数组中的元素个数达到5个，直接输出该数组
      if(i>=arr.length){
        console.log(arr);
        return;
      }
      //递归整个insertRandom方法
      else{
        insertRandom();
      }
  }
  //生成随机数的方法
  function rdmNumber(){
    return Math.ceil(Math.random()*(32-2+1)+2);
  }
```
优化：
```javascript
  function putRandom(i,arr=[]){
    if(i=5) return arr;
    var randomNumber=Math.ceil(Math.random()*(32-2+1)+2);
    if(!arr.include(randomNumber)){
      arr.push(randomNumber);
      i++;
    }
    return putRandom(i,arr);
  }
  console.log(putRandom(0));
```

**法2：**
```javascript
var arr=new Array;
var insertRandom=()=>{
    arr.push(randomIndex());    //向数组中添加随机数
    arr=Array.from(new Set(arr));//返回一个无重复的数组
	if(arr.length>=5){
        console.log(arr);
        return;
      }
      //递归整个insertRandom方法
      else{
        return insertRandom();
      }
}
//生成随机数的方法
var randomIndex=()=>{
    return Math.ceil(Math.random()*(32-2+1)+2)
}
insertRandom();
```

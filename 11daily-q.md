## 常见的浏览器内核有哪些，并介绍一下对内核的理解

- `Webkit`:(Chrome、Safari)
- `Trident`:(IE)
- `Gecko`:(firefox)
- `Blink`:(Chrome28版本及之后)、Opera

内核分为渲染引擎和`js`引擎，`js`引擎越来越独立，所以现在说的内核一般是渲染引擎，渲染引擎负责页面的渲染，`js`引擎负责解析`javascript`

## 说说你对盒子模型的理解

- 标准盒子模型：`margin`、`padding`、`border`、`content`
- IE盒子模型：`content`、`content-box`    

`CSS3`中引入了`box-sizing`，可以对这两种盒子模型进行切换。

- `content-box`:对应标准盒子模型，在宽度和高度之外绘制元素的内边距和边框。
- `border-box`:对应IE盒子模型，在宽度和高度之内绘制元素的内边距和边框，元素的宽度和高度决定了元素的边框盒。

## 简要描述一下js有哪些内置对象

- 基础对象`Object` 
- 数学对象`Math` 
- 数组对象`Array` 
- 方法对象`Function` 
- 数字对象`Number` 
- 布尔对象`Boolean` 
- 字符串对象`string` 
- 时间对象`Date` 
- 正则对象`Regex`

## 手写一个节流和防抖

```javascript
//防抖：若重复点击则清除定时器，从而触发定时器的重新计时
var deBounce=(Fn,time)=>{
    return ()=>{
        let context=this;
        let arr=arguments;//为了让deBounce函数返回的函数this指向不变以及依旧能接受到e参数
        
        if(timer) clearTimeout(timer);
        let timer=setTimeout(()=>{
            Fn.apply(context,arr)
        },time);
    }
}
```

```javascript
//节流：若多次点击，只有达到一定的时间差才会触发执行函数
var throttling=(Fn,time)=>{
    let last=0;
    return ()=>{
        let context=this;
        let arr=arguments;
        
        let now=Date now();
        if(now-last>=time){
            Fn.apply(context,arr);
            last=now;
        }
    }
}
```

## 写React/vue项目时为什么要在列表组件中加入key，其作用是什么？
React与vue都是采用了diff算法去对比操作前后的虚拟节点，从而更新节点的。key会为每一个虚拟节点提供一个唯一的标识，当头尾交叉对比没有结果时，会根据新节点的key与旧节点数组的key依次进行对比，从而快速找到相应的旧节点，如果没有匹配到相应的旧节点，那么就认为是新增节点。如果没有加入key，那么就会采取遍历的方式找出新节点对应的旧节点。
- 有key 采用的是map映射的方式，速度更快
- 无key 采用的是遍历的方式  

部分人会认为不带key的速度更快，为什么？那是因为不带key的情况下可以更有效的复用节点，从而提高性能，这并不是key的作用,并且带key在增删节点上是有性能消耗的。
部分的vue源码：
```javascript
// vue项目  src/core/vdom/patch.js  -488行
// 以下是为了阅读性进行格式化后的代码

// oldCh 是一个旧虚拟节点数组
if (isUndef(oldKeyToIdx)) {
  oldKeyToIdx = createKeyToOldIdx(oldCh, oldStartIdx, oldEndIdx)
}
if(isDef(newStartVnode.key)) {
  // map 方式获取
  idxInOld = oldKeyToIdx[newStartVnode.key]
} else {
  // 遍历方式获取
  idxInOld = findIdxInOld(newStartVnode, oldCh, oldStartIdx, oldEndIdx)
}
```
Map函数
```javascript
function createKeyToOldIdx (children, beginIdx, endIdx) {
  let i, key
  const map = {}
  for (i = beginIdx; i <= endIdx; ++i) {
    key = children[i].key
    if (isDef(key)) map[key] = i
  }
  return map
}
```
遍历寻找
```javascript
// sameVnode 是对比新旧节点是否相同的函数
 function findIdxInOld (node, oldCh, start, end) {
    for (let i = start; i < end; i++) {
      const c = oldCh[i]
      
      if (isDef(c) && sameVnode(node, c)) return i
    }
  }
```
- [vue中的diff算法](https://www.jianshu.com/p/2be289759ecb)


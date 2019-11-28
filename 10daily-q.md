## 谈谈对语义化标签的理解

见名知义，方便后期维护，易于代码重构，有助于SEO。

## CSS常用布局
1. 圣杯布局
2. 双飞翼布局
3. 弹性布局
4. 网格布局
5. 绝对布局
- [几种经典的布局](https://github.com/pigPEQ/Constant-Study/blob/master/doc/H5/layout.md)

## 简述回调函数并出例子

函数a作为参数传入函数b中，在执行函数b时，只有函数b执行完成后，才会去执行函数a，当然不一定执行函数a，只有达到一定的条件才会去执行a。主要用于异步操作 例如网络请求 防止页面同步代码阻塞导致渲染线程停止 。

```javascript
var b=(callback,time)=>{
    setTimeout(callback,time);
}
b(()=>{console.log('我是函数b')},1000);
console.log('我是同步任务');
```

## 手写一个promise

```javascript
 var promise=new Promise((resolve,reject)=>{
     //初始化promise状态为pending状态
     //启动异步任务
     $.ajax({
         type:'get',
         datatype:'json',
         url:'xxx.php',
         success:()=>resolve('成功了')； //修改promise状态为fullfilled
         error：()=>reject('失败了');  //修改promise状态为rejected
     })
 })
 
 promise.then((successMsg)=>{
     alert('success')
 },(errorMsg=>{
     alert('error')
 }))
 
```

- **原理：** 创建`promise`对象，`promise`对象发送异步请求，调用`.then()`方法去注册成功或失败的回调函数，异步请求成功或失败后，调用`resolve()`或`reject()`方法去执行之前注册的成功或失败的回调函数。

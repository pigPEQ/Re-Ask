## 浏览器内多个标签页之间的通信方式有哪些？

- `window.postMessgae`    可跨域   `H5`提供的一个新的`API`

- 本地存储    只要在同一个域名下就能实现通信与数据的共享
- `webSocket`   可跨域

## 优雅降级与渐进增强

- **优雅降级：** 一开始就做好一个完善的版本，然后向低版本兼容；（向下兼容）
- **渐进增强：** 一开始先做一个基本使用的版本，然后逐渐丰富内容与体验。（向上兼容）

## 分别写一个加密字符串与解密字符串的方法

```javascript
var encodeStr=(str)=>{
    return [...str].map((s)=>{
        return String.fromCharCode(s.charCodeAt()*10); //charCodeAt(index)将字符串转为Unicode编码，有一点觉得奇怪，许多教程上说index是必选参数，而实际上不填好像这里也没啥问题。
        //String.fromCharCode()  将Unicode编码转为字符串
    }).join('');
}

var decodeStr=(str)=>{
    return [...str].map((s)=>{
        return String.fromCharCode(s.charCodeAt()/10);
    }).join('');
}

console.log(encodeStr('SDSAH'))   //output '̾ʨ̾ʊː'
console.log(decodeStr('TETBI'))   //output 'SDSAH'
```
**优化：**
```javascript
//param:   method可选参数：encodeStr(加密)与decodeStr(解密)
var codeStr=(method,str)=>{
    var hit = method=='encodeStr'?'*':'/';
    return [...str].map((item)=>{
        return String.fromCharCode(eval(item.charCodeAt()+hit+10));
    }).join('');
}
console.log(codeStr('encodeStr','SDSAH'));
```

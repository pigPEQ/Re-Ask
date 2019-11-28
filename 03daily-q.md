## HTML里的全局属性（global attribute）有哪些，包含H5？

`id`      `name`     `value`     `class`     `style`      `src`       `width`     `height`      `lang`       `title`
  
  
## CSS的选择器有哪些，哪些可以继承?

- `id`选择器   `#header`
- 类选择器      `.student`
- 后代选择器    `>`
- 兄弟选择器    `+`
- 通配符            `*`
- 子选择器         
- 伪类选择器     `:hover`
- 伪元素选择器   `:before`
- 属性选择器   `[type='input']`

   **可以继承**

- 字体属性：`font-size`、`font-family`、`font-weight`、`font-style`
- 文本属性：`text-indent`、`text-align`、`line-height`、`word-spacing`、`letter-spacing`、`color`、`direction`、`text-transform`
- 元素可见：`visibility`、`opacity`
- 光标属性：`cursor`
  
  
## 去除字符串中的最后一个指定的字符

**思路1：**

- 找出最后一个字符串的位置   `lastIndexOf()`方法
- 截取两部分的字符串，拼接字符串   `substring()`、`slice()`、`substr()`方法
  - `substring(start,[end])`,负数转为0，两个参数中较小的作为start  
  - `slice(start,[end])`，负数加上字符串的长度后转为正值，第一个参数大于第二个参数返回空字符串  
  - `substr(start,[length])`
```javascript
function delLastChar(str,char){
    var index=str.lastIndexOf(char);
    return str.substring(0,index)+str.substring(index+1);
}
```
  
  
**思路2：**

- 找出最后一个字符串的位置   `lastIndexOf()`方法

- 删除该字符,返回删除指定字符后的字符串。

- 将字符串转化为数组，利用数组的方法删除某个字符，删除后再将数组转为字符串

  字符串转化数组：`spilt('')`   `Array.from(str)` `Array.from`将伪数组或可迭代对象转化为一个浅拷贝的数组 [...str] 

  数组方法删除某个字符  `splice()`方法

  将数组转化为字符串  `join()`方法

  ```javascript
  function delLastChar(str,char){
      var index =str.lastIndexOf(char);
      var arr=Array.from(str);
      arr.splice(index,1);  //注意：splice方法返回的是删除的对象
      return arr.join('');
  }
  ```
  
  
## 数组去重

```javascript
//双层嵌套循环，前者与后者比较
function arradvance(arr){
    for(var i=0;i<arr.length;i++){
        for(var j=i+1;j<arr.length;j++){
            if(arr[i]===arr[j]){
                arr.splice(j,1);
                j=j-1;
            }
        }
    }	
  return arr;  
}
```

```javascript
//开辟新数组，将不重复的数字放入新数组中
function arradvance(arr){
    var arr0=new Array();
    for(var i=0;i<arr.length;i++){
        if(arr0.indexOf(arr[i]==-1)){
            arr0.push(arr[i]);
        }
    }
    return arr0;
}
```

使用`filter`过滤：

```javascript
function arradvance(arr){
    var rest=arr.filter(function(item,index,array){
        return array.indexOf(index)==index;
    })
    return res;
}
```

使用ES6新的数据结构：

```javascript
function arradvance(arr){
    return Array.from(new Set(arr));//Set是ES6提供的新的数据结构，类似数组，但是成员值都是唯一，不重复的	
}

//再次简化
var arradvance=(arr)=>{
    return [...new Set(arr)];
}
```


## H5的离线缓存怎么使用，工作原理是什么？

#### 浏览器缓存

针对单个文件：

- `Cookie`

  可以设置有效期  

  存储大小限制在4k以内  

  安全性低，将数据内容加在了请求头中

- `localstorage`

  键值对方式存储  

  永久存储，不手动删除，永不失效

  存储大小5M  

  常用`API`：`localstorage.setItem`、`localstorage.getItem`、`localstorage.removeItem`、`localstorage.clear`

- `sessionstorage`

  与`localstorage`的使用方法相同  

  页面关闭时清空

#### 离线缓存（`application cache`）

针对整个应用，可以主动通知浏览器更新资源：

- 配置`manifest`文件

```html
//manifest文件是最简单的文本，相关配置在.appcache文件中，告知浏览器缓存及不缓存的内容
//该文件包含三部分
CACHE MANIFEST:            //CACHE MANIFEST:该标题下的文件在第一次加载时进行缓存
/theme.css
/main.js

NETWORK: 				 //NETWORK:该标题下的文件需要与服务器连接，且不需要缓存
login.jsp

FALLBACK:				 //FALLBACK：该标题下的文件页面无法访问时的回退页面（如404）
/html/404.html
```

- 服务器上：`manifest`文件需要配置正确的`MIME-type`，即`text/chache-manifest`

`application cache`的优势：

- 无网络时可访问页面
- 加快页面加载速度
- 降低服务器负载

#### Web-SQL

`Web-SQL`并不是H5规范中的一部分，它是一个独立的规范，引入了一组使用`SQL`来操作客户端数据库的`API`

```javascript
//openDatabase:使用现有的数据库或者创建一个数据库来创建一个数据库对象
var db=openDatabase('mydb', '1.0', 'TEST DB', 2 * 1024 * 1024, fn)

//transaction：用于控制一个事务，以及基于这种情况执行提交或回滚
//executeSql:执行实际的SQL语句
db.transaction(function(fc){
    fc.executeSql('CREATE TABLE IF NOT EXISTS WIN (id unique, name)');
    fc.executeSql('INSERT INTO WIN (id, name) VALUES (1, "winty")');
})
```

#### [IndexedDB](https://developer.mozilla.org/zh-CN/docs/Web/API/IndexedDB_API/Using_IndexedDB)

 索引数据库（`IndexedDB`）`API`（作为`HTML5`的一部分）对创建具有丰富本地存储数据的数据密集型的离线`HTML5 Web`应用程序很有用，同时它还有助于本地缓存数据，使传统在线`Web`应用程序（比如移动`Web`应用程序）能够快速的运行和响应。 

## CSS3中新增的伪类有哪些？

CSS3中规定伪类用`:`表示，伪元素用`::`表示。

常用部分：

- `:first-child`、`:last-child`         取第一个元素/最后一个元素  
- `:not()`        括号中的条件取反  
- `:nth-child(2n+1)`、`:nth-child(2n)`   奇数列、偶数列

其他：

- `:root`  `html`根元素  
- `:only-child()`   只有一个子元素时才会生效  
- `:empty()`   选择连空格都没有的元素  
- `:first-of-type()`、`:last-of-type()`  一组兄弟元素中第一个该类型的元素
- `:checked`  已勾选

## 写一个方法把下划线命名转成大驼峰命名

```javascript
function toCamel(str){
    var a=str.split('_');
    if(a.length==1) return;
    a.reduce((b,c)=>{
        return b+c.substr(0,1).toUpperCase()+c.substr(1);
    }) 
}
```
- [`.map()`、`.filter()`、`.reduce()`的用法](https://www.jianshu.com/p/e87b195f6943)

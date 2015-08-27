### [Location](https://developer.mozilla.org/en-US/docs/Web/API/Location)

#### 属性

##### href

设置或返回完整的 URL

##### protocol

设置或返回当前 URL 的协议，带后面的`:`

```javascript
// 例如页面地址为'http://www.baidu.com';
console.log(location.protocol); //'http:'
```

##### host

设置或返回主机名和当前 URL 的端口号

```javascript
// 例如页面地址为'http://www.baidu.com';
console.log(location.host); //"www.baidu.com"

// http://localhost:63342/ngtest/scope.html
console.log(location.host); //"localhost:63342"
```

##### hostname

设置或返回当前 URL 的主机名（和host不同的是它不包含端口号）

```javascript
// 例如页面地址为'http://www.baidu.com';
console.log(location.hostname); //"www.baidu.com"

// http://localhost:63342/ngtest/scope.html
console.log(location.hostname); //"localhost"，这里不带端口号
```

##### port

设置或返回当前 URL 的端口号

```javascript
// 例如页面地址为'http://www.baidu.com';
console.log(location.port); //"" 不存在端口号返回空

// http://localhost:63342/ngtest/scope.html
console.log(location.port); //"63342"
```

##### pathname

设置或返回当前 URL 的路径部分

```javascript
// 例如页面地址为'http://www.baidu.com';
console.log(location.pathname); //"/" 根域名下只返回'/'

// http://localhost:63342/ngtest/scope.html
console.log(location.pathname); //"/ngtest/scope.html"
```

##### search

设置或返回从问号 (?) 开始的 URL（查询部分）

```javascript
// 例如页面地址为'http://www.baidu.com?a=123';
console.log(location.search); //"?a=123"
```

##### hash

设置或返回从井号 (#) 开始的 URL（锚）

```javascript
// 例如页面地址为'http://www.baidu.com#123';
console.log(location.hash); //"#123"
```

#### 方法

##### assign()

加载一个新的文档

```javascript
location.assign('http://www.baidu.com');

// 等价于
location.href = 'http://www.baidu.com'
```

##### reload()

重新加载当前文档

##### replace()

用新的文档替换当前文档

注：`assign()`和`replace()`的不同之处在于：当使用`replace()`时，当前页面不会保存到历史记录中（session History），意味着不能通过回退按钮返回。而`assign()`则可以。


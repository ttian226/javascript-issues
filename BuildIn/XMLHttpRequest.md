### XMLHttpRequest

`XMLHttpRequest`是一个浏览器接口，可以使javascript进行HTTP(S)通信

#### XMLHttpRequest老版本的用法

1. 创建XMLHttpRequest实例

```javascript
var xhr = new XMLHttpRequest();
```

2. 向远程主机发出一个HTTP请求

```javascript
xhr.open('GET', 'example.php');
xhr.send();
```

3. 等待远程主机做出回应。这时需要监控XMLHttpRequest对象的状态变化，指定回调函数

```javascript
xhr.onreadystatechange = function() {
　　if ( xhr.readyState === 4 && xhr.status === 200 ) {
　　　　alert( xhr.responseText );
　　} else {
　　　　alert( xhr.statusText );
　　}
};
```

上面的代码包含了老版本XMLHttpRequest对象的主要属性：

    * xhr.readyState：XMLHttpRequest对象的状态，等于4表示数据已经接收完毕。
    * xhr.status：服务器返回的状态码，等于200表示一切正常。
    * xhr.responseText：服务器返回的文本数据
    * xhr.responseXML：服务器返回的XML格式的数据
    * xhr.statusText：服务器返回的状态文本。

例子:

test.php:

```php
$name = trim($_POST['name']);
$age = intval($_POST['age']);
$data = array('status'=>1, msg=>'ok', data=>array('name'=>$name, 'age'=>$age));
echo json_encode($data);
```

使用jquery来post数据

```javascript
$.post('http://localhost/test.php', {name: 'ttian226', age: '2'}, function(data) {
    JSON.parse(data);
});
```

使用XMLHttpRequest来post数据

```javascript
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
        console.log(JSON.parse(xhr.responseText));
    }
};

xhr.open('POST', 'http://localhost/test.php', true);
xhr.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
xhr.send('name=ttian226&age=2');
```

使用FormData来传输数据，FormData为html5新增的一种对象

```javascript
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
        console.log(JSON.parse(xhr.responseText));
    }
};

xhr.open('POST', 'http://localhost/test.php', true);

// 创建FormData对象
var data = new FormData();

// 通过append方法给FormData对象赋值
data.append('name', 'ttian226');
data.append('age', 3);

// send接受这个FormData对象
xhr.send(data);
```

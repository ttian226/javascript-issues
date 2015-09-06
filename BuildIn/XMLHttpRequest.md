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

老版本XMLHttpRequest的缺点：

    * 只支持文本数据的传送，无法用来读取和上传二进制文件。
    * 传送和接收数据时，没有进度信息，只能提示有没有完成。
    * 受到"同域限制"（Same Origin Policy），只能向同一域名的服务器请求数据。


#### 新版本XMLHttpRequest

针对老版本XMLHttpRequest做了如下改进：

    * 可以设置HTTP请求的时限。
    * 可以使用FormData对象管理表单数据。
    * 可以上传文件。
    * 可以请求不同域名下的数据（跨域请求）。
    * 可以获取服务器端的二进制数据。
    * 可以获得数据传输的进度信息

1. HTTP请求超时：

有时，ajax操作很耗时，而且无法预知要花多少时间。如果网速很慢，用户可能要等很久。
新版本的`XMLHttpRequest`对象，增加了`timeout`属性，可以设置HTTP请求的时限

```javascript
xhr.timeout = 3000;
```

上面的语句，将最长等待时间设为3000毫秒。过了这个时限，就自动停止HTTP请求。与之配套的还有一个`ontimeout`事件，用来指定回调函数。

```javascript
xhr.ontimeout = function() {
    alert('请求超时');
};
```

2. FormData对象

```javascript
// 创建FormData对象
var data = new FormData();

// 通过append方法给FormData对象赋值
data.append('name', 'ttian226');
data.append('age', 3);

// send接受这个FormData对象
xhr.send(data);
```

FormData对象也可以用来获取网页表单的值。

例子:

```html
<form action="http://localhost/test.php" method="post">
    <p>First name: <input type="text" name="fname" /></p>
    <p>Last name: <input type="text" name="lname" /></p>
    <input id="btn" type="submit" value="Submit" />
</form>
```

```javascript
document.addEventListener('DOMContentLoaded', complete, false);

function complete() {
    var btn = document.getElementById('btn');
    btn.addEventListener('click', function(e) {
        e.preventDefault();
        post();
    }, false);
}

function post() {
    var xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function() {
        if (xhr.readyState === 4 && xhr.status === 200) {
            console.log(JSON.parse(xhr.responseText));
        }
    };

    // 取得表单元素的引用
    var form = document.querySelector('form');
    // 用表单元素初始化FormData对象
    var data = new FormData(form);
    xhr.open('POST', form.action);
    xhr.send(data);
}
```


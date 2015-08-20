#### JSONP原理

利用在页面中创建`<script>`节点的方法向不同域提交HTTP请求的方法称为**JSONP**，这项技术可以解决跨域提交Ajax请求的问题

jsonp 的核心则是动态添加`<script>`标签来调用服务器提供的js脚本，允许用户传递一个`callback`参数给服务端，然后服务端返回数据时会将这个`callback`参数作为函数名来包裹住JSON数据，这样客户端就可以随意定制自己的函数来自动处理返回数据了

在同源策略下，在某个服务器下的页面是无法获取到该服务器以外的数据的，但 img、iframe、script 等标签是个例外，这些标签可以通过src属性请求到其他服务器上的数据。利用`<script>`标签的开放策略，我们可以实现跨域请求数据，当然，也需要服务端的配合。一般的ajax是不能跨域请求的，因此需要使用一种特别的方式来实现跨域，其中的原理是利用`<script>`元素的这个开放策略。


#### JSONP实例

实例一：

在域名`example1.com`下。客户端的html文件。在声明回调函数`jsonpCallback`之后，客户端通过`script`标签向服务器跨域请求数据，然后服务端返回相应的数据并动态执行回调函数。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <script>
        // 定义回调函数jsonpCallback
        function jsonpCallback(data) {
            console.log(data);
        }
    </script>
    <script src="http://example2.com/test/getdata?callback=jsonpCallback"></script>
</head>
<body>
</body>
</html>
```

在域名`example2.com`下。服务端的的test.php文件

```php
public function getData() {
    // get过来的回调函数名
    $callback = $_GET['callback'];

    $data = array('msg'=>'hello');
    $result = json_encode($data);

    echo $callback . "($result)";
}
```

当我们正常地请求一个JSON数据的时候，服务端返回的是一串JSON类型的数据，而我们使用JSONP模式来请求数据的时候，服务端返回的是一段可执行的JavaScript代码，所以我们可见服务器代码最后一行:

    $_GET['callback']. '(' . json_encode(array('msg'=>'hello')) . ')'


实例二：

使用`$.ajax()`

```javascript
var url = 'http://example2.com/test/getdata';

$.ajax({
    url: url,
    dataType: 'jsonp',
    success: function (data) {
        console.log(data);
    }
});
```
上面通过jsonp请求的路径为：
`http://example2.com/test/getdata?callback=jQuery21407163675976917148_1440034042647&_=1440034042648`

回调方法名是一个随机的字符串`jQuery21407163675976917148_1440034042647`


如果设置了`jsonp`属性，如下`jsonp: 'callbackparam'`将会使用`callbackparam`替代默认的`callback`
即请求路径变为`http://example2.com/test/getdata?callbackparam=jQuery21407163675976917148_1440034042647&_=1440034042648`

```javascript
var url = 'http://example2.com/test/getdata';

$.ajax({
    url: url,
    dataType: 'jsonp',
    jsonp: 'callbackparam',
    success: function (data) {
        console.log(data);
    }
});
```

如果设置了`jsonpCallback`属性，请求地址变为:`http://example2.com/test/getdata?callbackparam=callbackfunc&_=1440034042648`
就是把`jsonpCallback`属性替换成一个随机字符串

```javascript
var url = 'http://example2.com/test/getdata';

$.ajax({
    url: url,
    dataType: 'jsonp',
    jsonp: 'callbackparam',
    jsonpCallback: 'callbackfunc',
    success: function (data) {
        console.log(data);
    }
});
```

但实际的成功回调还是走`success`方法，而不是`callbackfunc`？？


#### JSONP原理

利用在页面中创建`<script>`节点的方法向不同域提交HTTP请求的方法称为**JSONP**，这项技术可以解决跨域提交Ajax请求的问题

jsonp 的核心则是动态添加`<script>`标签来调用服务器提供的js脚本，允许用户传递一个`callback`参数给服务端，然后服务端返回数据时会将这个`callback`参数作为函数名来包裹住JSON数据，这样客户端就可以随意定制自己的函数来自动处理返回数据了

在同源策略下，在某个服务器下的页面是无法获取到该服务器以外的数据的，但 img、iframe、script 等标签是个例外，这些标签可以通过src属性请求到其他服务器上的数据。利用`<script>`标签的开放策略，我们可以实现跨域请求数据，当然，也需要服务端的配合。一般的ajax是不能跨域请求的，因此需要使用一种特别的方式来实现跨域，其中的原理是利用`<script>`元素的这个开放策略。


#### 实例

实例一：

在域名`example1.com`下。客户端的html文件。在声明回调函数`jsonpCallback`之后，客户端通过`script`标签向服务器跨域请求数据，然后服务端返回相应的数据并动态执行回调函数。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <script>
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


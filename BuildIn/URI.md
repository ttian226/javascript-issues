#### [encodeURIComponent()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)

把字符串作为 URI 组件进行编码，参数中的某些字符将被十六进制的转义序列进行替换。

    * 该方法不会对 ASCII 字母和数字进行编码，也不会对这些 ASCII 标点符号进行编码： - _ . ! ~ * ' ( ) 。其他字符（比如 ：;/?:@&=+$,# 这些用于分隔 URI 组件的标点符号），都是由一个或多个十六进制的转义序列替换的。

```javascript
var url = 'http://baidu.com';
var encodeUrl = encodeURIComponent(url);    //"http%3A%2F%2Fbaidu.com"
```

#### [decodeURIComponent()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURIComponent)

对 `encodeURIComponent()` 函数编码的 URI 进行解码。

```javascript
var url = 'http://baidu.com';
var encodeUrl = encodeURIComponent(url);    //"http%3A%2F%2Fbaidu.com"
decodeURIComponent(encodeUrl);  //'http://baidu.com'
```

#### [encodeURI()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURI)

把字符串作为 URI 进行编码

    * 该方法不会对 ASCII 字母和数字进行编码，也不会对这些 ASCII 标点符号进行编码： - _ . ! ~ * ' ( ) 。该方法的目的是对 URI 进行完整的编码，因此对以下在 URI 中具有特殊含义的 ASCII 标点符号，encodeURI() 函数是不会进行转义的：;/?:@&=+$,#

下面的例子，encodeURI只是把空格转换成了`%20`，其它字符并没有被编码。

```javascript
var url = 'http://baidu.com&a=123 abc';
var encodeUrl = encodeURI(url); //"http://baidu.com&a=123%20abc"
```

#### [decodeURI()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURI)

对 encodeURI() 函数编码过的 URI 进行解码

```javascript
var url = 'http://baidu.com&a=123 abc';
var encodeUrl = encodeURI(url); //"http://baidu.com&a=123%20abc"
decodeURI(encodeUrl);   //'http://baidu.com&a=123 abc'
```

encodeURIComponent和encodeURI的区别：

1. `encodeURI()`和`encodeURIComponent()`方法可以对URI (Uniform ResourceIdentifiers,通用资源标识符)进行编码，以便发送给浏览器。有效的URI中不能包含某些字符，例如空格。而这URI编码方法就可以对URI进行编码，它们用特殊的UTF-8编码替换所有无效的字符，从而让浏览器能够接受和理解。
2. 其中`encodeURI()`主要用于整个URI，而`encodeURIComponent()`主要用于对URI中的某一段进行编码。它们的主要区别在于，`encodeURI()`不会对本身属于URI的特殊字符进行编码，例如冒号、正斜杠、问号和井字号；而`encodeURIComponent()`则会对它发现的任何非标准字符进行编码。
3. 一般来说,我们使用`encodeURIComponent()`方法的时候要比使用`encodeURI()`更多，因为在实践中更常见的是对查询字符串参数而不是对基础URL进行编码。

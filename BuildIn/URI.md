#### [encodeURIComponent()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)

把字符串作为 URI 组件进行编码，参数中的某些字符将被十六进制的转义序列进行替换。

    * encodeURI()和encodeURIComponent()方法可以对URI (Uniform ResourceIdentifiers,通用资源标识符)进行编码，以便发送给浏览器。有效的URI中不能包含某些字符，例如空格。而这URI编码方法就可以对URI进行编码，它们用特殊的UTF-8编码替换所有无效的字符，从而让浏览器能够接受和理解。
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

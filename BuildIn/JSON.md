#### [JSON](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON)

JSON不支持IE6，IE7

##### [JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)

把js对象转换为json字符串

```javascript
JSON.stringify({ x: 5 });       // '{"x":5}'
JSON.stringify({ x: 5, y: 6 }); // '{"x":5,"y":6}' or '{"y":6,"x":5}'
```

##### [JSON.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)

把json字符串转换为js对象

```javascript
var jsonStr = JSON.stringify({ x: 5 });       // '{"x":5}'
var obj = JSON.parse(jsonStr);  //{x:5}
```

`JSON.parse()`等同于jQuery的`$.parseJSON()`

jquery源码：

```javascript
jQuery.parseJSON = function( data ) {
    return JSON.parse( data + "" );
};
```

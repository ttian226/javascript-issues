### [Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function)

##### [Function.length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/length)

返回函数参数的长度

```javascript
console.log(Function.length); /* 1 */
console.log((function()        {}).length); /* 0 */
console.log((function(a)       {}).length); /* 1 */
console.log((function(a, b)    {}).length); /* 2 etc. */
```

##### [Function.prototype.apply()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)


##### [Function.prototype.call()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)


##### [Function.prototype.toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/toString)

返回函数的字符串形式。*`toString()`重写了`Object.prototype.toString()`函数*

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

`apply`和`call`的用法参考[call和apply](https://github.com/ttian226/javascript-design-patterns/blob/master/call%E5%92%8Capply.md)

##### [Function.prototype.bind()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

`bind`会创建一个新的函数，`bind`的第一个参数作为这个新函数中this指向的对象。

`fun.bind(thisArg[, arg1[, arg2[, ...]]])`

* `thisArg`作为返回的函数中this指向的对象
* `arg1, arg2, ...`作为返回函数的参数

例子1：

```javascript
var getX = function() {
    return this.x;
};

window.x = 9;

var obj = {
    x: 81
};

// 直接调用getX()，this指向window
var x = getX(); //9

// 通过调用bind方法，返回一个函数，函数内部的this指向obj
var bindGetX = getX.bind(obj);
var x1 = bindGetX();    //81
```

例子2：

```javascript
window.x = 9;

var module = {
    x: 81,
    getX: function() {
        return this.x;
    }
};

// this指向module
var x1 = module.getX(); //81

var getX = module.getX;
// this指向window
var x2 = getX();    //9

// 通过bind方法，返回一个函数，函数中的this指向bind参数中的对象。这里为module对象
var boundGetX = getX.bind(module);
var x = boundGetX();    //81
```

例子3：bind带参数

```javascript
window.x = 9;

var add = function(y, z) {
    return this.x + y + z;
}

var obj = {x: 81};

var addY = add.bind(obj, 10, 20);
var sum = addY();   //81+10+20=111

// 等价于
var addY = add.bind(obj);
var sum = addY(10, 20); //111
```

例子4：

```javascript
function list() {
    return Array.prototype.slice.call(arguments);
}

var arr1 = list(1, 2, 3);    //[1, 2, 3]

var nlist = list.bind(undefined, 10);

var arr2 = nlist(); //[10] 等价nlist(10);
var arr3 = nlist(4, 5, 6);  //[10, 4, 5, 6] 等价nlist(10, 4, 5, 6)
```

例子5：

```javascript
var obj = {
    name: 'wangxu'
};

function getName(a, b, c, d) {
    var arr = [a, b, c, d];
    console.log(this.name);
    console.log(arr);
}

var func = getName.bind(obj, 1, 2);
func(3, 4);

// output
// 'wangxu'
// [1, 2, 3, 4]
```

##### [Function.prototype.toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/toString)

返回函数的字符串形式。*`toString()`重写了`Object.prototype.toString()`函数*

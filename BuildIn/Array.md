### [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)


#### 静态方法

##### [Array.isArray()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)

判断一个对象是否是数组

```javascript
var isArray = Array.isArray;

isArray([]);    //true
isArray({});    //false
```

#### 原型属性和方法（实例属性和方法）

##### [Array.prototype.length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/length)

返回数组长度

##### [Array.prototype.push()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)

从数组的尾部添加一个或多个元素，并返回这个数组的新的长度

例1：向数组添加新的元素

```javascript
var sports = ['soccer', 'baseball'];
var total = sports.push('football', 'swimming');

console.log(sports); // ['soccer', 'baseball', 'football', 'swimming']
console.log(total);  // 4
```

例2：使用`push`合并两个数组

```javascript
var vegetables = ['parsnip', 'potato'];
var moreVegs = ['celery', 'beetroot'];

// 使用apply合并两个数组
Array.prototype.push.apply(vegetables, moreVegs);
// 等同于：Array.prototype.push.call(vegetables, moreVegs[0], moreVegs[1]);
// 等同于：vegetables.push('celery', 'beetroot');
console.log(vegetables); // ['parsnip', 'potato', 'celery', 'beetroot']
```

##### [Array.prototype.pop()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)

删除数组最后一个元素，并返回这个元素

```javascript
var myFish = ['angel', 'clown', 'mandarin', 'sturgeon'];
var popped = myFish.pop();
console.log(myFish); // ['angel', 'clown', 'mandarin' ]
console.log(popped); // 'sturgeon'
```

##### [Array.prototype.shift()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)

从数组中删除第一个元素，并返回这个元素

```javascript
var myFish = ['angel', 'clown', 'mandarin', 'surgeon'];
var shifted = myFish.shift(); 

console.log(myFish);    //['clown', 'mandarin', 'surgeon'];
console.log(shifted);   //'angel'
```

##### [Array.prototype.unshift()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)

从数组的头部添加一个或多个元素，并返回这个数组的新的长度

```javascript
var arr = [1, 2];
var tot = arr.unshift(0);

console.log(arr);   //[0, 1, 2]
console.log(tot);   //3
```

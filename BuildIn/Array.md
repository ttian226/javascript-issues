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

**以下这些方法可以改变数组本身，包括：**
* `Array.prototype.push()`
* `Array.prototype.pop()`
* `Array.prototype.shift()`
* `Array.prototype.unshift()`
* `Array.prototype.reverse()`

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

##### [Array.prototype.reverse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)

翻转数组，使数组最后一个元素变成第一个元素，第一个元素变成最后一个元素。并返回这个数组的引用

```javascript
var myArray = ['one', 'two', 'three'];
var newArr = myArray.reverse();

console.log(myArray);   // ['three', 'two', 'one']
console.log(newArr);    // ['three', 'two', 'one']
console.log(newArr === myArray);    //true
```

##### [Array.prototype.sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

给数组中的元素重新排序，并返回这个数组

`arr.sort([compareFunction])`

`sort`接受一个排序函数，如果为空则按照数组中的元素的Unicode值进行排序。

例：参数为空时

```javascript
var fruit = ['cherries', 'apples', 'bananas'];
fruit.sort();
console.log(fruit);  //[ "apples", "bananas", "cherries" ]

var scores = [1, 10, 2, 21];
scores.sort();
// 结果并不是按照数字的大小排序，而是按照Unicode值由小到大排序。
console.log(scores); //[ 1, 10, 2, 21 ]
```

例：按照数组中数字由小到大排序

```javascript
var numbers = [4, 2, 5, 1, 3];

numbers.sort(function(a, b) {
    return a - b;
});

console.log(numbers);   //[ 1, 2, 3, 4, 5 ]
```

例：按照数组中数字由大到小排序

```javascript
var numbers = [4, 2, 5, 1, 3];

numbers.sort(function(a, b) {
    return b - a;
});

console.log(numbers);   //[ 5, 4, 3, 2, 1 ]
```

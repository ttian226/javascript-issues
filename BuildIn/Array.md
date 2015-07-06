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
* `Array.prototype.sort()`
* `Array.prototype.splice()`

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

比较函数`compareFunction(a, b)`定义如下：
* 如果`compareFunction(a, b)`返回值小于0，则a要排在b的前面
* 如果`compareFunction(a, b)`返回值大于0，则b要排在a的前面
* 如果`compareFunction(a, b)`返回值等于0，则a,b的排序没有变化

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

例：对数组中对象按照不同属性进行排序

```javascript
var items = [
    { name: 'Edward', value: 21 },
    { name: 'Sharpe', value: 37 },
    { name: 'And', value: 45 },
    { name: 'The', value: -12 },
    { name: 'Magnetic', value: 28 },
    { name: 'Zeros', value: 37 }
];

// 按照name的unicode值由小到大排序
var compareByName = function(a, b) {
    if (a.name > b.name) {
        return 1;
    }
    if (a.name < b.name) {
        return -1;
    }
    return 0;
};

// 按照value的值由小到大排序
var compareByValue = function(a, b) {
    if (a.value > b.value) {
        return 1;
    }
    if (a.value < b.value) {
        return -1;
    }
    return 0;
};

items.sort(compareByName);
items.sort(compareByValue);
```

##### [Array.prototype.splice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

改变数组，删除一个数组中已经存在的元素或增加新的元素。

`array.splice(start, deleteCount[, item1[, item2[, ...]]])`

* `start` 改变数组的起始索引，从0开始。
* `deleteCount` 要删除的元素个数
* `itemN` 要增加的元素

例：删除元素

```javascript
var myFish = ['angel', 'clown', 'mandarin', 'surgeon'];

// 从索引1位置开始删除2个元素，即'clown'和'mandarin'
myFish.splice(1, 2);
console.log(myFish);    //[ "angel", "surgeon" ]
```

```javascript
var myFish = ['angel', 'clown', 'mandarin', 'surgeon'];

// 第二个参数为0，不删除任何元素
myFish.splice(1, 0);
console.log(myFish);    //[ "angel", "clown", "mandarin", "surgeon" ]
```

```javascript
var myFish = ['angel', 'clown', 'mandarin', 'surgeon'];

// 第二个参数如果大于等于剩余长度（这里>=3），删除余下的所有元素
myFish.splice(1, 3);
console.log(myFish);    //[ "angel" ]
```

例：增加新元素

```javascript
var myFish = ['angel', 'clown', 'mandarin', 'surgeon'];

// 从索引位置2插入一个元素'drum'，原来从索引2开始的元素依次向后移动
myFish.splice(2, 0, 'drum');
console.log(myFish);    //[ "angel", "clown", "drum", "mandarin", "surgeon" ]
```

```javascript
var myFish = ['angel', 'clown', 'mandarin', 'surgeon'];

// 从位置2删除一个元素'mandarin'，并在位置2插入一个新元素'trumpet'
removed = myFish.splice(2, 1, 'trumpet');
console.log(myFish);    //[ "angel", "clown", "trumpet", "surgeon" ]
```

```javascript
var myFish = ['angel', 'clown', 'mandarin', 'surgeon'];

// 从位置0删除两个元素'angel','clown'，并在位置0插入3个新元素'parrot', 'anemone', 'blue'
removed = myFish.splice(0, 2, 'parrot', 'anemone', 'blue');
console.log(myFish);    //[ "parrot", "anemone", "blue", "mandarin", "surgeon" ]
```

##### [Array.prototype.join()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join)

把数组中的元素用分隔符连接起来，并返回一个字符串。

`str = arr.join([separator = ','])`

*如果不指定参数，默认为','*

```javascript
var a = ['Wind', 'Rain', 'Fire'];

// 参数为空，默认使用','连接
var myVar1 = a.join();  //"Wind,Rain,Fire"
var myVar2 = a.join(', ');  //"Wind, Rain, Fire"
var myVar3 = a.join('');    //"WindRainFire"
```

##### [Array.prototype.concat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)

合并多个数组，并返回一个新数组

`var new_array = old_array.concat(value1[, value2[, ...[, valueN]]])`


```javascript
var alpha = ['a', 'b', 'c'],
    numeric = [1, 2, 3];

var alphaNumeric = alpha.concat(numeric);
console.log(alphaNumeric);  //[ "a", "b", "c", 1, 2, 3 ]

// 不会改变原有数组
console.log(alpha);     //['a', 'b', 'c']
console.log(numeric);   //[1, 2, 3]
```

```javascript
var num1 = [1, 2, 3],
    num2 = [4, 5, 6],
    num3 = [7, 8, 9];

var nums = num1.concat(num2, num3);
console.log(nums); //[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

##### [Array.prototype.slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

取得数组中的一部分元素，并返回这些元素组成的新的数组。

`arr.slice([begin[, end]])`

```javascript
var fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango'];

// 从数组第一个索引的元素开始截取直到第3个索引位置
var citrus = fruits.slice(1, 3);
console.log(citrus);    //[ "Orange", "Lemon" ]
```

例：把类数组对象转化为数组

```javascript
var slice = Array.prototype.slice;
var arr1 = [1, 2, 3, 4, 5];

var arr2 = slice.call(arr1, 0, 3);
console.log(arr2);  //[1, 2, 3]

// arr3是个类数组对象
var arr3 = {0: "a", 1: "b", 2: "c", length: 3, o: "other"};
var arr4 = slice.call(arr3);
console.log(arr4);  //['a', 'b', 'c']
```

```javascript
var slice = Array.prototype.slice;

function list() {
    return slice.call(arguments, 0);
}

var list1 = list(1, 2, 3);
console.log(list1); // [1, 2, 3]
```

##### [Array.prototype.toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toString)

返回数组的字符串形式

```javascript
var monthNames = ['Jan', 'Feb', 'Mar', 'Apr'];
var myVar = monthNames.toString();
console.log(myVar);     //"Jan,Feb,Mar,Apr"
```

##### [Array.prototype.indexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)

返回指定元素在数组中的第一个索引值，如果没有找到指定元素返回-1

`arr.indexOf(searchElement[, fromIndex = 0])`

* `searchElement` 要查找的元素
* `fromIndex` 起始索引，默认为0

```javascript
var array = [2, 5, 9, 2];
// 由于数组元素2第一个出现的位置是0，所以indexOf返回0
array.indexOf(2);   //0
```

```javascript
var array = [2, 5, 9];

// 从默认索引位置0查找元素2，找到元素返回元素索引位置
array.indexOf(2);     // 0

// 从默认索引位置0查找元素7，找不到元素返回-1
array.indexOf(7);     // -1

// 从索引位置2查找元素9
array.indexOf(9, 2);  // 2

// 从索引位置-1查找元素2，-1位置是数组最右的一个元素，相当于array.indexOf(2, 2)
array.indexOf(2, -1); // -1

// 从索引位置-3查找元素2，-3位置是数组的第一个元素，相当于array.indexOf(2, 0)
array.indexOf(2, -3); // 0
```

##### [Array.prototype.lastIndexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf)

返回指定元素在数组中最后一个索引值，如果没有找到指定元素返回-1。**从索引位置反向查找元素**

`arr.lastIndexOf(searchElement[, fromIndex = arr.length - 1])`

* `searchElement` 要查找的元素
* `fromIndex` 起始索引，默认为arr.length - 1

```javascript
var array = [2, 5, 9, 2];

// 从默认索引位置3反向查找元素2，由于数组元素2最后一个出现的位置是3，所以lastIndexOf返回3
array.lastIndexOf(2);     //3

// 从默认索引位置3反向查找元素7，未找到元素7，返回-1
array.lastIndexOf(7);     // -1

// 从位置3反向查找元素2
array.lastIndexOf(2, 3);  // 3

// 从位置2反向查找元素2
array.lastIndexOf(2, 2);  // 0

// 从位置-2反向查找元素2
array.lastIndexOf(2, -2); // 0

// 从位置-1反向查找元素2
array.lastIndexOf(2, -1); // 3
```


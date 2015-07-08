### [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)

#### 属性

##### [String.length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/length)

返回字符串的长度

```javascript
var x = 'Mozilla';
var empty = '';

console.log('Mozilla is ' + x.length + ' code units long');
/* "Mozilla is 7 code units long" */

console.log('The empty string has a length of ' + empty.length);
/* "The empty string has a length of 0" */
```

#### 方法

##### [String.prototype.charAt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/charAt)

返回字符串中指定的字符

`str.charAt(index)`

* `index`为从0开始的索引值，字符串最后一个字符的索引为`str.length-1`，如果索引值超界则返回空。

```javascript
var anyString = 'Brave new world';

console.log("The character at index 0   is '" + anyString.charAt(0)   + "'");
console.log("The character at index 1   is '" + anyString.charAt(1)   + "'");
console.log("The character at index 2   is '" + anyString.charAt(2)   + "'");
console.log("The character at index 3   is '" + anyString.charAt(3)   + "'");
console.log("The character at index 4   is '" + anyString.charAt(4)   + "'");
console.log("The character at index 999 is '" + anyString.charAt(999) + "'");

// The character at index 0   is 'B'
// The character at index 1   is 'r'
// The character at index 2   is 'a'
// The character at index 3   is 'v'
// The character at index 4   is 'e'
// The character at index 999 is ''
```

##### [String.prototype.concat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/concat)

合并字符串，并返回一个新的字符串

`str.concat(string2, string3[, ..., stringN])`

* `string2...stringN`为要合并的字符串

```javascript
var hello = 'Hello, ';
console.log(hello.concat('Kevin', ' have a nice day.'));

/* Hello, Kevin have a nice day. */
```

##### [String.prototype.indexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf)

查找字符串第一次出现的位置（从左向右），如果找不到则返回-1

`str.indexOf(searchValue[, fromIndex])`

* `searchValue` 要检索的字符串
* `fromIndex` 检索的起始位置（默认为0），如果`fromIndex >= str.length`则返回-1（除非要检索的字符串为空，这时返回字符串的长度）

```javascript
'Blue Whale'.indexOf('Blue');     // returns  0
'Blue Whale'.indexOf('Blute');    // returns -1
'Blue Whale'.indexOf('Whale', 0); // returns  5
'Blue Whale'.indexOf('Whale', 5); // returns  5

// 检索字符串为空，起始索引小于字符串长度，返回起始索引，这里返回9
'Blue Whale'.indexOf('', 9);      // returns  9

// 起始索引大于等于字符串长度，并且检索字符串为空，这时返回字符串长度10
'Blue Whale'.indexOf('', 10);     // returns 10
'Blue Whale'.indexOf('', 11);     // returns 10
```

##### [String.prototype.lastIndexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/lastIndexOf)

逆向查找字符串第一次出现的位置（从右向左），如果找不到则返回-1

`str.lastIndexOf(searchValue[, fromIndex])`

* `searchValue` 要检索的字符串
* `fromIndex` 检索的起始位置（默认为str.length）

```javascript
// 从字符串的尾部从右向左查找'a',如果查到则返回，第一个出现'a'的位置是3
'canal'.lastIndexOf('a');     // returns 3

// 从位置2'n'向左查找'a'，第一个出现'a'的位置是1
'canal'.lastIndexOf('a', 2);  // returns 1

// 从位置0'c'向左查找'a'，找不到'a'则返回-1
'canal'.lastIndexOf('a', 0);  // returns -1

// 从字符串的尾部从右向左查找'x'，没有找到返回-1
'canal'.lastIndexOf('x');     // returns -1
```

##### [String.prototype.match()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match)

执行正则匹配

`str.match(regexp)`

* `regexp` 正则表达式
* 返回值，包括匹配结果的一个数组，如果匹配不到返回null

例：

```javascript
var str = 'For more information, see Chapter 3.4.5.1';
var re = /(chapter \d+(\.\d)*)/i;
var found = str.match(re);

// 第2，3个元素为捕获的分组信息
console.log(found);     //["Chapter 3.4.5.1", "Chapter 3.4.5.1", ".1"]
```

例：全局匹配，忽略大小写

```javascript
var str = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
var regexp = /[A-E]/gi;
var matches_array = str.match(regexp);

console.log(matches_array);
// ['A', 'B', 'C', 'D', 'E', 'a', 'b', 'c', 'd', 'e']
```

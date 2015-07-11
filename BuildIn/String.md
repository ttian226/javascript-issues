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

##### [String.prototype.charCodeAt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt)

返回字符串中指定位置字符的Unicode的十进制值

```javascript
// 'A'的UNICODE编码十进制值是65  
'ABC'.charCodeAt(0); // returns 65

// 如果index超出范围，返回NaN
'ABC'.charCodeAt(-1); // returns NaN
'ABC'.charCodeAt(10); // returns NaN

// 参数可以转换为数值，'0'转换为0
'ABC'.charCodeAt('0'); // returns 65

// 参数不能转换为数值，参数默认为0。这里'b'不能转换为数值，按0处理
'ABC'.charCodeAt('b'); // returns 65
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

##### [String.prototype.replace()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace)

替换字符串

`str.replace(regexp|substr, newSubStr|function[, flags])`

* `regexp`正则表达式
* `substr`子字符串
* `newSubStr`要替换的新字符串，或者是包含分组信息（参考反向引用的例子）

例：替换字符串

```javascript
var newstr = 'hello world!'.replace('world', 'javascript');
console.log(newstr);    //hello javascript!
```

例：用正则表达式替换匹配的字符串

```javascript
var re = /apples/gi;
var str = 'Apples are round, and apples are juicy.';
var newstr = str.replace(re, 'oranges');
console.log(newstr);    // oranges are round, and oranges are juicy.
```
例：使用反向引用

```javascript
var re = /(\w+)\s(\w+)/;
var str = 'John Smith';
// $1,$2为对应的分组信息
var newstr = str.replace(re, '$1, $2');
console.log(newstr);
```

例：第二个参数为回调函数

* `match`正则表达式匹配到的字符串
* `p1-p3`捕获的分组字符串
* `offset`匹配到的字符串的第一个索引
* `string`原字符串

```javascript
'0123abc12345#$*%'.replace(/([^\d]+)(\d*)([^\w]*)/, replacer);

// 这里匹配到的字符串是'abc12345#$*%',offset是4，因为匹配的字符串的第一个字符'a'所在字符串的索引是4
function replacer(match, p1, p2, p3, offset, string) {
    console.log(arguments);
}

//["abc12345#$*%", "abc", "12345", "#$*%", 4, "0123abc12345#$*%"]
```

##### [String.prototype.search()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/search)

字符串搜索，参数为一个正则表达式，如果查找到返回第一个匹配的字符串的索引值，否则返回-1

`str.search(regexp)`

```javascript
var re = /apples/gi;
var str = 'Apples are round, and apples are juicy.';
var r = str.search(re);
console.log(r);     //0 第一个查找匹配的'apple'的索引为0
```

例：检测字符串中是否包含匹配的子字符串

```javascript
function testinput(re, str) {
    var midstring;
    if (str.search(re) !== -1) {
        midstring = ' contains ';
    } else {
        midstring = ' does not contain ';
    }
    console.log(str + midstring + re);
}

var str = 'Apples are round, and apples are juicy.';
var re = /apples/gi;
testinput(re, str);
```

##### [String.prototype.slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice)

切割字符串，返回一个新的字符串

`str.slice(beginSlice[, endSlice])`

* `beginSlice`起始位置
* `endSlice`结束位置，不设置就截取到字符串的结尾

```javascript
var str1 = 'The morning is upon us.';

// 省略endSlice参数，截取从位置4开始到字符串结尾的字符串
var str2 = str1.slice(4);
console.log(str2);  //morning is upon us.
```

```javascript
var str1 = 'The morning is upon us.';

// 截取从位置4开始到位置11的字符串
var str2 = str1.slice(4, 11);
console.log(str2);  //morning
```

```javascript
var str1 = 'The morning is upon us.';

// -1位置是字符串最后一个字符的位置
var str2 = str1.slice(4, -1);
console.log(str2);  //morning is upon us
```

```javascript
var str1 = 'The morning is upon us.';

// -2位置是字符串倒数第二字符的位置
var str2 = str1.slice(4, -2);
console.log(str2);  //morning is upon u
```

##### [String.prototype.substr()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substr)

返回字符串的一部分

`str.substr(start[, length])`

* `start`起始位置
* `length`截取长度

例：

```javascript
var str = 'abcdefghij';

// 从位置1截取2个字符
str.substr(1, 2);  //bc

// 从倒数第3个字符开始截取2个字符
str.substr(-3, 2);  //hi

// 从倒数第3个字符开始截取到字符串的末尾
str.substr(-3);     //hij

// 从位置1截取到字符串的末尾
str.substr(1);      //bcdefghij

// 由于20>str.length，-20从位置0开始截取2个字符
str.substr(-20, 2); //ab

// 由于20>str.length，字符串返回空
str.substr(20, 2);  //''
```

##### [String.prototype.toLowerCase()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase)

字符串大写转换成小写

```javascript
var str = 'ALPHABET'.toLowerCase();
console.log(str);   //alphabet
```

##### [String.prototype.toUpperCase()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase)

字符串小写转换成大写

```javascript
var str = 'alphabet'.toUpperCase();
console.log(str);   //ALPHABET
```

##### [String.prototype.toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toString)

把字符串对象转换为字符串

```javascript
var str = new String('hello world');
console.log(str.toString());    //hello world
```

##### [String.prototype.valueOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/valueOf)

返回字符串对象的原始值，这个值等于`String.prototype.toString()`返回的值

```javascript
var x = new String('Hello world');
console.log(x.valueOf()); // Displays 'Hello world'
```

##### [String.prototype.trim()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/Trim)

去除字符串两端的空白

```javascript
var orig = '   foo  ';
console.log(orig.trim()); // 'foo'
```

##### [String.prototype.split()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split)

把字符串分割成字符串数组

`str.split([separator[, limit]])`

* `separator`分隔字符串或正则表达式
* `limit`限制返回数组的最大长度

例：用空格分隔字符串

```javascript
var str = 'Oh brave new world that has such people in it.';
var arr = str.split(' ');
console.log(arr);   //["Oh", "brave", "new", "world", "that", "has", "such", "people", "in", "it."]
```

例：用逗号分隔字符串

```javascript
var str = 'Jan,Feb,Mar,Apr,May,Jun,Jul,Aug,Sep,Oct,Nov,Dec';
var arr = str.split(',');
console.log(arr);   //["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]
```
例：用正则表达式分隔字符串

```javascript
var str = 'Harry Trump ;Fred Barney; Helen Rigby ; Bill Abel ;Chris Hand ';
var arr = str.split(/\s*;\s*/);
console.log(arr);   //["Harry Trump", "Fred Barney", "Helen Rigby", "Bill Abel", "Chris Hand "]
```

例：使用第二个参数限制限制数组长度

```javascript
var str = 'Oh brave new world that has such people in it.';
var arr = str.split(' ', 3);
console.log(arr);   //["Oh", "brave", "new"]
```

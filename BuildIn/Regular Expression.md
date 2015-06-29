#### Regular expression flags

Flag | Description
-----|------------
g|Global search
i|Case-insensitive search
m|Multi-line search

* *g 全局搜索，默认搜索到第一个匹配立刻停止*
* *i 忽略大小写，默认大小写敏感*

To include a flag with the regular expression, use this syntax:

`var re = /pattern/flags;`

*or*

`var re = new RegExp("pattern", "flags");`


*javascript创建正则表达式两种方式*

```javascript
var re1 = new RegExp('abc', 'g');

// equal to
var re2 = /abc/g;

console.log(re2 instanceof RegExp); //true
```

*完全匹配：*

```javascript
var re = /abc/;
var str = 'abc';

var res = re.test(str);
var arr = re.exec(str);

console.log(res);   //true
console.log(arr);   //['abc']
```

*匹配字符串中的一部分：*

```javascript
var re = /abc/;
var str = '123abcdefg';

var res = re.test(str);
var arr = re.exec(str);

console.log(res);   //true
console.log(arr);   //['abc']
```

*找不到匹配：*

```javascript
var re = /abc/;
var str = 'ab';

var res = re.test(str);
var arr = re.exec(str);

console.log(res);   //false
console.log(arr);   //null
```

*不使用i匹配，默认大小写敏感：*

```javascript
var re = /abc/;
var str = 'ABC';

var res = re.test(str);
var arr = re.exec(str);

console.log(res);   //false
console.log(arr);   //null
```

*使用i匹配，忽略大小写：*

```javascript
var re = /abc/i;
var str = 'ABC';

var res = re.test(str);
var arr = re.exec(str);

console.log(res);   //true
console.log(arr);   //['ABC']
```

*使用g匹配：*

```javascript
var re = /abc/g;
var str = 'abc';

console.log(re.lastIndex);  //0

var res = re.test(str); //or re.exec(str)

console.log(re.lastIndex);  //3
```

*不使用g匹配：*

```javascript
var re = /abc/;
var str = 'abc';

console.log(re.lastIndex);  //0

var res = re.test(str); //or re.exec(str)

console.log(re.lastIndex);  //0
```

使用全局模式g匹配时，如果使用`.test()`或`.exec()`方法匹配时，每次匹配到一个字符串后，`lastIndex`值会被更新，如果不使用g匹配，索引值`lastIndex`不会更新。

```javascript
var re = /abc/;
var str = 'abc123abc456abc';

//未使用全局匹配时，只匹配到了第一个abc即终止
var arr = re.exec(str);

console.log(arr);   //['abc']
console.log(re.lastIndex);  //0
```

```javascript
var re = /abc/g;
var str = 'abc123abc456abc';

//使用全局匹配时，只匹配到了第一个abc即终止
var arr = re.exec(str);

console.log(arr);   //['abc']
console.log(re.lastIndex);  //3，此时lastIndex指向字符串中的'1'
```

*遍历所有匹配：*

```javascript
var re = /abc/g;
var str = 'abc123abc456abc';
var arr, list = [];

while ( (arr = re.exec(str)) ) {
    console.log(arr);
    console.log(re.lastIndex);
    list.push(arr[0]);
}

console.log(list);

// output
// ['abc']
// 3
// ['abc']
// 9
// ['abc']
// 15
// ['abc', 'abc', 'abc']
```

#### Special characters in regular expressions

##### 预定义特殊字符

Character | Meaning
----------|--------
\t|Matches a tab
\r|Matches a carriage return(回车)
\n|Matches a line feed(换行)


*匹配水平制表符*

```javascript
var re = /\t/;
var str = 'abc\tdef';

var res = re.test(str);
var arr = re.exec(str);

console.log(res);   //true
console.log(arr);   //['       ']
```

*匹配回车*

```javascript
var re = /\r/;
var str = 'abc\rdef';

var res = re.test(str); //true
```

*匹配换行*

```javascript
var re = /\n/;
var str = 'abc\ndef';

var res = re.test(str); //true
```

##### 集合

Character | Meaning
----------|--------
[xyz]|Character set.
[^xyz]|A negated or complemented character set.

[xyz] 包含x,y,z任意一个字符的集合
[a-d] 等价于[abcd]，或[a-zA-Z0-9]匹配a-z,A-Z,0-9
[^xyz] 不包含x,y,z任意一个字符

```javascript
var re = /[xyz]/;
var str = 'ax';
var arr = re.exec(str);
console.log(arr);   //['x']
```

```javascript
var re = /[^xyz]/;
var str = 'ax';
var arr = re.exec(str);
console.log(arr);   //['a']
```

##### 预定义类

Character | Meaning
----------|--------
**.**|matches any single character except the newline character.

**.**匹配除了回车和换行之外的所有字符，等价于[^\r\n]

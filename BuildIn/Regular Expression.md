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

*遍历所有匹配*

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

Character | Meaning
----------|--------
\t|Matches a tab
\r|Matches a carriage return(回车)
\n|Matches a line feed(换行)




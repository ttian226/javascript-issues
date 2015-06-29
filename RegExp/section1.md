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

* [xyz] 包含x,y,z任意一个字符的集合
* [a-d] 等价于[abcd]，或[a-zA-Z0-9]匹配a-z,A-Z,0-9
* [^xyz] 不包含x,y,z任意一个字符
* [a-z.] 如果方括号中包含`.`，仅仅匹配一个`.`而不是量词的`.`

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

*匹配集合中的`.`*

```javascript
var re = /[a-z.]+/;     //或 var re = /[\w.]+/
var str = 'test.i.ng';
var arr = re.exec(str);
console.log(arr);   //['test.i.ng']
```

##### 量词

Character | Meaning
----------|--------
`?`|Matches the preceding character 0 or 1 time. Equivalent to {0,1}.
`+`|Matches the preceding character 1 or more times. Equivalent to {1,}.
`*`|Matches the preceding character 0 or more times. Equivalent to {0,}.
{n}|Matches exactly n occurrences of the preceding character. N must be a positive integer.
{n,m}|Matches at least n and at most m occurrences of the preceding character.When m is omitted, it's treated as ∞.

* `{n}`匹配n次
* `{n,m}`匹配n到m次
* `{n,}`最少匹配n次
* `{,m}`最多匹配m次

*关于{n}的例子：*

```javascript
var re = /a{2}/;
var str = 'a';

//由于'a'只出现1次，所以无法匹配exec返回null
var arr = re.exec(str);

console.log(arr);   // null
```

```javascript
var re = /a{2}/;
var str = 'aa';

//'a'连续出现两次，匹配'aa'
var arr = re.exec(str);

console.log(arr);   // ['aa']
```

```javascript
var re = /a{2}/;
var str = 'aaa';

//'a'连续出现3次，也只能匹配两个'a'
var arr = re.exec(str);

console.log(arr);   // ['aa']
```

*关于{n,m}的例子*

```javascript
var re = /a{2,5}/;
var str1 = 'a';
var str2 = 'aa';
var str3 = 'aaaaa';
var str4 = 'aaaaaa';

var arr1 = re.exec(str1);   //匹配不到
var arr2 = re.exec(str2);   //可以匹配到'aa'
var arr3 = re.exec(str3);   //可以匹配到'aaaaa'
var arr4 = re.exec(str4);   //最多只能匹配到5个a

console.log(arr1);  //null
console.log(arr2);  //['aa']
console.log(arr3);  //['aaaaa']
console.log(arr4);  //['aaaaa']
```


*匹配0或1个a*

```javascript
var re = /a?/;
var str = 'a';

// 匹配到了1个'a'
var res = re.test(str);
var arr = re.exec(str);

console.log(res);   // true
console.log(arr);   // ['a']
```

```javascript
var re = /a?/;
var str = '';

// 匹配到了0个'a'
var res = re.test(str);
var arr = re.exec(str);

console.log(res);   // true
console.log(arr);   // ['']
```

```javascript
var re = /a+/;
var str = 'aaabc';

// 最多匹配1个'a'
var arr = re.exec(str);

console.log(arr);   // ['a']
```

*匹配1或多个a*

```javascript
var re = /a+/;
var str = 'abc';

// 匹配到了1个'a'
var arr = re.exec(str);

console.log(arr);   // ['a']
```

```javascript
var re = /a+/;
var str = 'aaabc';

// 匹配到了多个'a'
var arr = re.exec(str);

console.log(arr);   // ['aaa']
```

*集合+量词*

```javascript
var re = /[a-z]?/;
var str = 'aaabc';

// 匹配到了一个'a'
var arr = re.exec(str);

console.log(arr);   // ['a']
```

```javascript
var re = /[a-z]+/;
var str = 'aaabc';

// 匹配整个字符串
var arr = re.exec(str);

console.log(arr);   // ['aaabc']
```

```javascript
var re = /[a-z]?/;
var str = 'ABCdef';

// 匹配0或1次集合中字符，由于第一个字符不在集合中，所以匹配到了空字符（0个）
var arr = re.exec(str);

console.log(arr);   // ['']
```

```javascript
var re = /[a-z]?/;
var str = 'abcABCdef';

// 匹配0或1次集合中字符，由于第一个字符在集合中，所以最多匹配了一个字符'a'
var arr = re.exec(str);

console.log(arr);   // ['a']
```

```javascript
var re = /[a-z]+/;
var str = 'ABCdefGHijk';

// 匹配1或多次集合中字符，在字符串中找到了最先出现的匹配'def'
// 优先匹配多个字符'def'，而不是1个字符'd'
var arr = re.exec(str);

console.log(arr);   // ['def']
```

```javascript
var re = /[a-z]+/;
var str = 'aABCdefGHijk';

// 匹配1或多次集合中字符，在字符串中找到了最先出现的匹配'a'
// 由于接下来的是'A'所以停止匹配
var arr = re.exec(str);

console.log(arr);   // ['a']
```

```javascript
var re = /[a-z]*/;
var str = 'ABCdefGHijk';

// 匹配0或多次集合中字符，由于第一个字符不在集合中，所以匹配到了空字符（0个）
var arr = re.exec(str);

console.log(arr);   // ['']
```

```javascript
var re = /[a-z]*/;
var str = 'abcABCdefGHijk';

// 匹配0或多次集合中字符，由于前面的3个字符'abc'在集合中，所以匹配到了'abc'
var arr = re.exec(str);

console.log(arr);   // ['abc']
```

##### 预定义类

Character | Meaning
----------|--------
`.`|matches any single character except the newline character.
\d|Matches a digit character. Equivalent to [0-9].
\D|Matches any non-digit character. Equivalent to [^0-9].
\s|Matches a single white space character, including space, tab, form feed, line feed（空白符）
\S|Matches a single character other than white space（非空白符）
\w|Matches any alphanumeric character including the underscore. Equivalent to [A-Za-z0-9_].
\W|Matches any non-word character. Equivalent to [^A-Za-z0-9_].

`.`匹配除了回车和换行之外的所有字符，等价于[^\r\n]

*返回用空白符分隔的字符串组成的数组：*

```javascript
var re = /\S+/g;
var str = 'abc def ghi';
var arr = str.match(re);
console.log(arr);   //['abc', 'def', 'ghi']
```

* 使用`\.`匹配`.`例如：

```javascript
/[a-z]\.[0-9]/.test('a.9');     //true
```

* 使用`\/`匹配`/`例如：

```javascript
/\//.test('/');     //true
/\/+/.test('//');   //true
```

* 使用`\\`匹配`\`例如：

```javascript
/\\/.test('\\');        //true 匹配一个'\'
/^\\{2}$/.test('\\\\');   //true 匹配两个'\'
```

##### 边界

Character | Meaning
----------|--------
`^`|Matches beginning of input.
`$`|Matches end of input.
\b|Matches a word boundary
\B|Matches a non-word boundary


```javascript
/abc/.test('123abc');    //true 匹配到abc
/^abc/.test('123abc');   //false 在字符串起始位置未匹配到
/abc/.test('abc123');    //true 匹配到abc

/abc/.test('abc123');   //true  
/abc$/.test('abc123');  //false
/abc$/.test('123abc');  //true
```

* `\b`匹配单词边界，指[A-Za-z0-9_]之外的字符
* `\B`匹配非单词边界

```javascript
// 不使用边界\b匹配
var arr1 = '-12w-eefd&efrew'.match(/[\w-]+/g);

// 由于[\w-]包含'-'，所以匹配出的第一个字符串为'-12w-eefd'
console.log(arr1);   //["-12w-eefd", "efrew"]

// 使用边界\b匹配
var arr2 = '-12w-eefd&efrew'.match(/\b[\w-]+\b/g);

// 从第一个[A-Za-z0-9_]之外的字符开始匹配，即从'-'作为起始点匹配，所以第一个匹配出的字符串不包含'-'，为'12w-eefd'
console.log(arr2);   //["12w-eefd", "efrew"]
```

##### 贪婪模式和惰性模式

惰性模式匹配是在量词后面加`?`

```javascript
// 默认情况下为贪婪匹配，{3,5}优先从最大值5匹配
'123456789'.match(/\d{3,5}/g);  //["12345", "6789"]

// 在量词后面添加?为惰性匹配，{3,5}优先从最小值3匹配，如果匹配到则终止匹配
'123456789'.match(/\d{3,5}?/g); //["123", "456", "789"]
```

```javascript
// 贪婪匹配，匹配到整个字符串
'abbbcbbb'.match(/.*bbb/g); //["abbbcbbb"]

// 惰性匹配，当匹配到第一个'bbb'即停止匹配
'abbbcbbb'.match(/.*?bbb/g); //["abbb", "cbbb"]
```

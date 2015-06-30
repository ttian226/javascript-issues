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


```javascript
/abc/.test('123abc');    //true 匹配到abc
/^abc/.test('123abc');   //false 在字符串起始位置未匹配到
/abc/.test('abc123');    //true 匹配到abc

/abc/.test('abc123');   //true  
/abc$/.test('abc123');  //false
/abc$/.test('123abc');  //true
```

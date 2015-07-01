#### 预定义类

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

* 使用`\|`匹配`|`例如：

```javascript
/\|/.test('|');        //true
```

#### 边界

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

#### 贪婪模式和惰性模式

* 惰性模式匹配是在量词后面加`?`

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

```javascript
// 贪婪匹配，同时匹配了2个p
"<p></p>".match(/<(.|\s)*>/);   //["<p></p>", "p"]

// 惰性匹配，只匹配了第一个p
"<p></p>".match(/<(.|\s)*?>/);  //["<p>", "p"]

// 通过惰性+全局，匹配每个html标签
"<p></p>".match(/<(.|\s)*?>/g); //["<p>", "</p>"]

// 替换所有的<p>标签，只保留文本
"<p>hello world</p>".replace(/<(.|\s)*?>/g, '');    //'hello world'
```

#### 或

Character | Meaning
----------|--------
`x|y`|Matches either 'x' or 'y'.

```javascript
/a|b/.test('a');    //true 只匹配a或b任一个字符
/a|b/.test('c');    //false
```

```javascript
/[a|b]/.test('|');  //true 在集合中'|'不代表或，只代表字符'|'
```

```javascript
/(a|b|c)+/.test('a');   //true 可以在分组中使用'|'
```

#### 分组匹配

Character | Meaning
----------|--------
`(x)`|Matches 'x' and remembers the match

使用`()`进行分组匹配

```javascript
/(foo){3}/.test('foofoofoo');   //true 连续匹配'foo'3次
```

* 使用`exec()`，返回的数组的第0个元素存储匹配的字符串，从第1个元素开始依次存储分组字符串

```javascript
// 第0个元素为匹配后的字符串"foofoofoo"，第1个元素存储分组字符串"foo"
/(foo){3}/.exec('foofoofoo');   //["foofoofoo", "foo"]

// 第1，2个元素分别存储'foo','bar'
/(foo){1}(bar){2}/.exec('foobarbar');   //["foobarbar", "foo", "bar"]
```

* 使用`String.prototype.match()`

不使用`g`匹配，返回的数组的第0个元素存储匹配的字符串，从第1个元素开始依次存储分组字符串，同`exec()`的返回结果

```javascript
'foobarbar'.match(/(foo){1}(bar){2}/);  //["foobarbar", "foo", "bar"]

'abc123abcabc456abc'.match(/(abc)+/);   //["abc", "abc"]
```

使用`g`匹配，match返回的数组只存储匹配的字符串

```javascript
'foobarbar'.match(/(foo){1}(bar){2}/g);  //["foobarbar"]

'abc123abcabc456abc'.match(/(abc)+/g);   //["abc", "abcabc", "abc"]
```

**虽然使用`g`匹配，match的结果没有保存分组信息，但实际上还是捕获到了分组信息，如：**

```javascript
'foobarbar'.match(/(foo){1}(bar){2}/g);     //["foobarbar"]

// 通过反向引用查看捕获的分组信息
console.log(RegExp.$1);     //'foo'
console.log(RegExp.$2);     //'bar'
```

分组匹配的一些例子：

```javascript
'a'.match(/(a)?/);  //['a', 'a']，匹配到了'a'
'a'.match(/(a)?/g); //['a', '']，匹配到了'a'和''
'aa'.match(/(a)?/); //['a', 'a']，匹配到了第一个'a'
'aa'.match(/(a)?/g);//['a', 'a', '']，匹配到了第一个'a'，第二个'a'，和''

'a'.match(/(a)+/);  //['a', 'a']，匹配到了'a'
'a'.match(/(a)+/g); //['a']，只匹配到了'a'
'aa'.match(/(a)+/); //['aa', 'a']，匹配了'aa'
'aa'.match(/(a)+/g);//['aa']，只匹配到了'aa'

'a'.match(/(a)*/);  //['a', 'a']，匹配到了'a'
'a'.match(/(a)*/g); //['a', '']，匹配到了'a'和''
'aa'.match(/(a)*/); //['aa', 'a']，匹配了'aa'
'aa'.match(/(a)*/g);//['aa', '']，匹配到了'aa'和''

// 第二个参数为最后一次匹配的分组'dad'
'baddad'.match(/([bd]ad?)*/);   //["baddad", "dad"]
'baddad'.match(/([bd]ad?)*/g);  //["baddad", ""]

// 匹配到了ab，第1个元素为最外层分组'ab'，第2个元素为内层分组'b'
'ab'.match(/(a(b)?)/);  //['ab', 'ab', 'b']
```

#### 反向引用

* 使用`RegExp.$n`

```javascript
/(foo){3}/.exec('foofoofoo');   //["foofoofoo", "foo"]
console.log(RegExp.$1);     //'foo'

/(foo){1}(bar){2}/.exec('foobarbar');   //["foobarbar", "foo", "bar"]
console.log(RegExp.$1);     //'foo'
console.log(RegExp.$2);     //'bar'
```
* 在正则表达式中使用`\n`

```javascript
/(foo)/.exec('foofoo');    //['foo', 'foo']

// 因为'\1'='foo'，所以'/(foo)\1/'等价于'/(foo)foo/'
/(foo)\1/.exec('foofoo');      //['foofoo', 'foo']，匹配到了'foofoo'     
```
* 在`String.prototype.replace()`中使用反向引用

```javascript
var re = /(\w+)\s(\w+)/;
var str = 'John Smith';
str.match(re);  //["John Smith", "John", "Smith"]
var newstr = str.replace(re, '$2, $1');
console.log(newstr);    //Smith, John
```

#### 非捕获性分组

不记录分组信息，不能创建反向引用的匹配，格式为`(?:x)`

Character | Meaning
----------|--------
`(?:x)`|Matches 'x' but does not remember the match.

```javascript
// 正常情况下为捕获性分组，匹配字符串'abc'，捕获分组字符串'c'
'abc'.match(/(\w){3}/);     //["abc", "c"]

// 使用非捕获性分组，匹配字符串'abc'，未捕获到分组字符串
'abc'.match(/(?:\w){3}/);   //["abc"]
```

```javascript
// 正常情况下两个分组信息都捕获
'12345.123'.match(/^(\d)+.(\d){3}$/g);

console.log(RegExp.$1); //5
console.log(RegExp.$2); //3

// 第一个分组使用非捕获
'12345.123'.match(/^(?:\d)+.(\d){3}$/g);

console.log(RegExp.$1); //3
console.log(RegExp.$2); //不存在
```

#### 前瞻捕获

Character | Meaning
----------|--------
`x(?=y)`|Matches 'x' only if 'x' is followed by 'y'. This is called a lookahead.
`x(?!y)`|Matches 'x' only if 'x' is not followed by 'y'. This is called a negated lookahead.

* 正向前瞻匹配`x(?=y)`，找到x后面紧跟着y的位置，如果找到则匹配这个位置，返回x
* 逆向前瞻匹配`x(?!y)`，找到x后面不是y的位置，如果找到则匹配这个位置，返回x
* *括号`()`只代表匹配的一个位置，不代表匹配的字符*

```javascript
// 匹配到了位置，在a和1之间，结果匹配到了'a'
'a1'.match(/a(?=1)/);   //['a']

// 匹配到了位置，在a和1之间，'\d'匹配了后面的1
'a1'.match(/a(?=1)\d/);   //['a1']

// 匹配了第一个a和1之间的位置
'a1bcdefa1'.match(/a(?=1)/);    //['a']

// 匹配到了所有的a和1之间的位置(字符串开始和结束的两个'a1')
'a1bcdefa1'.match(/a(?=1)/g);   //['a', 'a']

// 在a后面没有找到1，所以没有匹配到a和1之间的位置
'a2'.match(/a(?=1)/);   //null
```

```javascript
// a后面为2不是1，所以找到了匹配的位置，在a和2之间
'a2'.match(/a(?!1)/);   //['a']

// 同上，用'\d'匹配了2
'a2'.match(/a(?!1)\d/); //['a2']

// 这里匹配的位置是'aba'和'a'之间的位置，返回的是[a-b]+匹配的结果
'abaa1'.match(/[a-b]+(?!1)/);  //['aba']
```

#### 一些正则表达式例子

* 匹配Email方法一：`/^[\w-]+@[\w]+(\.[\w]+)+$/`
* 匹配Email方法二：`/^[\w-]{2,}@([\w]+\.)+[a-z]{2,}$/`，`@`前面字符必须大于2位，`.`后面字符必须大于2位且必须为小写字母，这种匹配更精确
* 用户名为大写小写数字和下划线的组合并且长度为6-10：`/^[\w]{6,10}$/`


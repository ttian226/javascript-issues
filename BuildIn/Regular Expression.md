#### Regular expression flags

Flag | Description
-----|------------
g|Global search
i|Case-insensitive search
m|Multi-line search

To include a flag with the regular expression, use this syntax:

`var re = /pattern/flags;`

*or*

`var re = new RegExp("pattern", "flags");`


#### Special characters in regular expressions

Character | Meaning
----------|--------
\t|Matches a tab
\r|Matches a carriage return(回车)
\n|Matches a line feed(换行)


*Example1*

```javascript
var re1 = new RegExp('abc', 'g');

// equal to
var re2 = /abc/g;

console.log(re2 instanceof RegExp); //true
```

*Example2*

```javascript
var re = /abc/;
var str = 'abc';

var res = re.test(str);
var arr = re.exec(str);

console.log(res);   //true
console.log(arr);   //['abc']
```

*Example3*

```javascript
var re = /abc/;
var str = '123abcdefg';

var res = re.test(str);
var arr = re.exec(str);

console.log(res);   //true
console.log(arr);   //['abc']
```

*Example4*

```javascript
var re = /abc/;
var str = 'ab';

var res = re.test(str);
var arr = re.exec(str);

console.log(res);   //false
console.log(arr);   //null
```






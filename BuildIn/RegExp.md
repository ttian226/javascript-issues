
##### [RegExp.prototype.exec()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec)

The **exec()** method executes a search for a match in a specified string. Returns a result array, or null.


##### [RegExp.prototype.test()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test)

The **test()** method executes a search for a match between a regular expression and a specified string. Returns true or false.

* use global flag, `re.lastIndex` has changed.

```javascript
var re = /quick\s(brown).+?(jumps)/ig;
var str = 'The Quick Brown Fox Jumps Over The Lazy Dog';

console.log(re.lastIndex);
var arr = re.exec(str);
console.log(re.lastIndex);
console.log(arr);

// output
// 0
// 25
// ["Quick Brown Fox Jumps", "Brown", "Jumps", index: 4, input: "The Quick Brown Fox Jumps Over The Lazy Dog"]
```

* not use global flag, `re.lastIndex` not change always 0.

```javascript
var re = /quick\s(brown).+?(jumps)/i;
var str = 'The Quick Brown Fox Jumps Over The Lazy Dog';

console.log(re.lastIndex);
var arr = re.exec(str);
console.log(re.lastIndex);

// output
// 0
// 0
```

**Example:** Finding successive matches

```javascript
var myRe = /ab*/g;
var str = 'abbcdefabh';

var list = [], arr;
while ((arr = myRe.exec(str))) {
    var msg = 'Found ' + arr[0] + '. ';
    msg += 'Next match starts at ' + myRe.lastIndex;
    console.log(msg);
    list.push(arr[0]);
}
console.log(list);

// output
// Found abb. Next match starts at 3
// Found ab. Next match starts at 9
// ["abb", "ab"]
```


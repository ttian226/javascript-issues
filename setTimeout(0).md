
实现javascript的异步，`alert(2)`虽然延时了0ms,但是执行顺序为：1，3，2。这样就保证setTimeout里面的语句在某一代码段中最后执行

```javascript
alert(1);
setTimeout(function () {
    alert(2);
}, 0);
alert(3);
```

在事件中，由于javascript是单线程的，在onmousedown时无法同时处理focus，select事件，导致这两个事件被忽略，使用setTimeout可以把这两个事件放在一个新的队列中执行。

```html
<body>
<h1><code>DEMO1</code></h1>

<h2>1、未使用 <code>setTimeout</code>（未选中文本框内容）</h2>
<button id="makeinput">生成 input</button>
<p id="inpwrapper"></p>

<h2>2、使用 <code>setTimeout</code>（立即选中文本框内容）</h2>
<button id="makeinput2">生成 input</button>
</h2>
<p id="inpwrapper2"></p>

<h1><code>DEMO2</code></h1>

<h2>1、未使用 <code>setTimeout</code>(只有输入第二个字符时，前一个字符才显示出来)</h2>
<input type="text" id="input1" value=""/>

<div id="preview1"></div>
<h2>2、使用 <code>setTimeout</code>(输入时，字符同时显示出来)</h2>
<input type="text" id="input2" value=""/>

<div id="preview2"></div>
</body>
```

```javascript
(function () {

    function get(id) {
        return document.getElementById(id);
    }

    window.onload = function () {
        get('makeinput').onmousedown = function () {
            var input = document.createElement('input');
            input.setAttribute('type', 'text');
            input.setAttribute('value', 'test1');
            get('inpwrapper').appendChild(input);
            input.focus();
            input.select();
        };
        get('makeinput2').onmousedown = function () {
            var input = document.createElement('input');
            input.setAttribute('type', 'text');
            input.setAttribute('value', 'test1');
            get('inpwrapper2').appendChild(input);
            setTimeout(function () {
                input.focus();
                input.select();
            }, 0);
        };
        get('input1').onkeypress = function () {
            get('preview1').innerHTML = this.value;
        };
        get('input2').onkeypress = function () {
            setTimeout(function () {
                get('preview2').innerHTML = get('input2').value;
            }, 0);
        };
    }
})();
```

*参考 [setTimeout(0)](http://www.cnblogs.com/fullhouse/archive/2012/10/10/2718542.html)*


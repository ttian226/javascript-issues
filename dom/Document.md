#### [Document](https://developer.mozilla.org/en-US/docs/Web/API/document)

每个在浏览器中加载的页面都有一个`document`对象。通过`document`对象可以访问页面的内容（比如dom树，和内部的元素）

`document`对象可以由以下几种方法获取

    1. 通常情况下直接使用`document`或`window.document`取得`document`对象
    2. 通过iframe的`contentDocument`属性获取
    3. The responseXML of an XMLHttpRequest object
    4. 通过`node`或`element`对象的`ownerDocument`属性获取

所有的`document`对象都是通过`Document`接口实现的

#### Properties

##### [Document.body](https://developer.mozilla.org/en-US/docs/Web/API/Document/body)

返回当前文档的`<body>`或`<frameset>`元素，如果元素不存在则返回null

```html
<body id="oldBodyElement"></body>
```

例（在页面加载完成后执行）：

```javascript
alert(document.body.id);    //'oldBodyElement'

// 创建一个新的body元素
var aNewBodyElement = document.createElement("body");
aNewBodyElement.id = "newBodyElement";

// 把创建好的body元素赋给document.body
document.body = aNewBodyElement;
alert(document.body.id);    //"newBodyElement"
```

*给文档设置一个新的body需要先删除已经存在的`<body>`元素*

##### [Document.documentElement](https://developer.mozilla.org/en-US/docs/Web/API/Document/documentElement)

它是一个只读属性，返回文档的根节点元素（例如对于html文档来说，返回的是`<html>`元素）

例：

```javascript
var rootElement = document.documentElement;
var firstTier = rootElement.childNodes;

// 遍历根节点的直接子元素
for (var i = 0; i < firstTier.length; i++) {
   // 对每一个直接子元素做些事情
   // as firstTier[i]
}
```

Notes：

    * 这个属性可以很方便的获取文档的直接子元素
    * html文档只包含一个子节点`<html>`，xml文档通常会包含多个子节点。
    * 通常要使用`document.documentElement`而不是`document.firstChild`去获取根节点元素

##### [Document.forms](https://developer.mozilla.org/en-US/docs/Web/API/Document/forms)

返回当前文档中form元素的集合（一个HTMLCollection对象）

例：

```html
<body>
<form id="robby">
    <input type="button" onclick="alert(document.forms[0].id);" value="robby's form" />
</form>

<form id="dave">
    <input type="button" onclick="alert(document.forms[1].id);" value="dave's form" />
</form>

<form id="paul">
    <input type="button" onclick="alert(document.forms[2].id);" value="paul's form" />
</form>
</body>
```

```javascript
var forms = document.forms;
alert(forms.length);    //3
var form1 = forms[0];   //取得第一个form元素
```

##### [Document.head](https://developer.mozilla.org/en-US/docs/Web/API/Document/head)

返回当前文档的`<head>`元素，如果文档中大于一个`<head>`元素，返回第一个元素。

Notes:

    这个属性是只读的，试图给这个属性赋值都会出错。

##### [Document.images](https://developer.mozilla.org/en-US/docs/Web/API/Document/images)

返回当前文档image元素的集合

例子：

```javascript
var ilist = document.images;

for(var i = 0; i < ilist.length; i++) {
    if(ilist[i].src == "banner.gif") {
        // found the banner
    }
}
```

Notes:

    * document.images.length返回当前页面的图片数
    * document.images它是html dom的一部分，只工作在html中

##### [Document.scripts](https://developer.mozilla.org/en-US/docs/Web/API/Document/scripts)

返回文档的script元素列表（是一个HTMLCollection对象）

例子：

```javascript
var scripts = document.scripts;

if (scripts.length) {
    alert("This page has scripts!");
}
```

##### [Document.title](https://developer.mozilla.org/en-US/docs/Web/API/Document/title)

获取或设置文档的标题

例子：

```html
<!DOCTYPE html>
<html>
<head>
<title>Hello World!</title> 
</head>
<body>

<script>
alert(document.title); // displays "Hello World!"
document.title = "Goodbye World!";
alert(document.title); // displays "Goodbye World!"
</script>

</body>
</html>
```

##### [Document.anchors](https://developer.mozilla.org/en-US/docs/Web/API/Document/anchors)

返回文档中的锚点列表

例子：

```html
<h1>Title</h1>
<h2><a name="contents">Contents</a></h2>
<h2><a name="plants">Plants</a></h2>
<h2><a name="veggies">Veggies</a></h2>
```

```javascript
// document.anchors返回一个数组包含3个值，[<a name="contents">Contents</a>, <a name="plants">Plants</a>, <a name="veggies">Veggies</a>]
alert(document.anchors.length); //3
```

Notes:

    返回的锚点集合中只包含带有name属性的<a>，并不包含使用id属性创建的锚点（<a>标签的name属性在html5已经不支持，html5推荐使用id属性来设置锚点）


##### [Document.links](https://developer.mozilla.org/en-US/docs/Web/API/Document/links)

links属性返回文档中带`href`属性的`<area>`元素和`<a>`元素的集合

```html
<a href="http://baidu.com">baidu</a>
<a href="http://taobao.com">taobao</a>
<area shape="" coords="" href="" alt=""/>
```

```javascript
alert(document.links.length);     //3
```

##### [Document.location](https://developer.mozilla.org/en-US/docs/Web/API/Document/location)

`Document.location`是一个只读属性，返回一个`Location`对象，它包含了当前文档URL的信息以及提供了一些方法来改变URL地址或者是加载另一个URL

##### [Document.URL](https://developer.mozilla.org/en-US/docs/Web/API/Document/URL)

返回当前文档的url

```javascript
document.location = 'http://www.mozilla.org';   //Equivalent to
document.location.href = 'http://www.mozilla.org';
```

##### [Document.referrer](https://developer.mozilla.org/en-US/docs/Web/API/Document/referrer)

返回链接到当前文档的url（之前link过来的路径）

##### [Document.domain](https://developer.mozilla.org/en-US/docs/Web/API/Document/domain)

获取或设置文档的域名

##### [Document.activeElement](https://developer.mozilla.org/en-US/docs/Web/API/Document/activeElement)

返回当前文档焦点所在的元素

**Example**

```html
<input type="text">
```
```javascript
var input = document.querySelector('input');
input.focus();
console.log(document.activeElement === input);  //true
```

注：当文档加载完成后，`document.activeElement` 返回`document.body`，在文档加载期间`document.activeElement`是null.

##### [Document.readyState](https://developer.mozilla.org/en-US/docs/Web/API/Document/readyState)

当文档正在加载时返回"loading"，解析完成但仍然加载资源返回"interactive"，所有的资源全部加载完成返回"complete"。

```javascript
document.onreadystatechange = function () {
    if (document.readyState === 'complete') {
        console.log('complete');
    }

    if (document.readyState === 'interactive') {
        console.log('interactive');
    }
};

// output
// interactive
// complete
```

*[readystatechange](https://developer.mozilla.org/en-US/docs/Web/Events/readystatechange)事件当readyState属性改变时触发。*

##### [Document.cookie](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie)

设置或读取当前文档的cookie

* 读取所有cookie:
`allCookies = document.cookie;`读取后的cookie是一个键值对的字符串

* 设置新的cookie:
`document.cookie = newCookie;`

#### Methods

##### [Document.getElementById()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById)

通过元素id返回元素的引用，如果在文档中找不到id，返回null(id是大小写敏感的)

##### [Document.getElementsByTagName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByTagName)

根据标签名返回元素的集合（一个HTMLCollection对象）

##### [Document.getElementsByName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByName)

根据节点的属性name值返回元素的集合（一个NodeList对象）

**Example**

```html
<div id="div1" name="test"></div>
<div id="div2" name="test"></div>
<div id="div3" name="test"></div>
```
```javascript
// 返回一个HTMLCollection对象
var divs = document.getElementsByTagName('div');
console.log(divs);

// 返回一个NodeList对象
var names = document.getElementsByName('test');
console.log(names);

// divs[0]和names[0]都返回了第一个div元素的引用
console.log(divs[0] === names[0]);
```
##### [Document.getElementsByClassName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)

根据类名返回元素的集合（一个类数组的对象HTMLCollection），当作用在document上，将搜索整个文档的。也可以通过`element.getElementsByClassName()`作用在指定的节点元素上查找。

```javascript
var elements = document.getElementsByClassName(names); // or:
var elements = rootElement.getElementsByClassName(names);
```

* elements是一个动态元素的集合。
* names要查找的类名的字符串，如果有多个类名时，需要用空格分开。
* getElementsByClassName可以作用在任意元素上，不仅仅是document对象

**Example1**

```javascript
// Get all elements that have a class of 'test'
document.getElementsByClassName('test');

// Get all elements that have both the 'red' and 'test' classes
document.getElementsByClassName('red test');

// Get all elements that have a class of 'test', inside of an element that has the ID of 'main'
document.getElementById('main').getElementsByClassName('test');
```

**Example2**

```html
<ul>
    <li class="test"></li>
    <li class="test"></li>
    <li class="test"></li>
</ul>
```
```javascript
var lis = document.getElementsByClassName('test');

console.log(lis.length);   //3
console.log(lis instanceof HTMLCollection);  //true
```

##### [Document.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)

通过匹配css选择器，返回第一个匹配的元素。

```javascript
var element = document.querySelector(selectors);
```
* *element* 是返回的一个元素对象
* *selectors* 是一组匹配的选择器

**Example**

```html
<ul>
    <li class="test" id="l1"></li>
    <li class="test" id="l2"></li>
    <li class="test" id="l3"></li>
    <li class="test" id="l4"></li>
    <li class="test" id="l5"></li>
</ul>
```
```javascript
var ul = document.querySelector('.test');   // equal to "document.querySelector('#l1')"
console.log(ul);    //<li class="test" id="l1"></li>
```


##### [Document.querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)

通过匹配css选择器返回NodeList对象

**Example1**

```html
<ul>
    <li class="test"></li>
    <li class="test"></li>
    <li class="test"></li>
    <li class="test"></li>
    <li class="test"></li>
</ul>
```
```javascript
var uls = document.querySelectorAll('.test');
console.log(uls.length);    //5
```

**Example2**
返回div元素带有calss为'note'或'alert'元素的集合

```javascript
var matches = document.querySelectorAll("div.note, div.alert");
```

##### [Document.createElement()](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)

创建一个html元素

```javascript
var element = document.createElement(tagName);
```

* *element* 创建后的元素对象
* *tagName* 要创建元素的标签名


##### [Document.createTextNode()](https://developer.mozilla.org/en-US/docs/Web/API/Document/createTextNode)

创建一个文本节点

```javascript
var text = document.createTextNode(data);
```
* *text* 创建后的文本节点
* *data* 文本字符串

##### [Document.createAttribute()](https://developer.mozilla.org/en-US/docs/Web/API/Document/createAttribute)

创建一个属性节点

```javascript
attribute = document.createAttribute(name)
```
* *attribute* 创建的属性节点.
* *name* 属性名.

**Example**

*初始html为:*

```html
<div>
    <span id="childSpan">foo bar</span>
</div>
```
```javascript
var sp1 = document.createElement('span');
sp1.setAttribute('id', 'newSpan');

// 创建属性节点a，属性名为myattr
var a = document.createAttribute('myattr');
// 设置属性值为my_value
a.value = 'my_value';
// 通过setAttributeNode设置节点属性
sp1.setAttributeNode(a);

var sp1_content = document.createTextNode('new replacement span element.');
sp1.appendChild(sp1_content);

var sp2 = document.getElementById('childSpan');
var parentDiv = sp2.parentNode;

parentDiv.appendChild(sp1);
```
*现在html为:*

```html
<div>
    <span id="childSpan">foo bar</span>
    <span id="newSpan" myattr="my_value">new replacement span element.</span>
</div>
```

##### [Document.hasFocus()](https://developer.mozilla.org/en-US/docs/Web/API/Document/hasFocus)

指示文档或文档中的任何元素是否处于焦点状态。这个方法用来检查在文档中是否有焦点元素

**Example**

```html
<p>Click anywhere in the document (the right frame) to get focus. If you click outside the document, it will lose focus.</p>

<p id="demo"></p>

```
```javascript
setInterval(myFunction, 1);

function myFunction() {
    var x = document.getElementById("demo");
    if (document.hasFocus()) {
        x.innerHTML = "The document has focus.";
    } else {
        x.innerHTML = "The document DOES NOT have focus.";
    }
}
```

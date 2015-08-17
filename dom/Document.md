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

Returns a list of the script elements in the document. The returned object is an HTMLCollection.

##### [Document.title](https://developer.mozilla.org/en-US/docs/Web/API/Document/title)

Gets or sets the title of the document

##### [Document.anchors](https://developer.mozilla.org/en-US/docs/Web/API/Document/anchors)

anchors returns a list of all of the anchors in the document.

*Note*
the returned set of anchors only contains those anchors created with the name attribute, not those created with the id attribute

```html
<h1>Title</h1>
<h2><a name="contents">Contents</a></h2>
<ul id="toc"></ul>

<h2><a name="plants">Plants</a></h2>
<ol>
    <li>Apples</li>
    <li>Oranges</li>
    <li>Pears</li>
</ol>

<h2><a name="veggies">Veggies</a></h2>
<ol>
    <li>Carrots</li>
    <li>Celery</li>
    <li>Beats</li>
</ol>
```

document.anchors reutrn a array: [<a name="contents">Contents</a>, <a name="plants">Plants</a>, <a name="veggies">Veggies</a>],contain 3 items

##### [Document.links](https://developer.mozilla.org/en-US/docs/Web/API/Document/links)

The links property returns a collection of all <area> elements and <a> elements in a document with a value for the href attribute

##### [Document.location](https://developer.mozilla.org/en-US/docs/Web/API/Document/location)

The Document.location read-only property returns a **Location** object, which contains information about the URL of the document and provides methods for changing that URL and loading another URL

##### [Document.URL](https://developer.mozilla.org/en-US/docs/Web/API/Document/URL)

The URL read-only property of the Document interface returns the document location as a string

```javascript
document.location = 'http://www.mozilla.org';   //Equivalent to
document.location.href = 'http://www.mozilla.org';
```

##### [Document.referrer](https://developer.mozilla.org/en-US/docs/Web/API/Document/referrer)

Returns the [URI](http://www.w3.org/Addressing/#background) of the page that linked to this page.

##### [Document.domain](https://developer.mozilla.org/en-US/docs/Web/API/Document/domain)

Gets/sets the domain portion of the origin of the current document, as used by the same origin policy.

##### [Document.activeElement](https://developer.mozilla.org/en-US/docs/Web/API/Document/activeElement)

Returns the currently focused element.

**Example**

```html
<input type="text">
```
```javascript
var input = document.querySelector('input');
input.focus();
console.log(document.activeElement === input);  //true
```

*Note:* after document finish load, `document.activeElement` reference to `document.body`. during document load `document.activeElement` is null.

##### [Document.readyState](https://developer.mozilla.org/en-US/docs/Web/API/Document/readyState)

Returns "loading" while the document is loading, "interactive" once it is finished parsing but still loading sub-resources, and "complete" once it has loaded.

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

*The [readystatechange](https://developer.mozilla.org/en-US/docs/Web/Events/readystatechange) event is fired when the readyState attribute of a document has changed*


#### Methods

##### [Document.getElementById()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById)

Returns a reference to the element by its ID.
* element is a reference to an **Element** object, or null if an element with the specified ID is not in the document
* id is a case-sensitive string representing the unique ID of the element being sought

##### [Document.getElementsByTagName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByTagName)

Returns an **HTMLCollection** of elements with the given tag name.

##### [Document.getElementsByName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByName)

Returns a nodelist collection with a given name in the (X)HTML document.

**Example**

```html
<div id="div1" name="test"></div>
<div id="div2" name="test"></div>
<div id="div3" name="test"></div>
```
```javascript
// divs return a HTMLCollection obj
var divs = document.getElementsByTagName('div');
console.log(divs);

// names return a nodelist obj
var names = document.getElementsByName('test');
console.log(names);

// divs[0] and names[0] return a same reference to the Element of the first div
console.log(divs[0] === names[0]);
```
##### [Document.getElementsByClassName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)

Returns an array-like object(HTMLCollection) of all child elements which have all of the given class names. When called on the document object, the complete document is searched, including the root node. You may also call getElementsByClassName() on any element; it will return only elements which are descendants of the specified root element with the given class names.

```javascript
var elements = document.getElementsByClassName(names); // or:
var elements = rootElement.getElementsByClassName(names);
```

* elements is a live HTMLCollection of found elements
* names is a string representing the list of class names to match; class names are separated by whitespace
* getElementsByClassName can be called on any element, not only on the document. The element on which it is called will be used as the root of the search

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
Returns the first element within the document (using depth-first pre-order traversal of the document's nodes) that matches the specified group of selectors.

```javascript
var element = document.querySelector(selectors);
```
* *element* is an element object.
* *selectors* is a string containing one or more CSS selectors separated by commas

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
Returns a list of the elements within the document (using depth-first pre-order traversal of the document's nodes) that match the specified group of selectors. The object returned is a **NodeList**.

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

**Example2** returns a list of all div elements within the document with a class of either "note" or "alert":

```javascript
var matches = document.querySelectorAll("div.note, div.alert");
```

##### [Document.createElement()](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)

In an HTML document, the Document.createElement() method creates the specified HTML element or an HTMLUnknownElement if the given element name isn't a known one

```javascript
var element = document.createElement(tagName);
```

* *element* is the created Element object.
* *tagName* is a string that specifies the type of element to be created. The nodeName of the created element is initialized with the value of tagName. Don't use qualified names (like "html:a") with this method


##### [Document.createTextNode()](https://developer.mozilla.org/en-US/docs/Web/API/Document/createTextNode)

Creates a new Text node.

```javascript
var text = document.createTextNode(data);
```
* *text* is a Text node.
* *data* is a string containing the data to be put in the text node.

##### [Document.createAttribute()](https://developer.mozilla.org/en-US/docs/Web/API/Document/createAttribute)

createAttribute creates a new attribute node, and returns it.

```javascript
attribute = document.createAttribute(name)
```
* *attribute* is an attribute node.
* *name* is a string containing the name of the attribute.

**Example**

*init html is:*

```html
<div>
    <span id="childSpan">foo bar</span>
</div>
```
```javascript
var sp1 = document.createElement('span');
sp1.setAttribute('id', 'newSpan');

var a = document.createAttribute('myattr');
a.value = 'my_value';
sp1.setAttributeNode(a);

var sp1_content = document.createTextNode('new replacement span element.');
sp1.appendChild(sp1_content);

var sp2 = document.getElementById('childSpan');
var parentDiv = sp2.parentNode;

parentDiv.appendChild(sp1);
```
*after appendChild html is:*

```html
<div>
    <span id="childSpan">foo bar</span>
    <span id="newSpan" myattr="my_value">new replacement span element.</span>
</div>
```

##### [Document.hasFocus()](https://developer.mozilla.org/en-US/docs/Web/API/Document/hasFocus)

The **Document.hasFocus()** method returns a Boolean value indicating whether the document or any element inside the document has focus. This method can be used to determine whether the active element in a document has focus.

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

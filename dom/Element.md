#### [Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)

#### Properties

##### [Element.attributes](https://developer.mozilla.org/en-US/docs/Web/API/Element/attributes)

**Element.attributes**属性返回一个节点属性的动态集合。它是一个[NamedNodeMap](https://developer.mozilla.org/en-US/docs/Web/API/NamedNodeMap)对象。它是一个类数组对象。

**Example**

```html
<div id="div1" name="test1" class="cls1" myattr="my_val"></div>
```
```javascript
var div = document.getElementById('div1');

// attrs是NamedNodeMap类型对象, 它是类数组对象，每一项都是Attr对象
var attrs = div.attributes;

// 迭代attrs
for (var i = 0; i < attrs.length; i++) {
    // one是Attr对象
    var one = attrs[i],

        // 获取attr名字
        name = one.name,

        // 获取attr的值
        value = one.value;
    console.log('name:' + name + ' value:' + value);
}

// output
// name:id value:div1
// name:name value:test1
// name:class value:cls1
// name:myattr value:my_val
```

##### [Element.className](https://developer.mozilla.org/en-US/docs/Web/API/Element/className)

获取或设置元素的class属性

**Example**

```html
<div id="div1" name="test1" class="cls1" myattr="my_val"></div>
```
```javascript
var div = document.getElementById('div1');

// get classname
var clname = div.className;
console.log(clname);    //cls1

// set classname
div.className = 'cls2'; //div's classname has been set to 'cls2'
```

##### [Element.id](https://developer.mozilla.org/en-US/docs/Web/API/Element/id)

获取或设置元素的id

**Example**

```html
<div id="div1" name="test1" class="cls1" myattr="my_val"></div>
```
```javascript
var div = document.getElementById('div1');

// get id
var id = div.id;
console.log(id); //div1

// set id
div.id = 'div2'; //div's id has been set to 'div2'
```

##### [Element.tagName](https://developer.mozilla.org/en-US/docs/Web/API/Element/tagName)

返回元素的标签名字

注：`tagName`是以大写字母来返回的，它的值等同于`Node.nodeName`

**Example**

```html
<div id="div1" name="test1" class="cls1" myattr="my_val"></div>
```
```javascript
var div = document.getElementById('div1');

// get tag name
var tagname = div.tagName;  //'DIV'
console.log(tagname.toLowerCase()); //'div'
```

##### [Element.classList](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)

classList返回元素的class属性的一个集合，它返回的是[DOMTokenList](https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList)对象。

**Example**

```html
<div id="div1" name="test1" class="cls1 cls2 cls3" myattr="my_val"></div>
```
```javascript
var div = document.getElementById('div1');
var clslist = div.classList;
console.log(clslist.length);   //div包含3个class，所以为3
```

**Example**

```html
<body>
    <div id="test"></div>
</body>
```
```javascript
var div = document.getElementById('test');

// divClass为DOMTokenList对象
var divClass = div.classList;

// 调用DOMTokenList对象的add方法，给元素增加一个class
divClass.add('cls1');

console.log(divClass.length);   //1

console.log(divClass.item(0));  //'cls1'等价于divClass[0]

console.log(divClass.contains('cls1')); //true

// 调用DOMTokenList对象的remove方法，给元素删除指定的class
divClass.remove('cls1');

console.log(divClass.length);   //0

console.log(divClass.contains('cls1')); //false
```

##### [Element.innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML)

**Element.innerHTML**属性设置或读取指定元素内的html

*注：如果在`<div>`, `<span>`, `<noembed>`元素内包含字符(&), (<), (>)时，innerHTML返回转义字符&amp, &lt, &gt。使用，如果要返回字符本身要使用`Node.textContent`*

**Example1**

```html
<div id="test">10>1&</div>
```
```javascript
var div = document.getElementById('test');

// innerHTML返回转移的字符串
console.log(div.innerHTML);     //10&gt;1&amp;

// textContent返回原始的字符串
console.log(div.textContent);   //10>1&
```

**Example2**

```html
<ul>
    <li></li>
    <li></li>
    <li></li>
</ul>
<div id="test">some words</div>
```
```javascript
var div = document.getElementById('test');
var ul = document.querySelector('ul');

// 获取ul节点内的html
var html = ul.innerHTML;

// 设置div内部的html替换原有的内容
div.innerHTML = html;
```
*执行之后html如下：*

```html
<ul>
    <li></li>
    <li></li>
    <li></li>
</ul>
<div id="test">
    <li></li>
    <li></li>
    <li></li>
</div>
```

*这个属性提供了一个简单的方法来替换元素里的内容，例如通过以下的方法来替换body元素里的内容:*

```javascript
document.body.innerHTML = "";
```

##### [Element.outerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/outerHTML)

The outerHTML attribute of the element DOM interface gets the serialized HTML fragment describing the element including its descendants. It can be set to replace the element with nodes parsed from the given string

和`innerHTML`相比，`outerHTML`除了获取元素内部的html还包含当前元素的html。

**Example1**

```html
<div id="d">
    <p>Content</p>
    <p>Further Elaborated</p>
</div>
```
```javascript
var d = document.getElementById("d");

// 通过outerHTML获取了元素节点内的html（包含当前元素）
console.log(d.outerHTML);   //'<div id="d"><p>Content</p><p>Further Elaborated</p></div>'
```

**Example2**

```html
<div id="container">
    <div id="d">This is a div.</div>
</div>
```
```javascript
var d = document.getElementById("d");

// 通过outerHTML替换当前节点html
d.outerHTML = "<p>This paragraph replaced the original div.</p>";
```
*设置之后的html为：*

```html
<div id="container"><p>This paragraph replaced the original div.</p></div>
```

##### [ParentNode.childElementCount](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/childElementCount)

##### [ParentNode.children](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/children)

##### [ParentNode.firstElementChild](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/firstElementChild)

##### [ParentNode.lastElementChild](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/lastElementChild)

##### [Element.clientHeight](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientHeight)

返回元素padding + height的总高度(不包括border,margin的高度)

获取窗口的高度：`document.documentElement.clientHeight`

##### [Element.clientWidth](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientWidth)

返回元素padding + height的总宽度(不包括border,margin的宽度)

##### [Element.scrollHeight](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollHeight)

返回元素内容区域的高度（它把padding计算在内，不包括margin）

##### [Element.scrollWidth](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollWidth)

返回元素内容区域的宽度

##### [Element.clientTop](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientTop)

返回元素上边框（top broder）的宽度,不包括padding和margin

##### [Element.clientLeft](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientLeft)

返回元素左边框(left border)的宽度,不包括padding和margin

返回元素内容区域的宽度

##### [Element.scrollTop](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollTop)

获取或设置元素内容区域垂直向上滚动的像素

##### [Element.scrollLeft](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollLeft)

获取或设置元素内容区域水平向左滚动的像素

#### Methods

##### [Element.getAttribute()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getAttribute)

`getAttribute()`返回元素指定属性的值。如果给定的属性不存在，返回null或""

```javascript
var attribute = element.getAttribute(attributeName);
```
* *attribute* 获取的属性值
* *attributeName* 属性名

**Example**

```html
<div id="div1" name="test1" class="cls1" myattr="my_val" style="display:none"></div>
```
```javascript
var div = document.getElementById('div1'),
    id = div.getAttribute('id'),
    name = div.getAttribute('name'),
    classname = div.getAttribute('class'),
    myattr = div.getAttribute('myattr'),
    style = div.getAttribute('style');

console.log(id);        //'div1'
console.log(name);      //'test1'
console.log(classname); //'cls1'
console.log(myattr);    //'my_val'
console.log(style);     //'display:none'
```

##### [Element.setAttribute()](https://developer.mozilla.org/en-US/docs/Web/API/Element/setAttribute)

给指定元素添加新的属性或改变原有的属性值

```javascript
element.setAttribute(name, value);
```
* *name* 要设置的属性名
* *value* 要设置的属性值

##### [Element.removeAttribute()](https://developer.mozilla.org/en-US/docs/Web/API/Element/removeAttribute)

删除指定元素的属性

```javascript
element.removeAttribute(attrName);
```
* *attrName* 要删除的属性名

**Example**

```html
<div id="div1" align="left" width="200px"></div>
```
```javascript
var div = document.getElementById('div1');

// 删除div节点的align属性
div.removeAttribute('align');
```
现在html:

```html
<div id="div1" width="200px"></div>
```

##### [Element.hasAttribute()](https://developer.mozilla.org/en-US/docs/Web/API/Element/hasAttribute)

检查节点是否存在指定的属性。

```javascript
var result = element.hasAttribute(attName);
```
* *result* 布尔值，真或假
* *attName* 要检查的属性名

##### [Element.getElementsByClassName()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getElementsByClassName)

根据指定的类名获取节点的集合（一个动态的HTMLCollection对象）

[Document.getElementsByClassName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName) 它是作用在整个的document上; 它返回的是整个文档匹配的class元素的集合。

##### [Element.getElementsByTagName()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getElementsByTagName)

根据指定的标签名获取节点的集合（一个动态的HTMLCollection对象）

##### [Element.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Element/querySelector)

通过匹配css选择器，返回第一个匹配的元素。

返回

```javascript
element = baseElement.querySelector(selectors);
```
* *element* 和 *baseElement* 是元素对象。
* *selectors* 是一组匹配的选择器。


##### [Element.querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Element/querySelectorAll)

通过匹配css选择器返回NodeList对象

```javascript
elementList = baseElement.querySelectorAll(selectors);
```
* *elementList* 是一个非动态的元素列表
* *baseElement* 指定的元素（基于这个元素进行查找）
* *selectors* css选择器

**Example**

```javascript
// 返回body中所有的p元素
var matches = document.body.querySelectorAll('p');

// 返回一个p元素的列表，它的父节点是一个div带有class名为'highlighted'
var el = document.querySelector('#test');
var matches = el.querySelectorAll('div.highlighted > p');
```

##### [Element.getBoundingClientRect()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect)

返回元素相对于视窗的相对位置，返回是一个[DOMRect对象](https://developer.mozilla.org/en-US/docs/Mozilla/Tech/XPCOM/Reference/Interface/nsIDOMClientRect)

DOMRect对象包括如下属性：
1. bottom，视窗顶部距离元素底部的高度
2. height，等价于`offsetHeight`
3. left，视窗左侧距离元素左侧的宽度
4. right，视窗左侧距离元素右侧的宽度
5. top，视窗顶部距离元素顶部的高度
6. width，等价于`offsetWidth`

*left,right,top,bottom是相对于window而不是相对于document的*

##### [Element.setAttributeNode()](https://developer.mozilla.org/en-US/docs/Web/API/Element/setAttributeNode)

给指定的元素添加一个新的属性，它接受一个Attr Object（nodeType=2）作为参数

```javascript
var sp1 = document.createElement('span');

// 创建一个Attr Object
var a = document.createAttribute('myattr');
a.value = 'my_value';

sp1.setAttributeNode(a);
// <span myattr="my_value"></span>
```



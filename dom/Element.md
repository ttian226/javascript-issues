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

#### Methods

##### [Element.getAttribute()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getAttribute)

getAttribute() returns the value of a specified attribute on the element. If the given attribute does not exist, the value returned will either be null or "" (the empty string); see Notes for details

```javascript
var attribute = element.getAttribute(attributeName);
```
* *attribute* is a string containing the value of *attributeName*.
* *attributeName* is the name of the attribute whose value you want to get

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

Adds a new attribute or changes the value of an existing attribute on the specified element.

```javascript
element.setAttribute(name, value);
```
* *name* is the name of the attribute as a string.
* *value* is the desired new value of the attribute.

##### [Element.removeAttribute()](https://developer.mozilla.org/en-US/docs/Web/API/Element/removeAttribute)

removeAttribute removes an attribute from the specified element

```javascript
element.removeAttribute(attrName);
```
* *attrName* is a string that names the attribute to be removed from element.

**Example**

```html
<div id="div1" align="left" width="200px"></div>
```
```javascript
var div = document.getElementById('div1');
div.removeAttribute('align');
```
Now html:

```html
<div id="div1" width="200px"></div>
```

##### [Element.hasAttribute()](https://developer.mozilla.org/en-US/docs/Web/API/Element/hasAttribute)

The **Element.hasAttribute()** method returns a Boolean value indicating whether the specified element has the specified attribute or not

```javascript
var result = element.hasAttribute(attName);
```
* *result* holds the return value true or false.
* *attName* is a string representing the name of the attribute

##### [Element.getElementsByClassName()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getElementsByClassName)

The **Element.getElementsByClassName()** method returns a live HTMLCollection containing all child elements which have all of the given class names. When called on the document object, the complete document is searched, including the root node.

Similarly the method [Document.getElementsByClassName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName) acts on the whole document; it will return elements which are descendants of the specified document root element with the given class names.

##### [Element.getElementsByTagName()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getElementsByTagName)

The **Element.getElementsByTagName()** method returns a live HTMLCollection of elements with the given tag name. The subtree underneath the specified element is searched, excluding the element itself.


##### [Element.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Element/querySelector)

Returns the first element that is a descendant of the element on which it is invoked that matches the specified group of selectors

```javascript
element = baseElement.querySelector(selectors);
```
* *element* and *baseElement* are element objects.
* *selectors* is a group of selectors to match on.


##### [Element.querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Element/querySelectorAll)

Returns a non-live NodeList of all elements descended from the element on which it is invoked that match the specified group of CSS selectors.

```javascript
elementList = baseElement.querySelectorAll(selectors);
```
* *elementList* is a non-live list of element objects.
* *baseElement* is an element object.
* *selectors* is a group of selectors to match on

**Example**

```javascript
// This example returns a list of all the p elements in the HTML document body
var matches = document.body.querySelectorAll('p');

// This example returns a list of p children elements under a container, whose parent is a div that has the class 'highlighted':
var el = document.querySelector('#test');
var matches = el.querySelectorAll('div.highlighted > p');
```

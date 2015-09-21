#### [Node](https://developer.mozilla.org/en-US/docs/Web/API/Node)

A Node is an interface from which a number of DOM types inherit, and allows these various types to be treated (or tested) similarly

The following interfaces all inherit from Node its methods and properties: ```Document```, ```Element```, ```CharacterData``` (which ```Text```, ```Comment```, and CDATASection inherit), ProcessingInstruction, DocumentFragment, DocumentType, Notation, Entity, EntityReference

#### Properties

##### [Node.childNodes](https://developer.mozilla.org/en-US/docs/Web/API/Node/childNodes)

返回指定元素子节点的集合（它是NodeList对象）

**Example1**

```html
<body></body>
```
```javascript
var nodes = document.body.childNodes;
var len = nodes.length;     //1
var node = nodes[0];        //first node
var type = node.nodeType;   //3 TEXT_NODE 
var name = node.nodeName;   //'#text'
```
注：在元素中间空白符作为text类型的节点

**Example2**

```html
<body>
    <!-- This is a comment node! -->
    <p>Click the button get info about the body element's child nodes.</p>
    <button onclick="myFunction()">Try it</button>
    <p><strong>Note:</strong> Whitespace inside elements is considered as text, and text
    is considered as nodes. Comments are also considered as nodes.</p>
    <p id="demo"></p>
    <script src="test.js"></script>
</body>
```
DOM加载完成后执行以下脚本:

```javascript
var nodes = document.body.childNodes;
var len = nodes.length;
for (var i = 0; i < len; i++) {
    var type = nodes[i].nodeType;
    var name = nodes[i].nodeName;
    console.log('nodeName:' + name + ' nodeType:' + type);
}

// 控制台输出：
// nodeName:#text nodeType:3
// nodeName:#comment nodeType:8     comment
// nodeName:#text nodeType:3
// nodeName:P nodeType:1            p
// nodeName:#text nodeType:3
// nodeName:BUTTON nodeType:1       button
// nodeName:#text nodeType:3
// nodeName:P nodeType:1            p
// nodeName:#text nodeType:3
// nodeName:P nodeType:1            p
// nodeName:#text nodeType:3
// nodeName:SCRIPT nodeType:1       script
// nodeName:#text nodeType:3
```


##### [Node.firstChild](https://developer.mozilla.org/en-US/docs/Web/API/Node/firstChild)

返回指定元素的第一个子节点，如果没有子节点返回null

```html
<p id="para-01"><span>First span</span><span>Middle span</span><span>Last span</span></p>
```
```javascript
var pNode = document.getElementById('para-01');
var first = pNode.firstChild;   // <span>First span</span>
```
##### [Node.lastChild](https://developer.mozilla.org/en-US/docs/Web/API/Node/lastChild)

返回指定元素的最后一个子节点，如果没有子节点返回null

```html
<p id="para-01"><span>First span</span><span>Middle span</span><span>Last span</span></p>
```
```javascript
var pNode = document.getElementById('para-01');
var last = pNode.lastChild;   // <span>Last span</span>
```

注：如果元素包含空白，firstNode或lastNode返回文本节点

**Example**

```html
<p id="para-01">
    <span>First span</span>
    <span>Middle span</span>
    <span>Last span</span>
</p>
```
```javascript
var pNode = document.getElementById('para-01');
var first = pNode.firstChild;   //a node reference to text Node
var last = pNode.lastChild;     //a node reference to text Node
```

##### [Node.nodeName](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeName)

返回节点名字

*不同类型的节点返回的名字如下:*

节点类型 | nodeName值
----------|---------------
Comment|"#comment"
Document|"#document"
Text|"#text"
Element|Element.tagName（元素返回tagName的值）


##### [Node.nodeType](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeType)

返回节点的类型（无符号短整型）

*不同类型节点的值如下:*

Name | Value
-----|------
ELEMENT_NODE|1
TEXT_NODE|3
COMMENT_NODE|8
DOCUMENT_NODE|9


##### [Node.nodeValue](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeValue)

返回或设置当前节点的值，对于document自身返回null，对于Text和Comment类型返回节点内容

Attr | value of attribute
-----|-------------------
Comment|content of comment
Document|null
Element|null
Text|content of the text node


##### [Node.textContent](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent)

显示节点的文本内容

```html
<div id="div1">some text</div>
```
```javascript
var div = document.getElementById('div1');

// 获取节点的文本内容
var content = div.textContent;      //some text

// 设置文本内容
div.textContent = 'other text';     //content set to "other text"
```

##### [Node.parentNode](https://developer.mozilla.org/en-US/docs/Web/API/Node/parentNode)

返回指定节点的父节点

```html
<html>
    <body>
        <div id="div0"><div id="div1">some text</div></div>
    </body>
</html>
```
```javascript
var div1 = document.getElementById('div1');
var div0 = div1.parentNode;     // reference to div0
var body = div0.parentNode;     // reference to body
var html = body.parentNode;     // reference to html

console.log(html.nodeType);     // 1 html节点仍然是元素类型，ELEMENT_NODE
console.log(html.parentNode.nodeType);      // 9 html的父节点是DOCUMENT_NODE
```

##### [Node.nextSibling](https://developer.mozilla.org/en-US/docs/Web/API/Node/nextSibling)

返回指定节点的下一个同级节点

##### [Node.previousSibling](https://developer.mozilla.org/en-US/docs/Web/API/Node/previousSibling)

返回指定节点的上一个同级节点

```html
<div id="div1"></div><div id="div2"></div><div id="div3"></div>
```
```javascript
var div2 = document.getElementById('div2');
var div3 = div2.nextSibling;
var div1 = div2.previousSibling;
```
##### [Node.ownerDocument](https://developer.mozilla.org/en-US/docs/Web/API/Node/ownerDocument)

返回指定节点的所属文档节点。

```html
<body>
    <div id="div1"></div>
</body>
```
```javascript
var div = document.getElementById('div1');

// 返回文档对象
var owner = div.ownerDocument;
console.log(owner === document);    //true

// documentElement返回的是文档的根html节点，而不是document文档节点。
var html = owner.documentElement;
```

#### Methods

##### [Node.appendChild()](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild)

The *Node.appendChild()* method adds a node to the end of the list of children of a specified parent node. If the given child is a reference to an existing node in the document, appendChild() moves it from its current position to the new position


**Example1**

create new element <p> and append to <body> element

```javascript
var p = document.createElement('p');
document.body.appendChild(p);
```
result:

```html
<body>
    <p></p>
</body>
```

**Example2**
before append, html is like:

```html
<body>
    <div id="div1"></div>
    <div id="div0"></div>
</body>
```
```javascript
var div1 = document.getElementById('div1');
var div0 = document.getElementById('div0');
div0.appendChild(div1);
```
after append, div1's position has been changed

```html
<body>
    <div id="div0"><div id="div1"></div></div>
</body>
```

##### [Node.cloneNode()](https://developer.mozilla.org/en-US/docs/Web/API/Node/cloneNode)

The *Node.cloneNode()* method returns a duplicate of the node on which this method was called

```javascript
var dupNode = node.cloneNode(deep);
```
* *node:* The node to be cloned
* *deep:* The new node that will be a clone of node
* *dupNode:* true if the children of the node should also be cloned, or false to clone only the specified node, default is false

```html
<body>
    <div id="div1"><div id="subdiv1"></div></div>
    <div id="div0"></div>
</body>
```
```javascript
var div1 = document.getElementById('div1');
var div0 = document.getElementById('div0');
// no deep clone or equal to div1.cloneNode(false)
var newdiv1 = div1.cloneNode();
div0.appendChild(newdiv1);
```
```html
<body>
    <div id="div1"><div id="subdiv1"></div></div>
    <div id="div0"><div id="div1"></div></div>
</body>
```

deep clone

```javascript
var newdiv2 = div1.cloneNode(true);
div0.appendChild(newdiv2);
```
```html
<body>
    <div id="div1"><div id="subdiv1"></div></div>
    <div id="div0"><div id="div1"><div id="subdiv1"></div></div></div>
</body>
```

##### [Node.hasChildNodes()](https://developer.mozilla.org/en-US/docs/Web/API/Node/hasChildNodes)

The *Node.hasChildNodes()* method returns a Boolean value indicating whether the current Node has child nodes or not.

##### [Node.insertBefore()](https://developer.mozilla.org/en-US/docs/Web/API/Node/insertBefore)

The Node.insertBefore() method inserts the specified node before a reference element as a child of the current node

```javascript
var insertedElement = parentElement.insertBefore(newElement, referenceElement);
```

* *insertedElement:* The node being inserted, that is newElement
* *parentElement:* The parent of the newly inserted node.
* *newElement:* The node to insert
* *referenceElement:* The node before which newElement is inserted

**Example**

```html
<div id="parentElement">
    <span id="childElement">foo bar</span>
</div>
```
```javascript
var sp1 = document.createElement('span');
var sp2 = document.getElementById('childElement');
var parent = sp2.parentNode;
var newnode = parent.insertBefore(sp1, sp2);
console.log(newnode === sp1);   //ture
```
after insertBefore:

```html
<div id="parentElement">
    <span></span>
    <span id="childElement">foo bar</span>
</div>
```

##### [Node.removeChild()](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild)

The Node.removeChild() method removes a child node from the DOM. Returns removed node

```javascript
var oldChild = element.removeChild(child);
```

* *child* is the child node to be removed from the DOM.
* *element* is the parent node of child.
* *oldChild* holds a reference to the removed child node. oldChild === child.

**Example**

```html
<div id="top">
    <div id="nested"></div>
</div>
```
```javascript
var d_top = document.getElementById('top');
var d_nested = document.getElementById('nested');
var throwawayNode = d_top.removeChild(d_nested);
console.log(throwawayNode === d_nested);    //true
```

#### [Node.replaceChild()](https://developer.mozilla.org/en-US/docs/Web/API/Node/replaceChild)

The Node.replaceChild() method replaces one child node of the specified element with another

```javascript
replacedNode = parentNode.replaceChild(newChild, oldChild);
```
* *newChild* is the new node to replace oldChild. If it already exists in the DOM, it is first removed.
* *oldChild* is the existing child to be replaced.
* *replacedNode* is the replaced node. This is the same node as oldChild.

**Example**

```html
<div>
    <span id="childSpan">foo bar</span>
</div>
```
```javascript
var sp1 = document.createElement('span');
sp1.setAttribute('id', 'newSpan');

var sp1_content = document.createTextNode('new replacement span element.');
sp1.appendChild(sp1_content);

var sp2 = document.getElementById('childSpan');
var parentDiv = sp2.parentNode;

var replaceNode = parentDiv.replaceChild(sp1, sp2);
console.log(replaceNode === sp2);   //true
```
after replace:

```html
<div>
    <span id="newSpan">new replacement span element.</span>
</div>
```

#### [Node.normalize()](https://developer.mozilla.org/en-US/docs/Web/API/Node/normalize)

The **Node.normalize()** method puts the specified node and all of its sub-tree into a "normalized" form. In a normalized sub-tree, no text nodes in the sub-tree are empty and there are no adjacent text nodes

**Example**

```javascript
var wapper = document.createElement('div');
wapper.appendChild(document.createTextNode('Part 1'));
wapper.appendChild(document.createTextNode('Part 2'));

var childs = wapper.childNodes;
console.log(childs.length);     //2
console.log(wapper.childNodes[0].textContent);  //Part 1
console.log(wapper.childNodes[1].textContent);  //Part 2

wapper.normalize();
console.log(childs.length);     //1
console.log(wapper.childNodes[0].textContent);  //Part 1Part 2
```


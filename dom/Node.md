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

添加一个子节点到指定元素内的尾部。如果给定的子节点已经存在文档内，将会把这个节点移动到新的位置

**Example1**

创建新的元素<p>并添加到<body>元素中

```javascript
var p = document.createElement('p');
document.body.appendChild(p);
```
结果:

```html
<body>
    <p></p>
</body>
```

**Example2**
appendChild之前，html如下：

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
由于div1已经存在，所以appendChild把div1移到div0的内部

```html
<body>
    <div id="div0"><div id="div1"></div></div>
</body>
```

##### [Node.cloneNode()](https://developer.mozilla.org/en-US/docs/Web/API/Node/cloneNode)

The *Node.cloneNode()* method returns a duplicate of the node on which this method was called
返回一个新的元素，它是指定元素的一个拷贝。

```javascript
var dupNode = node.cloneNode(deep);
```
* *node:* 要被复制的元素
* *deep:* 如果为ture就是深拷贝（不仅复制当前节点，而且复制子节点），为false是浅拷贝（只复制当前节点），默认是浅拷贝。
* *dupNode:* 复制后的元素

浅拷贝的例子

初始html为:

```html
<body>
    <div id="div1"><div id="subdiv1"></div></div>
    <div id="div0"></div>
</body>
```
```javascript
var div1 = document.getElementById('div1');
var div0 = document.getElementById('div0');
// 不指定参数默认为浅拷贝，等价于div1.cloneNode(false)
var newdiv1 = div1.cloneNode();
div0.appendChild(newdiv1);
```
执行后html为：

```html
<body>
    <div id="div1"><div id="subdiv1"></div></div>
    <div id="div0"><div id="div1"></div></div>
</body>
```

深拷贝的例子

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

判断指定的元素是否有子节点

##### [Node.insertBefore()](https://developer.mozilla.org/en-US/docs/Web/API/Node/insertBefore)

在当前元素的子节点前插入一个子节点

```javascript
var insertedElement = parentElement.insertBefore(newElement, referenceElement);
```

* *insertedElement:* 插入后的新的节点
* *parentElement:* 指定的父节点
* *newElement:* 要插入的新的节点
* *referenceElement:* 在哪个节点前插入（它是父节点的一个子节点）

**Example**

```html
<div id="parentElement">
    <span id="childElement">foo bar</span>
</div>
```
```javascript
// 创建一个新节点<span>
var sp1 = document.createElement('span');
// sp2一个子节点
var sp2 = document.getElementById('childElement');
// 通过子节点获取父节点
var parent = sp2.parentNode;
// 在sp2之前插入新创建的span节点
var newnode = parent.insertBefore(sp1, sp2);
console.log(newnode === sp1);   //ture
```
插入之后的html为:

```html
<div id="parentElement">
    <span></span>
    <span id="childElement">foo bar</span>
</div>
```

##### [Node.removeChild()](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild)

在指定的节点上删除一个子节点，返回这个删除的子节点

```javascript
var oldChild = element.removeChild(child);
```

* *child* 要被删除的节点
* *element* 指定的父节点
* *oldChild* 删除后的节点，oldChild === child.

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

在指定的节点上用一个新的子节点替换另一个子节点

```javascript
replacedNode = parentNode.replaceChild(newChild, oldChild);
```
* *newChild* 要替换的新的节点
* *oldChild* 要被替换的子节点
* *replacedNode* 被替换的节点，它和oldChild相同
* *parentNode* 指定的父节点

**Example**

```html
<div>
    <span id="childSpan">foo bar</span>
</div>
```
```javascript
// 创建一个新的节点span
var sp1 = document.createElement('span');
// 给新节点加属性
sp1.setAttribute('id', 'newSpan');
// 创建文本节点并加入到新创建的节点中
var sp1_content = document.createTextNode('new replacement span element.');
sp1.appendChild(sp1_content);
// 获取子节点sp2
var sp2 = document.getElementById('childSpan');
// 获取父节点
var parentDiv = sp2.parentNode;
// 用sp1替换sp2
var replaceNode = parentDiv.replaceChild(sp1, sp2);
console.log(replaceNode === sp2);   //true
```
替换之后的html如下:

```html
<div>
    <span id="newSpan">new replacement span element.</span>
</div>
```

#### [Node.normalize()](https://developer.mozilla.org/en-US/docs/Web/API/Node/normalize)

The **Node.normalize()** method puts the specified node and all of its sub-tree into a "normalized" form. In a normalized sub-tree, no text nodes in the sub-tree are empty and there are no adjacent text nodes
把父节点内的子节点格式化，如果有多个文本子节点，格式化后会变成一个子节点。

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


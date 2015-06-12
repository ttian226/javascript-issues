#### Node

A Node is an interface from which a number of DOM types inherit, and allows these various types to be treated (or tested) similarly

The following interfaces all inherit from Node its methods and properties: ```Document```, ```Element```, ```CharacterData``` (which ```Text```, ```Comment```, and CDATASection inherit), ProcessingInstruction, DocumentFragment, DocumentType, Notation, Entity, EntityReference

#### Properties

##### Node.childNodes

The Node.childNodes read-only property returns a live collection of child nodes of the given element.

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
*Note:* Whitespace inside elements is considered as text

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
After dom loaded, run script:

```javascript
var nodes = document.body.childNodes;
var len = nodes.length;
for (var i = 0; i < len; i++) {
    var type = nodes[i].nodeType;
    var name = nodes[i].nodeName;
    console.log('nodeName:' + name + ' nodeType:' + type);
}

// output
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


##### Node.firstChild

The Node.firstChild read-only property returns the node's first child in the tree, or null if the node is childless

```html
<p id="para-01"><span>First span</span><span>Middle span</span><span>Last span</span></p>
```
```javascript
var pNode = document.getElementById('para-01');
var first = pNode.firstChild;   // <span>First span</span>
```
##### Node.lastChild

The Node.lastChild read-only property returns the last child of the node. It returns null if there are no child elements

```html
<p id="para-01"><span>First span</span><span>Middle span</span><span>Last span</span></p>
```
```javascript
var pNode = document.getElementById('para-01');
var last = pNode.lastChild;   // <span>Last span</span>
```

*Note:* If the Node contains whitespace, the firstNode or lastNode return a text node

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

##### Node.nodeName

interface | nodeName value
----------|---------------
Comment|"#comment"
Text|"#text"
Element|The value of Element.tagName

Node.nodeType

Node.nodeValue
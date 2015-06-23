#### [ParentNode](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode)

The **ParentNode** interface contains methods that are particular to Node objects that can have children.

ParentNode is a raw interface and no object of this type can be created; it is implemented by Element, Document, and DocumentFragment objects.

#### Properties

##### [ParentNode.childElementCount](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/childElementCount)

The ParentNode.childElementCount read-only property returns an unsigned long representing the number of child elements of the given element.

**Example**

```html
<body>
    <!-- This is a comment node! -->
    <p>Click the button get info about the body element's child nodes.</p>
    <button onclick="myFunction()">Try it</button>
    <p><strong>Note:</strong> Whitespace inside elements is considered as text, and text
    is considered as nodes. Comments are also considered as nodes.</p>
    <p id="demo"></p>
</body>
```

```javascript
var body = document.body;
var bodyNodes = body.childNodes;
console.log(bodyNodes.length);  //13  all type of node count
console.log(body.childElementCount);    //4  only element node count
```

*The returned value contains the number of child element nodes, not the number of all child nodes (like text and comment nodes).*

##### [ParentNode.children](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/children)

Node.children is a read-only property that returns a live [HTMLCollection](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection) of the child elements of Node

```javascript
var elList = elementNodeReference.children;
```
elList is a HTMLCollection, which is an ordered collection of DOM elements that are children of elementNodeReference. If there are no element children, then elList contains no elements and has a length of 0

**Example**

```javascript
var children = document.body.children;

// now children is a HTMLCollection object that contain 4 items
var len = children.length;  //4
```

##### [ParentNode.firstElementChild](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/firstElementChild)

The **ParentNode.firstElementChild** read-only property returns the object's first child Element, or null if there are no child elements

##### [ParentNode.lastElementChild](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/lastElementChild)

The **ParentNode.lastElementChild** read-only property returns the object's last child Element or null if there are no child elements

**Example**

```javascript
var body = document.body;

// get first element
var firstEle = body.firstElementChild;

// get last element
var lastEle = body.lastElementChild;
```

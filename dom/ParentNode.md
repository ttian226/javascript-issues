#### [ParentNode](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode)

The **ParentNode** interface contains methods that are particular to Node objects that can have children.

ParentNode is a raw interface and no object of this type can be created; it is implemented by Element, Document, and DocumentFragment objects.

#### Properties

##### [ParentNode.childElementCount](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/childElementCount)

childElementCount属性返回子元素（只返回elements类型）的数量。

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
console.log(bodyNodes.length);  //13  所有节点类型的数量
console.log(body.childElementCount);    //4  只是包含元素节点的数量
```

##### [ParentNode.children](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/children)

返回节点中的子元素列表，它是动态的[HTMLCollection](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection)类型

```javascript
var elList = elementNodeReference.children;
```
elList是一个HTMLCollection对象，它是一个节点中有序的DOM子元素的集合。如果没有子元素，它的长度为0

**Example**

```javascript
var children = document.body.children;

// now children is a HTMLCollection object that contain 4 items
var len = children.length;  //4
```

##### [ParentNode.firstElementChild](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/firstElementChild)

返回节点中的第一个子元素

##### [ParentNode.lastElementChild](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/lastElementChild)

返回节点中的最后一个子元素

**Example**

```javascript
var body = document.body;

// get first element
var firstEle = body.firstElementChild;

// get last element
var lastEle = body.lastElementChild;
```

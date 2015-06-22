#### [ParentNode](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode)

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

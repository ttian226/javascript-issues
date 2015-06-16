#### [HTMLCollection](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection)

The HTMLCollection interface represents a generic collection (array-like object) of elements (in document order) and offers methods and properties for selecting from the list.

##### HTMLCollection.length

Returns the number of items in the collection

##### [HTMLCollection.item()](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection/item)

Returns the specific node at the given zero-based index into the list. Returns null if the index is out of range.

##### HTMLCollection.namedItem()

Returns the specific node whose ID or, as a fallback, name matches the string specified by name. Matching by name is only done as a last resort, only in HTML, and only if the referenced element supports the name attribute. Returns null if no node exists by the given name.

**Example**

```html
<div id="div1" name="test1"></div>
<div id="div2" name="test2"></div>
<div id="div3" name="test3"></div>
```

```javascript
// divs is a HTMLCollection object contain 3 items
var divs = document.getElementsByTagName('div');

// get the length of divs
var length = divs.length;   //3

// get first element
var div1 = divs.item(0);    //equal to divs[0]

// get the element by its name
var div2 = divs.namedItem('test2');
```



#### Document

#### Properties

##### document.body

Returns the <body> or <frameset> node of the current document, or null if no such element exists.



#### Methods

##### document.getElementById()

Returns a reference to the element by its ID.
* element is a reference to an **Element** object, or null if an element with the specified ID is not in the document
* id is a case-sensitive string representing the unique ID of the element being sought

##### document.getElementsByTagName()

Returns an **HTMLCollection** of elements with the given tag name.

##### document.getElementsByName()

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
##### document.getElementsByClassName()

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

##### document.querySelector(selectors)
Returns the first element within the document (using depth-first pre-order traversal of the document's nodes) that matches the specified group of selectors.

```javascript
var element = document.querySelector(selectors);
```
* **element** is an element object.
* **selectors** is a string containing one or more CSS selectors separated by commas

##### document.querySelectorAll(selectors)
Returns a list of the elements within the document (using depth-first pre-order traversal of the document's nodes) that match the specified group of selectors. The object returned is a **NodeList**.

#### Document

#### Properties

##### document.body

Returns the <body> or <frameset> node of the current document, or null if no such element exists.

##### document.documentElement

The Document.documentElement read-only property returns the Element that is the root element of the document (for example, the <html> element for HTML documents).

##### document.forms

forms returns a collection (an HTMLCollection) of the form elements within the current document.

##### document.head

Returns the <head> element of the current document. If there are more than one <head> elements, the first one is returned

##### document.images

document.images returns a collection of the images in the current HTML document.

*Note*
```document.images.length``` – property, returns the number of images on the page.

##### document.scripts

Returns a list of the script elements in the document. The returned object is an HTMLCollection.

##### document.title

Gets or sets the title of the document

##### document.anchors

anchors returns a list of all of the anchors in the document.

*Note*
the returned set of anchors only contains those anchors created with the name attribute, not those created with the id attribute

```html
<h1>Title</h1>
<h2><a name="contents">Contents</a></h2>
<ul id="toc"></ul>

<h2><a name="plants">Plants</a></h2>
<ol>
    <li>Apples</li>
    <li>Oranges</li>
    <li>Pears</li>
</ol>

<h2><a name="veggies">Veggies</a></h2>
<ol>
    <li>Carrots</li>
    <li>Celery</li>
    <li>Beats</li>
</ol>
```

document.anchors reutrn a array: [<a name="contents">Contents</a>, <a name="plants">Plants</a>, <a name="veggies">Veggies</a>],contain 3 items

##### document.links

The links property returns a collection of all <area> elements and <a> elements in a document with a value for the href attribute

##### document.location

The Document.location read-only property returns a **Location** object, which contains information about the URL of the document and provides methods for changing that URL and loading another URL

##### document.URL

The URL read-only property of the Document interface returns the document location as a string

```javascript
document.location = 'http://www.mozilla.org';   //Equivalent to
document.location.href = 'http://www.mozilla.org';
```

##### document.referrer

Returns the [URI](http://www.w3.org/Addressing/#background) of the page that linked to this page.

##### document.domain

Gets/sets the domain portion of the origin of the current document, as used by the same origin policy.

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

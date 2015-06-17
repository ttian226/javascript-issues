#### [Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)

#### Properties

##### [Element.attributes](https://developer.mozilla.org/en-US/docs/Web/API/Element/attributes)

The **Element.attributes** property returns a live collection of all attribute nodes registered to the specified node. It is a [NamedNodeMap](https://developer.mozilla.org/en-US/docs/Web/API/NamedNodeMap), not an Array, so it has no Array methods and the Attr nodes' indexes may differ among browsers. To be more specific, attributes is a key/value pair of strings that represents any information regarding that attribute.

**Example**

```html
<div id="div1" name="test1" class="cls1" myattr="my_val"></div>
```
```javascript
var div = document.getElementById('div1');

// attrs is a NamedNodeMap object, is array like, each item is Attr object
var attrs = div.attributes;

// iterator attrs
for (var i = 0; i < attrs.length; i++) {
    // one is Attr object
    var one = attrs[i],

        // get it's attr name
        name = one.name,

        // get it's attr value
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

className gets and sets the value of the class attribute of the specified element.

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

The Element.id property represents the element's identifier, reflecting the id global attribute.

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

Returns the name of the element

*Note:* tagName returns the element name in the uppercase form, The value of tagName is the same as that of nodeName.

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

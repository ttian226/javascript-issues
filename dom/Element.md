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

```html
<div id="div1" name="test1" class="cls1" myattr="my_val"></div>
```
```javascript
var div = document.getElementById('div1');

// get tag name
var tagname = div.tagName;  //'DIV'
console.log(tagname.toLowerCase()); //'div'
```



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

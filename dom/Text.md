#### [Text](https://developer.mozilla.org/en-US/docs/Web/API/Text)

##### [Text.splitText()](https://developer.mozilla.org/en-US/docs/Web/API/Text/splitText)

The **Text.splitText()** method breaks the Textnode into two nodes at the specified offset, keeping both nodes in the tree as siblings.

Separated text nodes can be concatenated using the [Node.normalize()](https://developer.mozilla.org/en-US/docs/Web/API/Node/normalize) method.

```html
<p id="p">foobar</p>
```

```javascript
var p = document.getElementById('p');
textnode = p.firstChild;

// now replacementNode = 'bar', textnode = 'foo'
var replacementNode = textnode.splitText(3);
```
after splitText:

```html
<p>
    foo
    bar
</p>
```

```javascript
var span = document.createElement('span');
span.appendChild(document.createTextNode('span contents'));

p.insertBefore(span, replacementNode);
```

```html
<p>
    foo
    <span>
        span contents
    </span>
    bar
</p>
```


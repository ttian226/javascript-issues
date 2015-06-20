#### [HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement)

The **HTMLElement** interface represents any HTML element. Some elements directly implement this interface, others implement it via an interface that inherits it.

#### Properties

Inherits properties from its parent, [Element](https://developer.mozilla.org/en-US/docs/Web/API/Element), and implements those from GlobalEventHandlers and TouchEventHandlers.

##### HTMLElement.draggable

Is a Boolean indicating if the element can be dragged.

##### HTMLElement.hidden

Is a Boolean indicating if the element is hidden or not.

##### [HTMLElement.style](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style)

The **HTMLElement.style** property returns a [CSSStyleDeclaration](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration) object that represents the element's style attribute.

Setting style:

```html
<div id="test">test</div>
```

```javascript
elt.style.color = "blue";  // Directly

var st = elt.style;
st.color = "blue";  // Indirectly
```

After set style:

```html
<div id="test" style="color:blue">test</div>
```

*It is generally better to use the style property than to use elt.setAttribute('style', '...'), since using the style property will not overwrite other CSS properties that may be specified in the style attribute.*

Getting style:

**Example1**

```html
<div id="test" style="color:blue">test</div>
```

```javascript
var div = document.getElementById('test');

// get div's color
var color = div.style.color;

// or
var st = div.style;
color = st.color;
```

**Example2**

```html
<div id="test">test</div>
```

```css
#test {
    color: blue
}
```

```javascript
var div = document.getElementById('test');

// get div's color
var color = div.style.color;    // color is "", div.style can only get the inline style
```

*The style property is not useful for learning about the element's style in general, since it represents only the CSS declarations set in the element's inline style attribute, not those that come from style rules elsewhere, such as style rules in the `<head>` section, or external style sheets. To get the values of all CSS properties for an element you should use window.getComputedStyle() instead*

##### [HTMLElement.title](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/title)

The **HTMLElement.title** property represents the title of the element, the text usually displayed in a 'tool tip' popup when the mouse is over the displayed node.

**Example**

```html
<button id="btn1">button1</button>
```

```javascript
var button1 = document.getElementById('btn1');
button1.title = "click to refresh";
```

After set title:

```html
<button id="btn1" title="click to refresh">button1</button>
```

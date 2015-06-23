#### [Event](https://developer.mozilla.org/en-US/docs/Web/API/Event)

The **Event** interface represents any event of the DOM. It contains common properties and methods to any event.

#### Properties

##### [Event.target](https://developer.mozilla.org/en-US/docs/Web/API/Event/target)

A reference to the object that dispatched the event. It is different than [event.currentTarget](https://developer.mozilla.org/en-US/docs/Web/API/Event/currentTarget) when the event handler is called during the bubbling or capturing phase of the event.

**Example**

```html
<ul>
    <li id="li1"></li>
    <li id="li2"></li>
    <li id="li3"></li>
</ul>
```

```javascript
var ul = document.querySelector('ul');

ul.addEventListener('click', function(e) {
    console.log(e.target);
});

// e.target reference to the ul element or li element that has been clicked(ul or li element)
```


##### [Event.currentTarget](https://developer.mozilla.org/en-US/docs/Web/API/Event/currentTarget)

Identifies the current target for the event, as the event traverses the DOM. It always refers to the element the event handler has been attached to as opposed to event.target which identifies the element on which the event occurred.

**Example**

```html
<ul>
    <li id="li1"></li>
    <li id="li2"></li>
    <li id="li3"></li>
</ul>
```

```javascript
var ul = document.querySelector('ul');

ul.addEventListener('click', function(e) {
    console.log(e.currentTarget);
});

// when click li element e.currentTarget always reference to ul element
```

##### [Event.type](https://developer.mozilla.org/en-US/docs/Web/API/Event/type)

Returns a string containing the type of event.

#### Methods

##### [Event.preventDefault()](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)

Cancels the event if it is cancelable, without stopping further propagation of the event.

*The browser has default behaviors that will respond when certain events occur in the document. The most common event is a link being clicked. When a click event occurs on an <a> element, it will bubble up to the document level of the DOM, and the browser will interpret the href attribute and reload the window at the new address.

In Web applications, developers usually want to manage the navigation themselves, without causing the page to refresh. To do this, we need to prevent the browser’s default response to clicks and instead do our own thing. To do this, we call event.preventDefault()*

```html
<a href="http://smashingmagazine.com">Go to Smashing Magazine</a>
```

```javascript
var a = document.querySelector('a');

a.addEventListener('click', function(e) {
    e.preventDefault();
    alert('Default behaviour prevented');
});
```

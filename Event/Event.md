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

#### Methods

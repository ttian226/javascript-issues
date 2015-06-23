#### [EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)

EventTarget is an interface implemented by objects that can receive events and may have listeners for them.

##### [EventTarget.addEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)

The **EventTarget.addEventListener()** method registers the specified listener on the EventTarget it's called on. The event target may be an [Element](https://developer.mozilla.org/en-US/docs/Web/API/Element) in a document, the [Document](https://developer.mozilla.org/en-US/docs/Web/API/Document) itself, a [Window](https://developer.mozilla.org/en-US/docs/Web/API/Window), or any other object that supports events (such as XMLHttpRequest).

```javascript
target.addEventListener(type, listener[, useCapture]);
```

**type:** This is the name or type of event that you would like to listen to. It could be any of the standard DOM events (`click`, `mousedown`, `touchstart`, `transitionEnd`, etc.) 

**listener:** This function gets called when the event happens. The event object, containing data about the event, is passed as the first argument.

**useCapture:** This declares whether the callback should be fired in the “capture” phase.

**Example1**

```html
<button id="element">click me</button>
```

```javascript
var element = document.getElementById('element');

function callback() {
    alert('ok');
}

element.addEventListener('click', callback);
```

#### Maintaining Callback Context

```javascript
var element = document.getElementById('element');

var user = {
    firstname: 'wang',
    greeting: function() {
        alert('My name is ' + this.firstname);
    }
};

element.addEventListener('click', user.greeting);

// alert => 'My name is undefined'
```

Using Anonymous Functions:

```javascript
element.addEventListener('click', function() {
    user.greeting();
});

// alert => 'My name is wang'
```

*The method isn’t so good because now we don’t have a handle on the function when we want to remove it with .removeEventListener(). Plus, it’s pretty ugly. I prefer to use the .bind() method to generate a new function (bound) that will always run in the given context. We then pass that function as the callback to .addEventListener()*

Function.prototype.bind:

```javascript
// Overwrite the original function with
// one bound to the context of 'user'
user.greeting = user.greeting.bind(user);

// Attach the bound user.greeting as a callback
element.addEventListener('click', user.greeting);
```

We also have a reference to the callback at hand, which we can use to unbind the listener if need be.

```javascript
element.removeEventListener('click', user.greeting);
```

##### [EventTarget.removeEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener)

Removes the event listener previously registered with **EventTarget.addEventListener()**

```javascript
target.removeEventListener(type, listener[, useCapture])
```
**type:** A string representing the event type to remove.

**listener:** The EventListener function to remove from the event target

**Example1**

```html
<button id="element">click me</button>
```

```javascript
var element = document.getElementById('element');

function callback() {
    alert('ok once');
    element.removeEventListener('click', callback);
}

element.addEventListener('click', callback);
```

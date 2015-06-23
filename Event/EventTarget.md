#### [EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)

EventTarget is an interface implemented by objects that can receive events and may have listeners for them.

##### [EventTarget.addEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)

The **EventTarget.addEventListener()** method registers the specified listener on the EventTarget it's called on. The event target may be an [Element](https://developer.mozilla.org/en-US/docs/Web/API/Element) in a document, the [Document](https://developer.mozilla.org/en-US/docs/Web/API/Document) itself, a [Window](https://developer.mozilla.org/en-US/docs/Web/API/Window), or any other object that supports events (such as XMLHttpRequest).

```javascript
target.addEventListener(type, listener[, useCapture]);
```

*type* This is the name or type of event that you would like to listen to. It could be any of the standard DOM events (`click`, `mousedown`, `touchstart`, `transitionEnd`, etc.) 

*listener* This function gets called when the event happens. The event object, containing data about the event, is passed as the first argument.

*useCapture* This declares whether the callback should be fired in the “capture” phase.

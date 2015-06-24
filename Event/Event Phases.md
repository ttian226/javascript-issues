#### Event Phases

When a DOM event fires in your app, it doesn’t just fire once where the event originated; it embarks on a journey of three phases. In short, the event flows from the document’s root to the target (i.e. capture phase), then fires on the event target (target phase), then flows back to the document’s root (bubbling phase)

![Event Phases](http://media.mediatemple.netdna-cdn.com/wp-content/uploads/2013/10/eventflow.png)

**Example**

```html
<body>
  <div class="">
    <ul>
      <li>Click on a layer to watch the event move through the DOM tree.</li>
    </ul>
  </div>
</body>
```

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 20px;
  transition: background 800ms;
}

html {
  height: 100%;
  background: hsl(193, 66%, 55%);
  font: bold 40px helvetica, sans-serif;
  color: red;
}

body {
  height: 100%;
  background: hsl(193, 66%, 65%);
}

div {
  height: 100%;
  background: hsl(193, 66%, 75%);
}

ul {
  height: 100%;
  list-style: none;
  background: hsl(193, 66%, 85%);
}

li {
  height: 100%;
  background: hsl(193, 66%, 95%);
}

.highlight {
  background: red;
}
```

```javascript
var html = document.documentElement;
var body = document.body;
var div = body.querySelector('div');
var ul = body.querySelector('ul');
var li = body.querySelector('li');
var pause = 200;

// Capture
html.addEventListener('click', callback, true);
body.addEventListener('click', callback, true);
div.addEventListener('click', callback, true);
ul.addEventListener('click', callback, true);
li.addEventListener('click', callback, true);

// Bubble
html.addEventListener('click', callback, false);
body.addEventListener('click', callback, false);
div.addEventListener('click', callback, false);
ul.addEventListener('click', callback, false);
li.addEventListener('click', callback, false);

function callback(event) {
    var ms = event.timeout = (event.timeout + pause) || 0;
    var target = event.currentTarget;
    
    setTimeout(function() {
        target.classList.add('highlight');
        setTimeout(function() {
            target.classList.remove('highlight');
        }, pause);
    }, ms);
}
```

#### Capture Phase

The first phase is the capture phase. The event starts its journey at the root of the document, working its way down through each layer of the DOM, firing on each node until it reaches the event target. The job of the capture phase is to build the propagation path, which the event will travel back through in the bubbling phase.

As mentioned, you can listen to events in the capture phase by setting the third argument of addEventListener to true. 

*when click li element, capture order: html > body > div > ul > li*

```javascript
html.addEventListener('click', callback, true);
body.addEventListener('click', callback, true);
div.addEventListener('click', callback, true);
ul.addEventListener('click', callback, true);
li.addEventListener('click', callback, true);
```
*when click li element, capture order: html > body > stop*

```javascript
html.addEventListener('click', callback, true);
body.addEventListener('click', callback, true);
div.addEventListener('click', function(e) {
    e.stopPropagation();
}, true);
ul.addEventListener('click', callback, true);
li.addEventListener('click', callback, true);
```

#### Target Phase

An event reaching the target is known as the target phase. The event fires on the target node, before reversing and retracing its steps, propagating back to the outermost document level.

#### Bubbling Phase

After an event has fired on the target, it doesn’t stop there. It bubbles up (or propagates) through the DOM until it reaches the document’s root. This means that the same event is fired on the target’s parent node, followed by the parent’s parent, continuing until there is no parent to pass the event onto.

*when click li element, bubble order: li > ul > div > body > html*

```javascript
html.addEventListener('click', callback, false);
body.addEventListener('click', callback, false);
div.addEventListener('click', callback, false);
ul.addEventListener('click', callback, false);
li.addEventListener('click', callback, false);
```
*when click li element, nothing happened*

```javascript
html.addEventListener('click', callback, false);
body.addEventListener('click', callback, false);
div.addEventListener('click', callback, false);
ul.addEventListener('click', callback, false);
li.addEventListener('click', function(e) {
    e.stopPropagation();
}, false);
```
*when click li element, bubble order: li > ul > stop*

```javascript
html.addEventListener('click', callback, false);
body.addEventListener('click', callback, false);
div.addEventListener('click', function(e) {
    e.stopPropagation();
}, false);
ul.addEventListener('click', callback, false);
li.addEventListener('click', callback, false);
```

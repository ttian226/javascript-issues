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

##### [Event.bubbles](https://developer.mozilla.org/en-US/docs/Web/API/Event/bubbles)

Indicates whether the given event bubbles up through the DOM or not

##### [Event.cancelable](https://developer.mozilla.org/en-US/docs/Web/API/Event/cancelable)

Indicates whether the event is cancelable or not

##### [Event.defaultPrevented](https://developer.mozilla.org/en-US/docs/Web/API/Event/defaultPrevented)

Returns a boolean indicating whether or not [event.preventDefault()](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault) was called on the event

##### [Event.timeStamp](https://developer.mozilla.org/en-US/docs/Web/API/Event/timeStamp)

Returns the time (in milliseconds since the epoch) at which the event was created.

#### Methods

##### [Event.preventDefault()](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)

Cancels the event if it is cancelable, without stopping further propagation of the event.

The browser has default behaviors that will respond when certain events occur in the document. The most common event is a link being clicked. When a click event occurs on an <a> element, it will bubble up to the document level of the DOM, and the browser will interpret the href attribute and reload the window at the new address.

In Web applications, developers usually want to manage the navigation themselves, without causing the page to refresh. To do this, we need to prevent the browser’s default response to clicks and instead do our own thing. To do this, we call event.preventDefault().

**Example1**

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

**Example2**

```html
<body>
    <p>Please click on the checkbox control.</p>

    <form>
        <input type="checkbox" id="my-checkbox" />
        <label for="my-checkbox">Checkbox</label>
    </form>
</body>
```

```javascript
var stopDefAction = function(e) {
    e.preventDefault();
};

document.getElementById('my-checkbox').addEventListener('click', stopDefAction, false);
```

##### [Event.stopPropagation()](https://developer.mozilla.org/en-US/docs/Web/API/Event/stopPropagation)

阻止当前事件的冒泡

例子：

```html
<div id="parent" style="padding:100px"><div id="child">child</div></div>
```

```javascript
// 以下代码需要在DOMContentLoaded事件后执行
var parent = document.getElementById('parent');
var child = document.getElementById('child');

parent.addEventListener('click', callback, false);
child.addEventListener('click', callback1, false);

// 父节点事件函数
function callback() {
    console.log('parent event');
}

// 子节点事件函数
function callback1(e) {
    e.stopPropagation();    //阻止冒泡
    console.log('child event');
}
```

* 点击子元素，由于在子元素中阻止事件冒泡，只会触发子元素事件。
* 如果不阻止事件冒泡会先触发子元素事件，然后会触发父元素事件。

*更多参考 [事件的三个阶段](https://github.com/ttian226/javascript-issues/blob/master/Event/Event%20Phases.md)*

##### [Event.stopImmediatePropagation()](https://developer.mozilla.org/en-US/docs/Web/API/Event/stopImmediatePropagation)

除了阻止事件冒泡，而且还阻止了当前元素的同类事件

例子：

```html
<div>
    <p>paragraph</p>
</div>
```
```css
p { height: 30px; width: 150px; background-color: #ccf; }
div {height: 30px; width: 150px; background-color: #cfc; }
```
```javascript
document.addEventListener('DOMContentLoaded', complete, false);

function complete(e) {
    var p = document.querySelector('p');
    var div = document.querySelector('div');

    p.addEventListener("click", function (event) {
        console.log("我是p元素上被绑定的第一个监听函数");
    }, false);

    p.addEventListener("click", function (event) {
        console.log("我是p元素上被绑定的第二个监听函数");
        event.stopImmediatePropagation();
        //执行stopImmediatePropagation方法,阻止click事件冒泡,并且阻止p元素上绑定的其他click事件的事件监听函数的执行.
    }, false);

    p.addEventListener("click", function (event) {
        console.log("我是p元素上被绑定的第三个监听函数");
        //该监听函数排在上个函数后面,该函数不会被执行.
    }, false);

    div.addEventListener("click", function (event) {
        console.log("我是div元素,我是p元素的上层元素");
        //p元素的click事件没有向上冒泡,该函数不会被执行.
    }, false);
}
```

* 元素p同时绑定了3个click事件
* 在第二个监听函数上如果使用`stopPropagation()`会依次触发3个监听函数。事件不会冒泡
* 在第二个监听函数上如果使用`stopImmediatePropagation()`，会阻止p元素上绑定的其他click事件的事件监听函数的执行（第一个监听函数被执行，因为它位于第二个监听函数的前面）


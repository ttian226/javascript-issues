#### Event Phases

When a DOM event fires in your app, it doesn’t just fire once where the event originated; it embarks on a journey of three phases. In short, the event flows from the document’s root to the target (i.e. capture phase), then fires on the event target (target phase), then flows back to the document’s root (bubbling phase)

![事件的三个阶段](http://media.mediatemple.netdna-cdn.com/wp-content/uploads/2013/10/eventflow.png)

#### 事件捕获

`addEventListener()`第三个参数设置为true时，可以捕获事件。事件捕获顺序是从文档的根节点开始，一直到目标节点结束。

```javascript
html.addEventListener('click', callback, true);
body.addEventListener('click', callback, true);
div.addEventListener('click', callback, true);
ul.addEventListener('click', callback, true);
li.addEventListener('click', callback, true);
```

在这个例子中鼠标点击`<li>`元素，从`<html>`节点开始依次捕获点击事件，直到目标节点`<li>`。顺序是：html > body > div > ul > li。事件捕获后就不会触发事件冒泡。[完整例子](http://jsbin.com/rijuko/edit?html,js)

使用`stopPropagation()`终止事件捕获，下面的例子在div节点上终止了事件捕获，会导致ul,li节点的事件不会被触发。[完整例子](http://jsbin.com/yocahe/edit?html,js)

```javascript
function callback(event) {
    // 终止捕获
    var target = event.currentTarget;
    if (target.nodeName === 'DIV') {
        event.stopPropagation();
    }
    // ...
}
```

#### Target Phase

An event reaching the target is known as the target phase. The event fires on the target node, before reversing and retracing its steps, propagating back to the outermost document level.

#### 事件冒泡

`addEventListener()`最后一个参数设置`false`可以禁止捕获。（禁止捕获可以触发事件冒泡）当事件在目标节点触发后，会依次沿着父节点向上传播，直到文档的根节点（它的路径正好与事件捕获相反）

```javascript
html.addEventListener('click', callback, false);
body.addEventListener('click', callback, false);
div.addEventListener('click', callback, false);
ul.addEventListener('click', callback, false);
li.addEventListener('click', callback, false);
```

这个例子中，当点击`<li>`节点后，事件传播的路径为：li > ul > div > body > html。[完整代码](http://jsbin.com/coseho/edit?html,js)

使用`stopPropagation()`阻止事件冒泡。**它既可以阻止事件捕获，又可以阻止事件冒泡的传播。**

```javascript
function callback(event) {
    // 阻止冒泡继续传播
    var target = event.currentTarget;
    if (target.nodeName === 'DIV') {
        event.stopPropagation();
    }
    // ...
}
```

[完整代码](http://jsbin.com/zelefe/edit?html,js)

事件冒泡机制可以实现事件委托，我们没有必要监听某个指定的元素上的事件，而是在父节点上监听多个元素的事件。这样会大大提高性能。

#### Stopping Propagation

Interrupting the path of the event at any point on its journey (i.e. in the capture or bubbling phase) is possible simply by calling the stopPropagation method on the event object. Then, the event will no longer call any listeners on nodes that it travels through on its way to the target and back to the document.

```javascript
child.addEventListener('click', function(event) {
    event.stopPropagation();
});

parent.addEventListener('click', function(event) {
    // If the child element is clicked
    // this callback will not fire
});
```
Calling `event.stopPropagation()` will not prevent any additional event listeners from being called on the current target if multiple listeners for the same event exist. If you wish to prevent any additional listeners from being called on the current node, you can use the more aggressive `event.stopImmediatePropagation()` method.

```javascript
child.addEventListener('click', function(event) {
    event.stopImmediatePropagation();
});

child.addEventListener('click', function(event) {
    // If the child element is clicked
    // this callback will not fire
});
```

#### 一个例子

```javascript
var overlay = document.querySelector('.overlay');

// 点击overlay时阻止冒泡
overlay.addEventListener('click', function(event) {
    event.stopPropagation();
});

// 点击外部时才响应事件
document.addEventListener('click', function(event) {
    if (overlay.parentNode) {
        overlay.parentNode.removeChild(overlay);
    }
});
```

[完整代码](http://jsbin.com/miyupu/edit?html,js,output)

也可以不使用`stopPropagation()`来实现。

```javascript
document.addEventListener('click', function (e) {
    if (e.target !== overlay) {
        if (overlay.parentNode) {
            overlay.parentNode.removeChild(overlay);
        }
    }
});
```

[完整代码](http://jsbin.com/ceciwi/edit?html,js)

*参考文章 [An Introduction To DOM Events](http://www.smashingmagazine.com/2013/11/12/an-introduction-to-dom-events/)*

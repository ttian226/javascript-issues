#### dragstart

当用户开始拖拽元素时触发

#### dragenter

当拖拽的元素进入一个有效的目标元素时触发

#### dragover

当被拖拽元素在目标元素上移动时触发（每100毫秒触发一次）。通过阻止浏览器默认行为设置元素为可拖放元素。

*如果需要相应drop事件，必须要有dragover事件，并且需要阻止默认行为，如下：*

```javascript
document.addEventListener("dragover", function( event ) {
    // 阻止默认行为，可以触发drop事件
    event.preventDefault();
}, false);

//有上面这段代码可以触发drop事件，否则不会触发drop事件
document.addEventListener("drop", function( event ) {
    
}, false);
```

#### dragleave

拖拽元素离开目标元素时，在目标元素上触发。

```javascript
document.addEventListener("dragleave", function( event ) {
    // 当元素离开目标元素时，重置目标元素的背景色
    if ( event.target.className == "dropzone" ) {
        event.target.style.background = "";
    }
}, false);
```

#### drop

当被拖拽的目标元素在一个有效的目标区域（元素）中放下时触发

#### dragend

当拖放结束时触发，它的目标对象为被拖拽的元素

```html
<div class="dropzone">
    <div id="draggable" draggable="true">
        This div is draggable
    </div>
</div>
<div class="dropzone"></div>
<div class="dropzone"></div>
<div class="dropzone"></div>
<div class="test"></div>
```

```css
#draggable {
    width: 200px;
    height: 20px;
    text-align: center;
    background: white;
}

.dropzone {
    width: 200px;
    height: 20px;
    background: blueviolet;
    margin-bottom: 10px;
    padding: 10px;
}

.test {
    width: 200px;
    height: 20px;
    background: dodgerblue;
    margin-bottom: 10px;
    padding: 10px;
}
```

```javascript
var dragged;

/* events fired on the draggable target */
document.addEventListener("drag", function( event ) {

}, false);

// 开始拖拽元素时触发dragstart事件
document.addEventListener("dragstart", function( event ) {
    // 获取拖拽目标元素，并存储在全局变量中
    dragged = event.target;
    // 设置拖拽目标元素半透明
    event.target.style.opacity = .5;
}, false);

document.addEventListener("dragend", function( event ) {
    // 重置被拖拽元素的透明度
    event.target.style.opacity = "";
}, false);

document.addEventListener("dragover", function( event ) {
    // 阻止默认行为，可以触发drop事件
    event.preventDefault();
}, false);

document.addEventListener("dragenter", function( event ) {
    // 当被拖拽的元素进入目标区域时，给目标元素设置不同的背景色
    if ( event.target.className == "dropzone" ) {
        event.target.style.background = "purple";
    } else if (event.target.className == "test") {
        event.target.style.background = "black";
    }

}, false);

document.addEventListener("dragleave", function( event ) {
    // 当被拖拽元素离开目标元素时，重置目标元素的背景色
    if ( event.target.className == "dropzone" ) {
        event.target.style.background = "";
    }

}, false);

document.addEventListener("drop", function( event ) {
    // 阻止某些元素的默认行为，比如<a>
    event.preventDefault();

    // 当目标元素class为dropzone时
    if ( event.target.className == "dropzone" ) {
        // 还原目标元素背景色
        event.target.style.background = "";
        // 改变被拖拽元素的位置（从原来的父元素上移到新的目标元素上）
        dragged.parentNode.removeChild( dragged );
        event.target.appendChild( dragged );
    }

}, false);
```

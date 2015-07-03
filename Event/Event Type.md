##### [DOMContentLoaded](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded)

`DOMContentLoaded`事件是在Dom树加载完成后触发，而不用等待样式文件，图片和子frame加载。而load事件是所有文件加载完成后触发。`DOMContentLoaded`事件IE9以下不支持。

```javascript
document.addEventListener('DOMContentLoaded', complete, false);

function complete(e) {
    console.log('Dom load complete!');
}
```

##### load

页面上所有元素加载完成后触发，包括Dom树，样式，图片，frame等。

* window.onload

方法1：

```javascript
window.addEventListener('load', complete, false);

function complete(e) {
    console.log('All load complete!');
}
```
方法2：

```javascript
window.onload = function(e) {
    console.log('All load complete!');
};
```

* document.body.onload，body里面所有元素全部加载完成后触发

方法1：

```javascript
document.body.onload = complete;

function complete(e) {
    console.log('Body load complete!');
}
```

方法2：

```html
<body onload="complete()"></body>
```
```javascript
function complete(e) {
    console.log('Body load complete!');
}
```

*使用`document.body.addEventListener('load', complete, false)`确不能触发load事件，原因？*

* 判断图片完全加载完成

方法1：

```html
<img src="http://***/test.jpg">
```
```javascript
var img = document.getElementsByTagName("img")[0];
img.addEventListener('load', imgLoad, false);

function imgLoad(e) {
    console.log('img loaded!');
}
```

方法2：

```html
<img src="http://***/test.jpg" onload="imgLoad()">
```
```javascript
function imgLoad(e) {
    console.log('img loaded!');
}
```

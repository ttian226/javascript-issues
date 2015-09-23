#### [HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement)

**HTMLElement**继承了Element

#### Properties

一部分属性继承自[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)

##### HTMLElement.draggable

指示元素是否可以被拖拽，当元素有draggable="true"属性时返回true，否则返回false

##### HTMLElement.hidden

指示元素是否隐藏，也可以通过改变hidden属性来设置元素隐藏或显示。

##### [HTMLElement.style](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style)

style属性返回一个[CSSStyleDeclaration](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration)对象，用来描述元素style属性。

设置style:

```html
<div id="test">test</div>
```

```javascript
elt.style.color = "blue";  // 直接设置

var st = elt.style;
st.color = "blue";  // 间接设置
```

设置之后html为:

```html
<div id="test" style="color:blue">test</div>
```

*通常来说使用`style`属性要比使用`elt.setAttribute('style', '...')`要好，因为使用`style`属性不会覆盖在style节点的样式*

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
var color = div.style.color;    // color 为 "", div.style 只能获取内联样式
```

*因为style属性无法读取在style标签内的css样式（只能获取元素的内联样式），要想获取元素全部的css属性需要使用window.getComputedStyle()来替代*

##### [HTMLElement.title](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/title)

设置或读取元素的title属性

**Example**

```html
<button id="btn1">button1</button>
```

```javascript
var button1 = document.getElementById('btn1');
button1.title = "click to refresh";
```

设置title属性之后:

```html
<button id="btn1" title="click to refresh">button1</button>
```

##### [HTMLElement.dataset](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dataset)

获取或设置自定义属性(data-*)的值

**Example**

```html
<div id="user" data-id="1234567890" data-user="johndoe" data-date-of-birth="1960-10-03">John Doe</div>
```
```javascript
var el = document.querySelector('#user');

// 读取属性值
console.log(el.dataset.id);
console.log(el.dataset.user);
console.log(el.dataset.dateOfBirth);

// 设置属性值
el.dataset.dateOfBirth = '1981-08-25';
```
设置完成之后：

```html
<div id="user" data-id="1234567890" data-user="johndoe" data-date-of-birth="1981-08-25">John Doe</div>
```

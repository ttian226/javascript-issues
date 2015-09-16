#### [DataTransfer](https://developer.mozilla.org/en-US/docs/Web/API/DataTransfer)

拖拽事件周期中会初始化一个`DataTransfer`对象,用于保存拖拽数据和交互信息.以下是它的属性和方法.

    dropEffect: 拖拽交互类型,通常决定浏览器如何显示鼠标光标并控制拖放操作.常见的取值有copy,move,link和none
    effectAllowed: 指定允许的交互类型,可以取值:copy,move,link,copyLink,copyMove,limkMove, all, none默认为uninitialized(允许所有操作)
    files: 包含File对象的FileList对象.从操作系统向浏览器拖放文件时有用.
    types: 保存DataTransfer对象中设置的所有数据类型.
    setData(format, data): 以键值对设置数据,format通常为数据格式,如text,text/html
    getData(format): 获取设置的对应格式数据,format与setData()中一致
    clearData(format): 清除指定格式的数据
    setDragImage(imgElement, x, y): 设置自定义图标


`dataTransfer`是事件对象的一个属性（`event.dataTransfer`是`DataTransfer`对象的一个实例），用于从被拖拽元素向目标元素传递字符串格式的数据。因为它是事件对象的属性，所以只能在拖放事件的事件处理程序中访问dataTransfer对象。

```javascript
document.addEventListener("dragstart", function( event ) {
    // event.dataTransfer为DataTransfer对象的实例

    // 拖拽开始时保存数据，这里保存文本类型的字符串'hello world'
    event.dataTransfer.setData('text/plain', 'Hello World');
}, false);
```

保存在`DataTransfer`对象中的数据只能在`drop`事件处理程序中读取。

```javascript
document.addEventListener("dragover", function(event) {
    event.preventDefault();
});

document.addEventListener("drop", function( event ) {
    var data = event.dataTransfer.getData('text/plain');
    console.log(data);  //打印拖拽开始时保存的数据'hello world'
}, false);
```


在页面中选择文本并拖拽,无需处理`dragstart`设置数据,浏览器自动设置选取的文本.相当于`event.dataTransfer.setData("text/plain", "this is text to drag")`.只需要在拖放目标上读取对应格式的数据即可.

例：当拖拽页面上`<p>`标签内的任意文字到`<div>`中，控制台会把相应的文字打印出来

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        .dropzone {
            width: 200px;
            height: 20px;
            background: aliceblue;
            margin-bottom: 10px;
            padding: 10px;
        }
    </style>
</head>
<body>
<p>hello world</p>
<div class="dropzone"></div>
</body>
<script>
    document.addEventListener('dragover', function(e) {
        e.preventDefault();
    });

    document.addEventListener('drop', function(e) {
        e.preventDefault();
        if (e.target.className === 'dropzone') {
            var data = e.dataTransfer.getData('text/plain');
            console.log(data);
        }
    });
</script>
</html>
```

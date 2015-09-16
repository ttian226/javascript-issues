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

`DataTransfer`对象在传递给监听器的事件对象中可以访问,如下:

```javascript
document.addEventListener("dragstart", function( event ) {
    event.dataTransfer.setData('text', 'Hello World');
    console.log(event.dataTransfer instanceof DataTransfer);    //true
}, false);
```



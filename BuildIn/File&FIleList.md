#### [FileList](https://developer.mozilla.org/en-US/docs/Web/API/FileList)

属性

#### length

文件列表的长度

方法

#### item(index)

返回指定索引的文件对象(File)

例：

`<input>`标签添加`multiple`属性，允许同时选择多个文件

```html
<input type="file" multiple id="fileitem"/>
```

```javascript
document.getElementById('fileitem').addEventListener('change', function(e) {
    var files = this.files; //这里的files是一个FileList对象
    var length = files.length;  //选择文件的个数
    var file = files[0];    //第1个文件，它是一个File对象
    //或者用item()
    var file = files.item(0);
    console.dir(file);
}, false);
```

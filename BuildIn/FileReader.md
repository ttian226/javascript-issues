#### [FileReader](https://developer.mozilla.org/en-US/docs/Web/API/FileReader)

FileReader对象使web应用可以异步读取存储在用户电脑上的文件内容，使用File或Blog对象指定要读取的文件

文件对象可以通过FileList的结果集来取得。

例子：拖拽图片到指定区域并预览图片，代码片段：

```javascript
document.addEventListener('drop', function (e) {
    // 操作系统拖放文件到浏览器需要取消默认行为
    e.preventDefault();

    // 这里e.dataTransfer.files取得的是FileList对象，遍历FileList对象
    [].forEach.call(e.dataTransfer.files, function(file) {

        // 此时file为File对象
        if (file && file.type.match('image.*')) {

            // 创建FileReader的实例
            var reader = new FileReader();

            // readAsDataURL用来读取Blob或File文件的内容，读取完毕后onload会被触发
            reader.readAsDataURL(file);

            // 读取完毕后触发的事件
            reader.onload = function(e) {

                // e.target为FileReader对象
                var img = doc.createElement('img');

                // e.target.result为文件内容
                img.src = e.target.result;
                var li = doc.createElement('li');
                li.appendChild(img);
                preview.appendChild(li);
            };
        }
    });

}, false);
```

#### iframe文件上传

```html
<body>
<form action="http://localhost/test" method="post" enctype="multipart/form-data">
    <input type="file" name="filedata" accept="image/*">
</form>
<script src="jquery-2.1.4.js"></script>
<script src="form.js"></script>
</body>
```

form.js文件

```javascript
var $form = $('form');

$form.on('change', function() {
    // 在form标签内加一个隐藏的iframe标签
    appendIframe();
    // 提交表单
    $(this).submit();
});

function appendIframe() {
    var seed = Math.floor(Math.random() * 1000);    //生成随机数
    var id = 'uploader-frame-' + seed;              //随机id，用于设置iframe的name属性和form的target属性
    var callback = 'uploader-frame-' + seed;        //随机回调函数名
    var iframe = $('<iframe name="' + id + '" style="display:none;">');
    var url = $form.attr('action');                 //取form的action属性
    var acturl = url + '?iframe=' + callback;       //拼成一个新的action路径，带上一个回调函数名

    // 给form添加target属性，并插入iframe节点，设置新的action属性
    $form.attr('target', id).append(iframe).attr('action', acturl);

    // 定义随机回调函数，上传成功后调用此函数。
    window[callback] = function(data) {
        console.log('received callback:', data);
        iframe.remove();                //移出iframe节点
        $form.removeAttr('target');     //移除form的target属性
        $form.attr('action', url);      //重置form的action属性为初始值
        window[callback] = undefined;   //给回调函数设为undefined
    };
}
```

test.php文件

```php
// 取得回调函数名
$callback = $_GET['iframe'];

$fileInfo = pathinfo($_FILES['filedata']['name']);
$extension = strtolower( $fileInfo['extension'] );
$tmppath = '/tmp';  //服务器保存图片的文件夹
$tmpname = date("YmdHis") . mt_rand(10000,99999) . '.' . $extension;

//保存到服务器的路径
$fullpath = $tmppath . '/' . $tmpname;
$res = move_uploaded_file($_FILES['filedata']['tmp_name'], $fullpath);

if ($res) {
    // 上传成功后调用回调函数
    echo '<script type="text/javascript">
            window.top.window["'.$callback.'"]("some data")
            </script>';
}
```

几点说明：

* iframe上传属于异步上传，网页不会锁死（表单提交后会在iframe中打开，所以不会对父html产生影响。）
* form的target属性要和iframe的name属性相同。
* php中script脚本是运行在iframe中的，所以要通过`window.top`或`window.parent`调用父层的js的回调函数

#### XMLHttpRequest上传文件

```html
<input type="file" name="filedata" accept="image/*">
<progress min="0" max="100" value="0">0% complete</progress>
```

```javascript
function uploadFiles(url, file, name) {
    var progressBar = document.querySelector('progress');

    var formData = new FormData();
    formData.append(name, file);

    var xhr = new XMLHttpRequest();
    xhr.upload.onprogress = function(e) {
        if (e.lengthComputable) {
            progressBar.value = (e.loaded / e.total) * 100;
            progressBar.textContent = progressBar.value;
        }
    };
    xhr.open('POST', url);
    xhr.onload = function(e) {
        if (xhr.readyState === 4 && xhr.status === 200) {
            console.log('上传成功');
        }
    };
    xhr.send(formData);
}

document.querySelector('input[type="file"]').addEventListener('change', function(e) {
    uploadFiles('http://localhost/test.php', this.files[0], this.name);
}, false);
```

```php
$fileInfo = pathinfo($_FILES['filedata']['name']);
$extension = strtolower( $fileInfo['extension'] );
$tmppath = '/tmp';
$tmpname = date("YmdHis") . mt_rand(10000,99999) . '.' . $extension;
//保存到服务器的路径
$fullpath = $tmppath . '/' . $tmpname;
$res = move_uploaded_file($_FILES['filedata']['tmp_name'], $fullpath);
if ($res) {
    echo 'move file ok';
}
```
使用`XMLHttpRequest`上传文件不会触发页面提交动作。也就没有办法在服务端通知前端js是否完成拷贝文件的操作。

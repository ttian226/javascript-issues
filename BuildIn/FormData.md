#### 使用FormData提交表单数据

```html
<form id="myform" name="myform" action="http://localhost/test.php">
    <input type="text" name="username" value="johndoe">
    <input type="number" name="id" value="123456">
    <input type="submit" onclick="return sendForm(this.form);">
</form>
```

```javascript
function sendForm(form) {
     var formdata = new FormData(form);

     // 给formdata附加额外数据
     formdata.append('secret_token', '1234567890');

     var xhr = new XMLHttpRequest();
     xhr.open('POST', form.action);
     xhr.onreadystatechange = function() {
         if (xhr.readyState === 4 && xhr.status === 200) {
             console.log('ok');
         }
     };
     xhr.send(formdata);

     return false; //阻止页面提交
 }
```

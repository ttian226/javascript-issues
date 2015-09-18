#### [History](https://developer.mozilla.org/en-US/docs/Web/API/History)

方法

##### history.pushState(state, title, url);

* state它可以理解为一个拿来存储自定义数据的元素。它和同时作为参数的url会关联在一起。
* title是一个字符串，目前各类浏览器都会忽略它（以后才有可能启用，用作页面标题），所以设置成什么都没关系。目前建议设置为空字符串。
* url是url地址

关于url，假设页面url地址是`http://localhost:63342/dom/history.html`

    1.如果url='/1',地址变为http://localhost:63342/1
    2.如果url='1',地址变为http://localhost:63342/dom/1
    3.如果url='?1',http://localhost:63342/dom/history.html?1
    4.如果url='#1',http://localhost:63342/dom/history.html#1

调用`pushState()`方法将新生成一条历史记录，方便用浏览器的“后退”和“前进”来导航

##### history.replaceState(state, title, url)

它和`history.pushState()`方法基本相同，区别只有一点，`history.replaceState()`不会新生成历史记录，而是将当前历史记录替换掉。

事件

##### window.onpopstate

只有点击浏览器的“前进”、“后退”这些导航按钮，或者是由JavaScript调用的`history.back()`等导航方法，且切换前后的两条历史记录都属于同一个网页文档，才会触发本事件。

`popstate`事件是设计出来和前面的2个方法搭配使用的。一般只有在通过前面2个方法设置了同一站点的多条历史记录，并在其之间导航（前进或后退）时，才会触发这个事件。同时，前面2个方法所设置的状态对象（第1个参数），也会在这个时候通过事件的event.state返还回来

例子：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <link rel="stylesheet" href="demo.css"/>
</head>
<body>
<title>HTML5 History API</title>
<style>
    #examples {
        padding-left: 20px;
    }
    #examples li {
        list-style: square;
        padding: 0;
        margin: 0;
    }
</style>
<article>
    <p id="status">HTML5 History API not supported</p>
    <p><em>Last event fired: <span id="lastevent">(none)</span></em></p>
    <p>To test the History API, click through the urls below. Note that none of these urls point to <em>real</em> pages. JavaScript will intercept these clicks, load data and the browser address bar will <em>appear</em> to change - but this is the History API in action!</p>
    <p>Use the back and forward buttons in your browser to navigate the history.</p>
    <ul id="examples">
        <li><a href="/history/first">first</a></li>
        <li><a href="/history/second">second</a></li>
        <li><a href="/history/third">third</a></li>
        <li><a href="/history/fourth">fourth</a></li>
        <li><a href="/history/other">other</a></li>
    </ul>
    <p><small>Note: since these urls aren't real, refreshing the page will land on an invalid url.</small></p>
    <div id="output"></div>
</article>
</body>
<script src="his.js"></script>
</html>
```

```javascript
/**
 * Created by wangxu on 9/17/15.
 */

var $ = function (id) {
        return document.getElementById(id);
    },
    state = $('status'),
    lastevent = $('lastevent'),
    examples = $('examples'),
    output = $('output'),
    template = '<p>URL: <strong>{url}</strong>, name: <strong>{name}</strong>, location: <strong>{location}</strong></p>',
    
    // 假设data是ajax传过来的数据
    data = {
        first : {
            name: "Remy",
            location: "Brighton, UK"
        },
        second: {
            name: "John",
            location: "San Francisco, USA"
        },
        third: {
            name: "Jeff",
            location: "Vancover, Canada"
        },
        fourth: {
            name: "Simon",
            location: "London, UK"
        },
        other: {
            name: "wangxu",
            location: "Shenyang, China"
        }
    };


// 判断history api是否可用
if (typeof history === 'undefined') {
    state.className = 'fail';
} else {
    state.className = 'success';
    state.innerHTML = 'HTML5 History API available';
}

// 点击事件
examples.addEventListener('click', function (e) {
    var title;
    e.preventDefault();
    if (e.target.nodeName.toLowerCase() === 'a') {
        title = e.target.innerHTML;
        data[title].url = e.target.getAttribute('href');
        var url = e.target.href;    //获取a标签链接
        if (title !== 'other') {
            history.pushState(data[title], title, url);
        } else {
            // 当点击other链接时，用新的data替换当前的data
            history.replaceState(data[title], title, url);
        }
        reportData(data[title]);
    }
}, false);

// 当有history.pushState数据时，并且点击浏览器的后退或前进按钮会触发popstate事件
window.addEventListener('popstate', function (e) {
    var data = e.state;
    reportEvent(e);
    reportData(data || { url: "unknown", name: "undefined", location: "undefined" });
}, false);

// 记录当前data数据
function reportData(data) {
    output.innerHTML = template.replace(/(\{(.*?)\})/g, function (a,b,c) {
        return data[c];
    });
}

// 记录事件类型
function reportEvent(e) {
    lastevent.innerHTML = e.type;
}
```

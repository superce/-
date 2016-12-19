---
title: 修改 server 配置
---


把 `get('/')` 改为 `get('*')`

访问 localhost:3000/hello2 会报错

```
TypeError: path must be absolute or specify root to res.sendFile
   at ServerResponse.sendFile (/Users/peter/Desktop/react-router-monkey-stuff/react-router-monkey-demo/node_modules/express/lib/response.js:404:11)
   at /Users/peter/Desktop/react-router-monkey-stuff/react-router-monkey-demo/server.js:9:7
...

```


最终改成下面这样就可以了：

```
const path = require('path');
var express = require('express');
var app = express();

app.use(express.static('public'));
// 用跟 本文件平级的一个 public 夹作为静态文件的存放位置
// 没有这一行，后面 sendFile 的 index.html 就找不到了。

app.get('*', function(req, res){
  res.sendFile('index.html', {root: 'public'});
});

app.listen(3000, function(err) {
  console.log('Listening at http://localhost:3000');
});
```

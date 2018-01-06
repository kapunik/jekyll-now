---
layout: post
title: Мое первое приложение на node.js + express + socket.io
---

Я создал файлик **app.js** со следующим содержанием:
```javascript
var fs = require('fs'),
    https = require('https'),
    express = require('express');

var port = 443;
var app = express();

var options = {
    key: fs.readFileSync('/var/www/cert/ca.key'),
    cert: fs.readFileSync('/var/www/cert/ca.crt'),
    requestCert: true
};

app.get('/', function (req, res) {
  res.send('Hello World!');
});

var server = https.createServer(options, app);
server.listen(port, function() {
	console.log("Express server listening on port " + port);
});

```

В консоли, для запуска приложения на портах 80/443, нужно запускать ноду через **sudo**. Я до этого не сразу допёр, и минут 10 не мог понять, почему же не работает? В консоли выкатывало вот эти ошибки:
```bash
events.js:141
      throw er; // Unhandled 'error' event
      ^

Error: listen EACCES 0.0.0.0:443
    at Object.exports._errnoException (util.js:870:11)
    at exports._exceptionWithHostPort (util.js:893:20)
    at Server._listen2 (net.js:1224:19)
    at listen (net.js:1273:10)
    at Server.listen (net.js:1369:5)
    at Object.<anonymous> (/var/www/domains/t2k.su/app.js:19:8)
    at Module._compile (module.js:410:26)
    at Object.Module._extensions..js (module.js:417:10)
    at Module.load (module.js:344:32)
    at Function.Module._load (module.js:301:12)
```



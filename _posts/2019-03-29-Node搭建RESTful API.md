---
layout: post
title: Node搭建RESTful API
subtitle: Node.js学习笔记系列
date: 2019-03-29
author: Jalever
header-img: img/home-bg-geek.jpg
catalog: true
tags:
  - Node.js
  - Server
---

服务器上的`server.js`文件源码

```javascript
const express = require("express");
const app = express();
const bodyParser = require("body-parser");
const port = process.env.PORT || 8081;
const router = express.Router();

app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

router.get("/", function(req, res) {
  res.send("Hello World!");
});

router.get("/user", function(req, res) {
  res.send("Got a get Request!");
});

app.use("/api", router);

app.listen(port, function() {
  console.log(`Example app listening on ${port}`);
});
```

## `Mockjs`模拟数据

`server.js`中:

```javascript
const express = require("express");
const app = express();
const http = require("http");

const port = process.env.PORT || 8081;

const bodyParser = require("body-parser");
const router = express.Router();
const data = require("./data.js");

app.use("/user", data);
http.createServer(app).listen(port);

console.log("Express are listening 47.106.132.253:" + port);
```

`data.js`中:

```javascript
const request = require("request");
const express = require("express");
const router = express.Router();
const Mock = require("mockjs");

router.get("/data", (req, res, next) => {
  let data = Mock.mock({
    resultCode: 200,
    resultJson: {
      "list|50": [
        {
          "id|1-20000": 1000,
          name: "@cname",
          age: "@date()",
          "locked|1-2": "false",
          address: "@province()",
          phone: /^(13|14|15)[0-9]\d{8}$/,
          loginTime: function() {
            return new Date().getTime();
          },
          time: "@now()"
        }
      ]
    },
    resultMessage: "Query Success!"
  });

  res.json(data);
});

module.exports = router;
```

## 浏览器验证 API

#### Chrome 插件
`postman`
#### Firefox 插件
`RESTClient`

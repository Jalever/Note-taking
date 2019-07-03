---
layout: post
title: File System Module
subtitle: Nodejs Built-in Module
date: 2019-07-03
author: Jalever
header-img: img/post_light_bulb_bg.png
catalog: true
tags:
  - Node.js
---

- [Introduction](#introduction)
    - [Definition](#definition)
    - [Syntax](#syntax)
    - [File System Methods](#file-system-methods)
- [Common Usage for the File System Module](#common-usage-for-the-file-system-module)
    - [Create Files](#Create Files)
        - [fs.appendFile](#fsappendfile)
        - [fs.open](#fsopen)
        - [fs.writeFile](#fswritefile)
    - [Read Files](#read-files)
    - [Update Files](#update-files)
        - [fs.appendFile](#fsappendfile)
        - [fs.writeFile](#fswritefile)
    - [Delete Files](#delete-files)
    - [Rename Files](#rename-files)



## Introduction
#### Definition
The Node.js file system module allows you to work with the file system on your computer.

#### Syntax
To include the File System module, use the `require()` method:
```js
var fs = require('fs');
```

#### File System Methods
![ZtjGWV.png](https://s2.ax1x.com/2019/07/03/ZtjGWV.png)
![ZtjNyF.png](https://s2.ax1x.com/2019/07/03/ZtjNyF.png)
![ZtjUL4.png](https://s2.ax1x.com/2019/07/03/ZtjUL4.png)
![ZtjdeJ.png](https://s2.ax1x.com/2019/07/03/ZtjdeJ.png)
![Ztjww9.png](https://s2.ax1x.com/2019/07/03/Ztjww9.png)
![ZtjDF1.png](https://s2.ax1x.com/2019/07/03/ZtjDF1.png)

## Common Usage for the File System Module

#### Create Files
The File System module has methods for creating new files:
- fs.appendFile()
- fs.open()
- fs.writeFile()

###### fs.appendFile
The `fs.appendFile()` method appends specified content to a file. If the file does not exist, the file will be created:

```js
const fs = require("fs");
var express = require("express");
var app = express();
const server = require("http").createServer(app);
const port = process.env.PORT || 3000;

server.listen(port, () => {
	console.log("The server is listening on http://47.106.132.253:%d", port);
});

app.get("/index", (req, res) => {
	fs.appendFile("./src/hello.txt", "Hello Jalever,it's first time to create file by node", err => {
		if(err) {
			throw err;
		}

		console.log("create hello.txt successfully!!!");
	});
});
```

###### fs.open
The `fs.open()` method takes a "flag" as the second argument, if the flag is "w" for "writing", the specified file is opened for writing. If the file does not exist, an empty file is created:
```js
const fs = require("fs");
var express = require("express");
var app = express();
const server = require("http").createServer(app);
const port = process.env.PORT || 3000;

server.listen(port, () => {
	console.log("The server is listening on http://47.106.132.253:%d", port);
});

app.get("/index", (req, res) => {
	fs.open("./src/youtube.txt", "w", (err, file) => {
		if(err) {
			throw err;
		}

		console.log("create youtube.txt successfully!!!");
	});

	fs.readFile("./src/index.html", (err, data) => {
		res.writeHead(200, {
			"Content-Type": "text/html"
		});
		res.write(data);
		res.end();
	});
});
```

###### fs.writeFile
The `fs.writeFile()` method replaces the specified file and content if it exists. If the file does not exist, a new file, containing the specified content, will be created:
```js
const fs = require("fs");
var express = require("express");
var app = express();
const server = require("http").createServer(app);
const port = process.env.PORT || 3000;

server.listen(port, () => {
	console.log("The server is listening on http://47.106.132.253:%d", port);
});

app.get("/index", (req, res) => {
	fs.writeFile("./src/google.txt", "Hello Google!", err => {
		if(err) {
			throw err;
		}

		console.log("create Google.txt successfully!!!");
	});

	fs.readFile("./src/index.html", (err, data) => {
		res.writeHead(200, {
			"Content-Type": "text/html"
		});
		res.write(data);
		res.end();
	});
});
```

#### Read Files
The `fs.readFile()` method is used to read files on your computer.

```js
const fs = require("fs");
var express = require("express");
var app = express();
const server = require("http").createServer(app);
const port = process.env.PORT || 3000;

server.listen(port, () => {
	console.log("The server is listening on http://47.106.132.253:%d", port);
});

app.get("/index", (req, res) => {
	fs.readFile("./src/index.html", (err, data) => {
		res.writeHead(200, {
			"Content-Type": "text/html"
		});
		res.write(data);
		res.end();
	});
});
```

#### Update Files
The File System module has methods for updating files:
###### fs.appendFile()
The `fs.appendFile()` method appends the specified content at the end of the specified file:
```js
const fs = require("fs");
var express = require("express");
var app = express();
const server = require("http").createServer(app);
const port = process.env.PORT || 3000;

server.listen(port, () => {
	console.log("The server is listening on http://47.106.132.253:%d", port);
});

app.get("/index", (req, res) => {
	fs.appendFile("./src/google.txt", "This is AppendFile Method", err => {
		if(err) {
			throw err;
		}

		console.log("Update Google.txt successfully!!!");
	});

	fs.readFile("./src/index.html", (err, data) => {
		res.writeHead(200, {
			"Content-Type": "text/html"
		});
		res.write(data);
		res.end();
	});
});
```

###### fs.writeFile()
The `fs.writeFile()` method replaces the specified file and content:
```js
const fs = require("fs");
var express = require("express");
var app = express();
const server = require("http").createServer(app);
const port = process.env.PORT || 3000;

server.listen(port, () => {
	console.log("The server is listening on http://47.106.132.253:%d", port);
});

app.get("/index", (req, res) => {
	fs.writeFile("./src/google.txt", "Hello Google222!", err => {
		if(err) {
			throw err;
		}

		console.log("create Google.txt successfully!!!");
	});

	fs.readFile("./src/index.html", (err, data) => {
		res.writeHead(200, {
			"Content-Type": "text/html"
		});
		res.write(data);
		res.end();
	});
});
```

#### Delete Files
To delete a file with the File System module,  use the `fs.unlink()` method.

The `fs.unlink()` method deletes the specified file:

```js
const fs = require("fs");
var express = require("express");
var app = express();
const server = require("http").createServer(app);
const port = process.env.PORT || 3000;

server.listen(port, () => {
	console.log("The server is listening on http://47.106.132.253:%d", port);
});

app.get("/index", (req, res) => {
	fs.unlink("./src/google.txt", err => {
		if(err) {
			throw err;
		}

		console.log("Delete Google.txt successfully!!!");
	});

	fs.readFile("./src/index.html", (err, data) => {
		res.writeHead(200, {
			"Content-Type": "text/html"
		});
		res.write(data);
		res.end();
	});
});
```

#### Rename Files
To rename a file with the File System module,  use the `fs.rename()` method.

The `fs.rename()` method renames the specified file:

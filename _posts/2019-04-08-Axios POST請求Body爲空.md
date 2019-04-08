---
layout: post
title: Axios POST請求Body爲空
subtitle: 項目BUGS筆記
date: 2019-04-08
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Axios
  - Bugs
---



```javascript
let data = JSON.stringify({
    modelKey: "M1554686110975"
});

return axios.post("http://bos3d-demo.rickricks.com/api/o16f3b64e7b6425faaac86de57f73703/scenes", data, {
        headers: {
            "Content-Type": "application/json"
        }
});
```
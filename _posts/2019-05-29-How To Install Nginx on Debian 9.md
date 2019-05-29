---
layout: post
title: How To Install Nginx on Debian 9
subtitle: Web Development学习笔记系列
date: 2019-05-29
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Nginx
---

## Step 1 – Installing Nginx
```
apt update
apt install nginx
```


## Step 2 – Adjusting the Firewall
```
apt install ufw
ufw enable
ufw app list
```
You should get a listing of the application profiles:
```
Output
Available applications:
...
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
...
```

As you can see, there are three profiles available for Nginx:

- Nginx Full: This profile opens both port 80 (normal, unencrypted web traffic) and port 443 (TLS/SSL encrypted traffic)
- Nginx HTTP: This profile opens only port 80 (normal, unencrypted web traffic)
- Nginx HTTPS: This profile opens only port 443 (TLS/SSL encrypted traffic)

```

You should get a listing of the application profiles:

```
ufw allow 'Nginx HTTP'
ufw status
```

You should see HTTP traffic allowed in the displayed output:

```
Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere                  
Nginx HTTP                 ALLOW       Anywhere                  
OpenSSH (v6)               ALLOW       Anywhere (v6)             
Nginx HTTP (v6)            ALLOW       Anywhere (v6)
```

## Step 3 – Checking your Web Server

```
systemctl status nginx
```

If you do not know your server's IP address, try typing this at your server's command prompt:
```
ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
```

When you have your server's IP address, enter it into your browser's address bar:

```
http://your_server_ip
```

## Step 4 – Managing the Nginx Process
To stop your web server, type:
```
systemctl stop nginx
```

To start the web server when it is stopped, type:
```
systemctl start nginx
```

To stop and then start the service again, type:
```
systemctl restart nginx
```

If you are simply making configuration changes, Nginx can often reload without dropping connections. To do this, type:
```
systemctl reload nginx
```

By default, Nginx is configured to start automatically when the server boots. If this is not what you want, you can disable this behavior by typing:
```
systemctl disable nginx
```

To re-enable the service to start up at boot, you can type:
```
systemctl enable nginx
```

## Step 5 – Setting Up Server Blocks
In order for Nginx to serve this content, it's necessary to create a server block with the correct directives.
```
/etc/nginx/sites-available/xxx.html
```

Nginx on Debian 9 has one server block enabled by default that is configured to serve documents out of a directory at `/var/www/html`.

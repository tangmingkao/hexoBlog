---
title: Cookie简介
data: 2016-07-18 15:47:30
---

### Cookie简介

HTTP Cookie（也叫Web Cookie或浏览器Cookie）是服务器发送到用户浏览器并保存在本地的一小块数据，它会在浏览器下次向同一服务器再发起请求时被携带并发送到服务器上。通常，它用于告知服务端两个请求是否来自同一浏览器，如保持用户的登录状态。Cookie使基于无状态的HTTP协议记录稳定的状态信息成为了可能。

Cookie主要用于以下三个方面:

* 回话状态管理(例如用户登录状态 , 购物车等)
* 个性化设置(如用户自定义设置,主题等)
* 浏览器行为跟踪 (如跟踪分析用户行为等)

### 创建Cookie

当服务器收到HTTP请求时，服务器可以在响应头里面添加一个Set-Cookie选项。浏览器收到响应后通常会保存下Cookie，之后对该服务器每一次请求中都通过Cookie请求头部将Cookie信息发送给服务器。另外，Cookie的过期时间、域、路径、有效期、适用站点都可以根据需要来指定。

> **Set-Cookie: <cookie名>=<cookie值>**

```javascript
HTTP/1.0 200 OK
Content-type: text/html
Set-Cookie: yummy_cookie=choco
Set-Cookie: tasty_cookie=strawberry
[页面内容]
```
现在，对该服务器发起的每一次新请求，浏览器都会将之前保存的Cookie信息通过Cookie请求头部再发送给服务器。

```javascript
GET /sample_page.html HTTP/1.1
Host: www.example.org
Cookie: yummy_cookie=choco; tasty_cookie=strawberry
```

### 客户端获取Cookie

客户端可以通过如下代码获取Cookie值.
> ** document.cookie **


代码实现获取各个cookie值

```javascript
var Cookie = {};
var cookie = document.cookie;
var tempArr = cookie.split(';');
var len = tempArr.length;

for(var i = 0; i < len; i++){
	var tempCookie = tempArr[i];
	var p = tempCookie.indexOf('=');
	var key = tempCookie.substring(0,p);
	var value = tempCookie.substring(p+1);
	value = decodeURIComponent(value);
	Cookie[key] = value;
}
```

> Cookie 必须在 HTML 文件的内容输出之前设置；不同的浏览器 (Netscape Navigator、Internet Explorer) 对 Cookie 的处理不一致，使用时一定要考虑；客户端用户如果设置禁止 Cookie，则 Cookie 不能建立。 并且在客户端，一个浏览器能创建的 Cookie 数量最多为 300 个，并且每个不能超过 4KB，每个 Web 站点能设置的 Cookie 总数不能超过 20 个

##### 设置Cookie

```javascript
var setCookie = function(key,value,expires){
    var iDay = new Date();
    var maxTime = iDay.setDate(iDay.getDate() + expires);
    document.cookie = key + "=" + value + "; " + "expires=" + maxTime;
};

```


##### 删除Cookie值

```javascript

var deleteCookie = function(key){   
    setCookie(key,"",-1);
}

```

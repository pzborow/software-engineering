# Better http requests

[httpie](https://httpie.io/docs)

```http
$ http google.pl
HTTP/1.1 301 Moved Permanently
Cache-Control: public, max-age=2592000
Content-Length: 218
Content-Type: text/html; charset=UTF-8
Date: Fri, 05 Nov 2021 08:58:57 GMT
Expires: Sun, 05 Dec 2021 08:58:57 GMT
Location: http://www.google.pl/
Server: gws
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 0

<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.pl/">here</A>.
</BODY></HTML>
```

* Formatted and colorized terminal output
* Built-in JSON support
* Forms and file uploads
* HTTPS, proxies, and authentication
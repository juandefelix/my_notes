PERFORMANCE OF A WEBSITE
========================

### HTTP Protocol and TCP
The interaction of the HTTP and the TCP protocol causes performance problems. The three-way handshake to acknowledge the connection, the Round Trip Time, and the possibility of fetching only one object per request, among othe things, make this type of connection slow. Keep in mind that a new transacion will need to open a new connection. It is possible, although, to make multiple downloads in a single TCP connection. More info:  

- [http://www.w3.org/Protocols/HTTP-NG/http-prob.html](http://www.w3.org/Protocols/HTTP-NG/http-prob.html)
- [http://www.w3.org/Protocols/HTTP/Performance/](http://www.w3.org/Protocols/HTTP/Performance/)

More items to review:

- [https://developer.yahoo.com/blogs/ydn/high-performance-sites-rule-1-fewer-http-requests-7163.html](https://developer.yahoo.com/blogs/ydn/high-performance-sites-rule-1-fewer-http-requests-7163.html)
- [http://stackoverflow.com/questions/9855545/http-requests-vs-file-size](http://stackoverflow.com/questions/9855545/http-requests-vs-file-size)
- [Chrome Network Performance](https://developer.chrome.com/devtools/docs/network)
- [New Chrome Guide for debuggin tools](https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading)
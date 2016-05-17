PERFORMANCE OF A WEBSITE
========================

### HTTP Protocol and TCP
The interaction of the HTTP and the TCP protocol causes performance problems. The three-way handshake to acknowledge the connection, the Round Trip Time, and the possibility of fetching only one object per request, among othe things, make this type of connection slow. Keep in mind that a new transacion will need to open a new connection. It is possible, although, to make multiple downloads in a single TCP connection. More info:  

- [http://www.w3.org/Protocols/HTTP-NG/http-prob.html](http://www.w3.org/Protocols/HTTP-NG/http-prob.html)
- [http://www.w3.org/Protocols/HTTP/Performance/](http://www.w3.org/Protocols/HTTP/Performance/)

**TODO** The advantage of having a large file instad of two smaller files.  
The browsers are capable of sending between 2 and 8 parallel requests. Read about that on this
[post on StackOverflow](http://stackoverflow.com/questions/9855545/http-requests-vs-file-size)

More items to review:

- [https://developer.yahoo.com/blogs/ydn/high-performance-sites-rule-1-fewer-http-requests-7163.html](https://developer.yahoo.com/blogs/ydn/high-performance-sites-rule-1-fewer-http-requests-7163.html)
- [Chrome Network Performance](https://developer.chrome.com/devtools/docs/network)
- [New Chrome Guide for debuggin tools](https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading)

### Optimizing Web Images
Image files are used in websites as icons, buttons, backgrounds and pictures. Balancing file size and image quality will improve the load time, costs and data space, and user experience in general. Here are some thumb rules for sizes and file types:  
#### Image Sizes
 background | banners | high end photographs
 :---: | :---: | :---: | 
< 10kb | < 60kb | < 100kb

#### File Types
**GIF**: Great file type for saving graphics, charts, bullet points, icons, buttons, and textual details. Includes transparency   
**PNG**: Similar as GIF but files have more weight. Good for use in buttons, icons, etc, keeping them at low pixel size (16 x 16, 50 x 50). At sizes around 200px, files tend to weigh too much.  
**JPG**: User this format for higher quality images, keeping in mind that the appropriate compression should be used.  
[More Info](http://www.techrepublic.com/blog/web-designer/tips-for-optimizing-your-web-images/)

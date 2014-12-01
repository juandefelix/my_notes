.htaccess redirecting (Case 28317)
=====================

To write a redirect on the webserver, we have to access the **.htaccess** file corresponding to that website. In this case the path to that file is:  
`\\moneymark\websites\AIDSFoundationOfChicago\www.afc.dev09.thirdwavellc.com\webroot\.htaccess`  
where `moneymark` si the name of a server. You can connect to the server with __*command + K*__ in your Mac. Once you have connected and reached the file, open it with your editor.

You can use these resources to write the proper syntax for redirecting:  
[mod\_rewrite introduciton](http://httpd.apache.org/docs/2.2/rewrite/intro.html)  
[Apache mod_rewrite](http://httpd.apache.org/docs/2.2/mod/mod_rewrite.html#rewritebase)  
[Rewrite Rule Flags](http://httpd.apache.org/docs/2.4/rewrite/flags.html)  
[Regex in Perl](http://perldoc.perl.org/perlreref.html)  
[More regex in Perl](http://pcre.org/pcre.txt)  
[Lots of examples](https://gist.github.com/ScottPhillips/1721489)  
[Editing Query String](https://wiki.apache.org/httpd/RewriteQueryString)
An file example:  
```
RewriteEngine On
RewriteBase /
 

# Ignore all files that have an extension of three letters.
RewriteRule ^(.*\.[a-zA-Z]{2,4})$ $1 [L,QSA]
RewriteRule ^(/)$ $1 [L,QSA]

# Ignore all admin tool and development pages.
RewriteRule ^(common/admin.*)$ $1 [L,QSA]
RewriteRule ^(development/.*)$ $1 [L,QSA]
RewriteRule ^(flashservices/.*)$ $1 [L,QSA]

RewriteRule ^/([^/]*)(?:/[^/]*)*/(\d+)-.*$ /page/$1?id=$2

#DYNAMIC_CONTENT
RewriteRule ^shorturl/?$ page/news/all-news/afc-thanks-rep-mike-quigley-for-introducing-bill-to-modernize-federal-aids-housing-program [R=302,L,QSA,NC]
#END_DYNAMIC_CONTENT

#Redirecting to the new website format
RewriteRule /(\d+)[^\/]*$ /page/news?id=$1 [R=301]

# Pass along the REQUEST_URI as the page
RewriteRule ^(.*)/?$ content.cfm?page=%{REQUEST_URI} [NS,L,QSA]
```

## Using query strings  
You can write a condition against a query string with  
`RewriteCond %{QUERY_STRING} value`  
where value is can be a regular expression. The query string won't include the character `?`. Any capture in this statement can be used as %number in the replacement string. **If you write a `?` in the end of the replacement string, the query string won't be appended to it.**

# TNT PageSpeed Process


## Server Side
Make sure you add these to the server settings under the correct domain name.

''''
gzip         on;
gzip_disable "MSIE [1-6]\\.(?!.*SV1)";
gzip_proxied any;
gzip_types   text/plain text/css application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript image/x-icon image/bmp image/svg+xml;
gzip_vary    on;
'''

### Also

'''
location ~* .(js|jpg|jpeg|gif|png|css|tgz|gz|rar|bz2|doc|pdf|ppt|tar|wav|bmp|rtf|swf|ico|flv|txt|woff|woff2|svg)$ {
etag on;
if_modified_since exact;
add_header Pragma "public";
add_header Cache-Control "max-age=31536000, public";
}
'''

## Resources
[ Source 1 ](https://support.plesk.com/hc/en-us/articles/213380049-How-to-enable-gzip-compression-for-nginx-on-Plesk-server)
[ Source 2 ](https://support.plesk.com/hc/en-us/articles/115001374153-How-to-enable-leverage-browser-caching-for-nginx-)
[ Optimize images with Kraken or similar ](https://kraken.io/web-interface)

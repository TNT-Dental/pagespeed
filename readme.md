# TNT PageSpeed Process

## Server Side
Make sure you add these to the server settings under the correct domain name.

```
gzip         on;
gzip_disable "MSIE [1-6]\\.(?!.*SV1)";
gzip_proxied any;
gzip_types   text/plain text/css application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript image/x-icon image/bmp image/svg+xml;
gzip_vary    on;
```
[Source](https://support.plesk.com/hc/en-us/articles/213380049-How-to-enable-gzip-compression-for-nginx-on-Plesk-server)

### Also Add

```
location ~* .(js|jpg|jpeg|gif|png|css|tgz|gz|rar|bz2|doc|pdf|ppt|tar|wav|bmp|rtf|swf|ico|flv|txt|woff|woff2|svg)$ {
etag on;
if_modified_since exact;
add_header Pragma "public";
add_header Cache-Control "max-age=31536000, public";
}
```
[Source](https://support.plesk.com/hc/en-us/articles/115001374153-How-to-enable-leverage-browser-caching-for-nginx-)

## Homepage Optimization and Template Cleanup
View the current live desktop site and look for:
- Banner/Welcome videos
- Youtube embeds in the homepage ie. ( testimonials sections )
- Embeded google maps ( multi-locations ) 
- Any third party widget ie.( chat, make appointments, instagram feeds )

### Video Site?
If there are videos in the homepage:
- Set the site to staging mode
- Check for scripts calls in the template
- Does it have a fundation.js or tnt-videos.js?
- Make backups of all old script files
- Combine and comment out any extra files

#### Homepage videos
Type | Desc 
-----|-----
Banner Videos|Is it Vimeo Only, ask for youtube account/video upload
Youtube embeds|Add lazyload with class .youtube and make sure the thumbnail is beign pulled from youtube
Testimonials videos|Add lazyload or data-player and data-embed

[TNT Video scripts](https://github.com/TNT-Dental/tntvideos)

## Optional

- Display "none" google embeded maps for mobile ie. ( look for #map, #g-map, #fo-map )
- Hide high resolution stock images
- Check performance of google fonts (https://fonts.google.com/)

## Advanced

- Compress JQuery scripts
- Combine scripts files (backup old files)

## Useful Links
- [Optimize images with Kraken or similar](https://kraken.io/web-interface)
- [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)

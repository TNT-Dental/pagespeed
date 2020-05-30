# TNT PageSpeed Process

## 1. Server Side
Make sure to add these to the `Apache & nginx Settings` for the correct domain name under `Additional nginx directives`.

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

## 2. Homepage Optimization and Template Cleanup
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
- Replace any video thumbnail coming from youtube with screenshots resized and uploaded to the cms.

#### Homepage videos
Type | Desc 
-----|-----
Banner Videos|Is it Vimeo Only, ask for youtube account/video upload
Youtube embeds|Add lazyload with class .youtube and make sure the thumbnail is beign pulled from youtube
Testimonials videos|Add lazyload or data-player and data-embe

[TNT Video scripts](https://github.com/TNT-Dental/tntvideos)

## 3. Hiding Elements(optional)

- Display "none" google embeded maps for mobile ie. ( look for #map, #g-map, #fo-map )
- Hide high resolution stock images
- Check performance of google fonts (https://fonts.google.com/)

## 4. Advanced

- Compress JQuery scripts
- Combine scripts files (backup old files)
- Generate iframes or scripts with javascript:
```html
<!-- Dynamic Content -->
<script>
	function addMap() {
	    // Adds an element to the document
	    var p = document.getElementById("map");
	    var newElement = document.createElement("iframe");
	    newElement.setAttribute('src', 'https://www.google.com/maps/...');
	    newElement.setAttribute('width', '100%');
	    newElement.setAttribute('height', '480');
	    p.appendChild(newElement);
	}
	if( window.screen.width >= 600  ) {	addMap(); }
</script>	
```
- Add lazy loading to images by adding class "lazyload" loading=“lazy” and chang src to data-src…  and link to lazyload script at the bottom of the html
```html
<img class="lazyload" loading="lazy" data-src="assets/images/banner.jpg">
<script src="assets/js/lazysizes.min.js" async=""></script>
``` 

- Create smaller sized copies of large photos at 600px wide and wrap the original img in the picture element so it only downloads the image according to the screen size. Can also add lazy loading to the image.
```html
<picture>
     <source srcset="assets/images/banner-1-sm.jpg" media="(max-width: 600px)"> 
     <img src="assets/images/banner-1.jpg”  alt="" >
</picture>
```

## 5. Useful Links
- [Optimize images with Kraken OR ](https://kraken.io/web-interface)
- [Optimize images TinyPing](https://tinypng.com/)

- [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)

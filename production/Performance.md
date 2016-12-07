## Performance
This section lists performance optimisations and "gotchas" that we recommend to implement in most cases.

### Initial loading

* Don’t use client-side rendering for the initial view
* Announce DNS as soon as possible with `dns-prefetch`
* Announce resources using [Resource Hints](https://www.w3.org/TR/resource-hints/)
* Announce CSS first thing
* Don’t use blocking JavaScript, try to put scripts just before the closing `</body>`
* Minify and concatenate JavaScript and CSS if using HTTP1.1
* Analyze usage of defer or async in every `<script>` element
* Do not manipulate the page on `DOMContentLoaded` event
* Use HTTP/2 server push when possible


### Images

* Don’t use blocking images (Base64) as a general rule
* Apply responsive images with srcset and `<picture>`
* Use CSS/SVG Sprites on HTTP/1.1
* Compress your images
* Use progressive JPEG when possible
* Use SVG when possible
* [Replace animated GIFs with muted videos](http://rigor.com/blog/2015/12/optimizing-animated-gifs-with-html5-video) when possible


### Web fonts

* Use web fonts with a [font loader](https://github.com/typekit/webfontloader)
* Use web fonts with a CDN
* Optimise web fonts, removing glyphs and unused characters


### Responsiveness

* Verify that you don’t have scripts running for longer than 50 ms
* Use a mobile viewport or touch-action CSS to [remove touch delay](https://developers.google.com/web/updates/2013/12/300ms-tap-delay-gone-away)
* Use passive listeners, debouncing, or throttling on scroll and resize events
* Use web workers for long tasks
* Use `will-change` on elements that will be animated to avoid repaint
* Use [CSS containment](https://developers.google.com/web/updates/2016/06/css-containment) to reduce browsers’ useless recalculations
* Use the browser’s developer tools to turn on an FPS meter and check that you are reaching your goal of 60 fps, mostly while scrolling or animating


### Network

General technologies you should start implementing:

* TLS (HTTPS)
* HTTP/2

***Check that you have ticked off everything on the list below***

* gzip enabled on all text files
* DNS queries kept to a minimum
* Keep-alive enabled
* Minimium/No redirects

***Some nice to haves***

* If serving on TLS, use HSTS
* Small cookie size
* Static content with far-future expiration
* CDN for static content
* Domain sharding for HTTP/1.1
* If domain sharding enabled, disable it for HTTP/2 or use a multidomain certificate

__Resource fetching__ → performance enhancing technique. We can use it to tell the browser which assets the user will might need in the future.

__Prebrowsing__ → practice of guessing what users need before they need it. It's broken down into a number of different techniques.

### DNS prefetching
```html
<link rel="dns-prefetch" href="//example.com">
```
Tells the browser to resolve the DNS lookup as quickly as possible, meaning the DNS lookup process will already be underway by the time the browser hits the script. Particularly useful if we're using code from third parties, *e.g.* social network widget.

### Preconnect
```html
<link rel="preconnect" href="https://example.com/">
```
The browser will resolve the DNS but also make the TCP handshare and optional TLS negotiation. This sets up the necessary sockets ahead of time.

### Prefetcing
```html
<link rel="prefetch" href="image.png">
```
Asks the browser to request an item, and store it in the cache for reference later. Only to be used on resources we are certain will be needed. It could have huge performance benefits for webfonts - at the moment font files have to wait for the DOM and CSSOM to be constructed before they download.

It can be ignored by the browser, *e.g.* large file on a slow network.

### Prerendering pages
```html
<link rel="prerender" href="https://example.com/">
```
It preemptively loads all the assets of a certain document - all the resources are downloaded, the DOM is created, the page laid out, the CSS applied, the JavaScript executed, etc. When the user navigates to it, it appears to load instantly.

It should only be used on pages we're certain the user is going to click on. Otherwise, the client will download all of the assets necessary to render the page for no reason at all.

The Page Visibility API can be used to prevent scripts firing before they're rendered on the user's screen.

### Preloading (future)
```html
<link rel="preload" href="image.png">
```
Tells the browser it **must** download an asset, regardless of whether it thinks is a good idea or not.

> __Note:__ preloading is not currently supported by any browser at the moment.


# Source
[Prefetching, preloading, prebrowsing – CSS Tricks](https://css-tricks.com/prefetching-preloading-prebrowsing/)
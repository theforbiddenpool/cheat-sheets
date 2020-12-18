There are three ways to increase the speed of our website:
1. improve what happens on the client side – the time to render the page on the screen.
2. transfer of our files – network latency, the time to travel from our client to the server and back.
3. processing done on the backend – the time to load data and assemble the website before it is sent.

> “An average website makes more than 100 requests to load completely.”

We need to know where what's slowing down the website and have the tools to measure if our changes have solved the problem.

# Transfer
The more kilobytes a user needs to download the longer it takes to load the website. Therefore, we need to reduce the amount of data being transfered:
- minify the HTML, CSS, and JavaScript files;
- optimize images and use smaller images when the website is used on a smaller screen.

## Images
The primary way to change an image size is to change the file format and pick the format that is the best for the job. The four main image file formats are:
- __JPEG__ → images with many colors, *e.g.* photographs. Don't allow transparency, and tend to be big in file size.
- __GIF__ → usually limits the number we can use in a gif (2 - 256). Good for small animations.
- __PNG__ → limit the number of colors we can use. Tend to be smaller than JPEGs. Used a lot for logos.
- __SVG__ → vector graphics. Small in file size. Good for retina display or 4k displays. Tend to be simplistic.

Newer file formats have been created with superior compression, meaning images will be loaded faster and consume less data. *e.g.* JPEG 2000. However, browser support isn't there yet.

#### Compression
We can also use tools to compress images – especially JPEG and PNG. An example is [TinyPNG](https://tinypng.com/) for PNGs, and [JPEG-optimizer](http://www.jpeg-optimizer.com/) for JPG. We can also save JPG files with less quality (30 - 60%).

#### Resize image based on display size
If we're displaying an image at only 500px wide, we don't need to keep the image a heigher width. Resize or chop the image to the actual size it will be displayed. The larger the resolution the larger the file size.

Same can be applied to background images. We can use media queries to change the background image according to the device's size.

#### Use Content Delivery Networks (CDNs)
They take care of optimization and delivery for us, including caching. An example of such service is [imgIX](https://www.imgix.com/). They'll give us an URL we can use in our website.

#### Remove metatags
When a photo is taken, extra data, such as the device used, date, and location is also saved. This data is extra information we don't need, and increases the photo's size. We can use [online tools](https://www.verexif.com/en/) or programs to remove it.

## Reducing Download Frequency
There is a maximum amount of files the HTTP protocol allows to concurrently download from the same domain (depends on the browser). By reducing the amount of components a page requires, we reduce the number of HTTP requests we have to make. HTTP also has a limit to a file's total size.

When using big libraries and frameworks, like Bootstrap or Foundation, we need to ask ourselves if they are really needed. Can we use flexbox or CSS grid instead? Do we really need jQuery? If we must use a library, maybe we can find lightweight ones.

We can minimize our files and combine them into one.

# Frontend
## Critical Render Path
1. Request a website, the server returns an HTML file.
2. The browser starts reading the HTML file.
3. While it's parsing the HTML, it incrementally generates the tree model of HTML tags, known as the Document Object Model (DOM). The DOM describes the content of the page.
4. When it encounters a styl e link, the browser asks the CSS file from the server. It continues to work on the DOM.
5. After the CSS file arrives, the browser also starts generating a tree model called CSS Object Model (CSSOM). The tree describes how the content is styled.
6. When it encounters a JavaScript file in a script tag, it grabs it from the server. The browser reads it and executes anything it might change on the DOM.
7. Once all of that is done, it combines both DOM and CSSOM into a render tree. The browser will then use this render tree to figure out the layout.
8. When it's done figuring out, it will paint all the pixels. Finally, we will have our website.

The Critical Render Path shows what it takes to pain the website on the screen. Usually, CSS and JavaScript files take high priority, while other files like images take lower priority.

### DOM
We want to load CSS files as soon as possible, and JavaScript files as late as possible. `script` tags may block HTML and CSS from rendering. There are some exceptions, but generally we want CSS files in the `head`, and JavaScript at the bottom of the page.

### CSSOM
CSS is **render-blocking** - in order to construct the rendered tree we need to wait for the CSSOM to complete. So it makes sense to make it as lightweight as possible.
- __Only load whatever is needed__. Make sure you don't have any unused files and/or styles being loaded.
- __Above the fold loading__. We can move non-critical styles or things we'll only see later in the page to a separate file, and load that file after. We can do this with a bit of JavaScript.
- __Media attributes__. It's possible to use media attributes on the HTML file itself. On the `link` tag, we can add a `media` tag with the query we want. The CSS file will only be loaded if it matches. Useful to load files for specific screen sizes.
- __Less Specificity__. The more information we send, the more bytes that is. However, this isn't as important as the others.

### JavaScript
JavaScript can modify both the DOM and CSSOM. It's **parser-blocking** - only when both the DOM and CSSOM + the modifications by JavaScript are finished, the page can go through the Render Tree, Layout, and finally Paint.
- __Load scripts asynchronously__. When HTML is parsing and encounters a script tag, it will stop reading to download the JavaScript file and execute it. We can use HTML attributes to change this behavior.
[![script vs script async vs script defer](../_assets/perf_js-async.png)](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/loading-third-party-javascript "Loading Third-Party JavaScript – Web Fundamentals")
  - no tag → critical, app scripts.
  - `async` → scripts that don't affect the DOM or CSSOM, for example, external scripts that require no knowledge of our code. *e.g.* Google Analytics scripts
  - `defer` → third-party scripts that act on the DOM tree, but not important to load *above the fold* content.
- __Minimize DOM manipulation__ → the browser will have to do extra work if we're manipulating the DOM/CSSOM via JavaScript.
- __Avoid long running JavaScript__ → if we have JavaScript code that's executing for a long time, we'll have a poor user experience. *e.g.* `alert()`

#### Redraw
During runtime, JavaScript makes changes on the DOM/CSSOM, causing the browser to go through the Render Tree, Layout, and Paint phases again. Current browsers are smart enough to only do a partial update, however we can't be reliant on it to be efficient or performant. It's our job to make sure it's efficient.

# Sources
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie

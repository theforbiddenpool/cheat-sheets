__Web App__ → website that allows users to interact with the web page in many ways. It's inside a browser window. The server is the one who provides the necessary files.

__Native App__ → app on a mobile device - it's mean to work on a native platform. They have all the files required in the deviced itself. Additionally, they can also send push notifications, work offline, and have access to the phone hardware (*e.g.* camera, or geo location).

__Progressive Web App (PWA)__ → new technology aiming for web apps to behave similarly to native apps. Additionally, they work faster on mobile devices, since they are designed with mobile in mind.

When using React via Create React App, a lot of the setup is already done for us. We only need to make a few modifications to have a PWA up and running.

## Creating a PWA
There is a checklist, constantly being updated, that we can use to helps us create a PWA. We can find it on [web.dev](https://web.dev/pwa-checklist/). However, following the good practices, we can focus only on main three points. Additionally, there are certain features which implementation hasn't been that smooth or are still in the works.

### HTTPS
__HTTPS__ → prevents bad actors from tampering with communications between our app and browser to the server, by encrypting it.

__Certificate authority__ → authority that give us a certificate certifying that we are indeed whatever domain name we say we are.

Certain PWA features require HTTPS for security reasons. If we are not hosting our app in something like GitHub pages, we can use [Let's Encrypt](https://letsencrypt.org/). Let's Encrypt give free certificates, and it's easy to setup. We can also use [Cloudfare](https://www.cloudflare.com/), a Content Delivery Network (CDN). However, it's much harder to setup.

### App Manifest
The App Manifest allows us mimic certain things, *e.g.* splash screen, app icon, etc., a native app has. It's a simple JSON file that gives the ability to control how the app should appear to the user.

```json
{
  "short_name": "React App",
  "name": "Create React App Sample",
  "icons": [
    {
      "src": "favicon.ico",
      "sizes": "64x64 32x32 24x24 16x24",
      "type": "image/x-icon"
    }
  ],
  "start_url": "./index.html",
  "display": "standalone",
  "theme_color": "#000000",
  "background_color": "#ffffff"
}
```

To generate favicons in the different sizes required for each platform, we can use [Real Favicon Generator](https://realfavicongenerator.net/). We'll only need to put them in our public folder, and reference them in the `manifest.json` file.

The splash screen will also be generated from this file, using the name, icon, and background color provided.

#### Note
We can't forget to add the `viewport` meta tag to our HTML page. It optimizes our website to fit to the devices screen size.
```html
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
```

### Service Workers
__Service Worker__ → script the browser runs in the background separate from our app. Generally used for features that don't need a web page or user interaction. They act as a **programmable proxy**. They have been recently added into browsers. They provide the offline experience, background sync and push notifications.

Once we register a service worker, it can be in one of two states: stopped, to save memory, or running in the background, to fetch messages and events that occurs in the network request.

On PWAs our service worker will act as a **network proxy** - the request goes to the service worker, which verifies if there's anything in the Cache API. If the file requested is in cache, it returns the file to the app. Otherwise, it will let the request pass to the network.

If we created our app with Create React App, it automatically adds a *serviceWorker.js* file, which enables the offline experience. We just need to enable it by importing it in our *index.js* file and calling the registed method, `serviceWorker.register()`. However, if we are not using it, we can use [Workbox](https://developers.google.com/web/tools/workbox).

#### Register a Server Worker
```javascript
// Check for support of service worker
if('serviceWorker' in navigator) {
  navigator.serviceWorker.register('service-worker.js')
    .then(function(registration) {
      // Successful registration
      // scope is: registration.scope
    })
    .catch(function(err) {
      // Failed registration, service worker won't be installed 
    })
}
```

# Keywords
__Splash screen__ → screen presented to the user while the app is loading.

__Programmable proxy__ → allows us to control what happens on a request by request basis.

__Network proxy__ → intercepts any requests made first to the network, and checks to see if we really need to communicate with the network.

__Cache API__ → where the browser stores files, such as JavaScript files, and CSS files.

# Sources
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie

__Client-Side Rendering (CSR)__ → the client gets a bare-bones HTML page that links to the JavaScript files, which have to be downloaded and executed. Once the page is interactive, the browser doesn't have to make another request to the server - only parts of the webpage are loaded.

__Server-Side Rendering (SSR)__ → the server responds with a fully loaded HTML page, ready to be rendered to the user. However, the page is only interactive after the JavaScript has been evaluated.

Although the interactive point between CSR and SSR is the same, the two differ in when something is first displayed to the user. The Server-Side Rendered page appears a lot faster because it displays things on the page a lot sooner.

| | Pros | Cons
--- | --- | ---
CSR | - Rich Interactions<br>- Faster Response<br>- Web Applications | - Low SEO potential<br>- Longer initial load
SSR | - Static files<br>- SEO<br>- Initial Page Load | - Full Page Reloads<br>- Slower page rendering<br>- Increases codebase complexity

# SSR with React
For a basic SSR, we can use `renderToString` function from the *react-dom/server* package, passing the root component to it.
```javascript
import express from 'express'
import React from 'react'
import fs from 'fs'
import { renderToString } from 'react-dom/server'
import App from './App'

const app = express()
app.use(express.static('/public'))

const robots = JSON.parse(fs.readFileSync('/public/robos.json', 'utf8'))
const RobofriendsApp = React.createElement(App)
app.get('/', (request, response) => {
  response.render('index', {
    content: renderToString(RobofriendsApp({ data: robots }))
  })
})
```

On the browser, we have to do `ReactDOM.hydrate()`. This function will preserve the server-side rendered HTML, and will only attach the event listeners so the page can become interactive.

`ReactDomServer.renderToNodeStream()` uses **nodes streams** instead of plain text, which makes this process a lot faster.

## SSR React Libraries
Doing SSR with correctly is a hard thing to do. There are two very popular libraries to work with server-side rendering with React:
- __Gatsby__ → static site generator for React. Awesome for main-text based websites, *e.g.* documentation websites.
- __Next.js__ → full-blown dynamic tool to build rich applications. It's very easy to use, and we don't have to worry about `renderToString()`, *wepback*, routing, code splitting, and optimization.

### Next.js
Next.js includes routing, webpack setup, different types of CSS features, support for TypeScript, etc. To create a new Next.js project we can use:
```
$ npx create-next-app
```

We can also manually set it up by installing:
```
$ npm install next react react-dom
```
and updating the *package.json* scripts to use the `next` command.

Next.js excepts us to have a *pages* directory. Pages are associated with a route based on their file name.
```javascript
// pages/index.js
const Index = () => (
  <div>
    <h1>Page Title</h1>
  </div>
)

export default Index
```
With Next.js we don't need to import *React* on every file.

#### Client-Side Routing
__Client-Side Routing__ → a route is handle internally by JavaScript.

To move from one page to another, if we use a simple `<a>` tag, it will force a full page reload. We are provided with the `Link` component to handle page changes.

```jsx
import Link from 'next/Link'

const Index = () => {
  //...
  <Link href='/about'><a>About</a></Link>
}

export default Index
```

#### Dynamic Apps
Next allows us to fetch data before rendering the app, and pass it as `props`, by using `getInitialProps`. We can decide to either do this API call in the server or in the frontend.

```jsx
const RandomData = ({ data }) => {
  return (
    <div>
      <ul>
       {
         data.map(d => (
           <li key={d.id}>{d.name}</li>
         ))
       }
      </ul>
    </div>
  )
}

RandomData.getInitialProps = async () {
  // get data asynchronously
  return { randomData: data }
}
```

# Progressive Rendering
__Progressive Rendering__ → we send out only what we need for the initial render. Then, progressively, make more features and pages available in the background as more things arrive. This is achieved with code splitting.

Many companies use this kind of way of making their websites fast. There's also the idea of serving a **skeleton of an app** - on the initial render we serve a skeleton screen. This screen gets printed immediately, making the user feel that the content was loaded immediately, even though in the background there's still loading in the background.

It's important to think what we should render in the server, and what we sound render in frontend.

# Sources
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie

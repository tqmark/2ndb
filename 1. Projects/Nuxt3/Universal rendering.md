Nuxt has run the JavaScript (Vue.js) code in a server environment, producing an HTML document. Users immediately get the content of our application, contrary to client-side rendering. This step is similar to traditional **server-side rendering** performed by PHP or Ruby applications.

To not lose the benefits of the client-side rendering method, such as dynamic interfaces and pages transitions, the Client (browser) loads the JavaScript code that runs on the Server in the background once the HTML document has been downloaded. The browser interprets it again (hence **Universal rendering**) and Vue.js takes control of the document and enables interactivity.

Making a static page interactive in the browser is called "Hydration."

![[Pasted image 20230705174150.png]]
**Benefits of server-side rendering:**

- **Performance**: Users can get immediate access to the page's content because browsers can display static content much faster than JavaScript-generated one. At the same time, Nuxt preserves the interactivity of a web application when the hydration process happens.
- **Search Engine Optimization**: Universal rendering delivers the entire HTML content of the page to the browser as a classic server application. Web crawlers can directly index the page's content, which makes Universal rendering a great choice for any content that you want to index quickly.

**Downsides of server-side rendering:**

- **Development constraints:** Server and browser environments don't provide the same APIs, and it can be tricky to write code that can run on both sides seamlessly. Fortunately, Nuxt provides guidelines and specific variables to help you determine where a piece of code is executed.
- **Cost:** A server needs to be running in order to render pages on the fly. This adds a monthly cost like any traditional server. However, the server calls are highly reduced thanks to universal rendering with the browser taking over on client-side navigation. A cost reduction is possible by leveraging [edge-side-rendering](https://nuxt.com/docs/guide/concepts/rendering#edge-side-rendering).
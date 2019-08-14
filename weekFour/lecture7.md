###### Before I will continue with my journal writing, I will initially start by saying that, I have gone through **Matering Markdown**
This really helped me in:
* Making styled collborative editiing easy
* Formatting text
* Rendering text
* Using differnt extension
* Adding images in my journal
* Using quotes and header

# Express.js
**What is Express.js?**
*Express.js is a web framework based on the core of Node.js (http) module and connect (http://www.senchalabs.org/connect/) components. The components are called middleware and they are cornerstones of the framework philosophy, which is configuration over convention.  In other words, Express.js systems are highly configurable, which allows developers freely pick whatever **libraries** they need for a particular project. For these reasons, the Express.js framework leads to flexibility and high customization in the development of the web applications.*
*Express.js can serve as an effective framework which is based on Node.js. We can configure Express.js in any way we want. 


![Express.js](Express.jpg)


Based on Express.js, Node.js  framework is an effective tool for our home work, if we are considering. 
* Build a simple app.
* Consider the type of application you are building: prototype, production app, minimum viable product (MVP), small scale, large scale and so on.
* Consider the libraries already familiar to you and determine whether you can or plan to reuse them, and whether your framework plays nicely with them.
* Consider the nature of your application: REST API(with a separate front-end client), a traditional web app, or a traditional web app with REST API endpoints.
* Consider whether you need the support of reactive templates with WebSocket from the get-go.
* Evaluate the number of stars and follows on npm and GitHub to judge the popularity of the framework. More popular typically means more blogs posts, books, screencasts, tutorials and programs; less popular mean it's a newer framework, a custom choice, or a poor choice. With newer frameworks, there is a greater chance that contributing back to them will be valued.
* Evaluate npm, GitHub pages and a framework's website for the presence of good API docs with examples or open issues/bug.

**How Express.js works?**
Basically, Express.js works with an entry point and this is considered to be the main file. The names of these files could include server.js, apps.js, or index.js. This is the file where we begin with the node file. It is usually included with third party dependecnies. There are list of stuffs that we do while we are working on Express.js:
* Include third-party dependencies as well as our modules, such as controllers, utilities, helpers and models.
* Configure Express.js app setting, such as template engine and it's file extensions.
* Connect to databases such as MongoDB, Redis or MySQL.
* Define middleware such as error handlers, static file folder, cookies and other parsers.
* Define routes.
* Start the app.
* Export the app as module.
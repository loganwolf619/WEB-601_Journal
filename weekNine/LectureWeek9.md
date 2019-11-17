This week we worked on using restful api with the help of express.

# What is a REST API anyway?
The de-facto way to construct a web API is to follow the RESTful approach (referred to as a REST API).
REST APIs are resource-based interfaces. On the web this means that data resources (typically formatted in JSON, or XML) are represented by URIs (paths) accessed via HTTP.
Actions such as Create, Read, Update, and Delete (commonly referred to as CRUD) are made against these resources using HTTP methods (otherwise referred to as verbs): POST, GET, PUT/PATCH, and DELETE.
Each request made to a REST API is stateless. This means that the server handling your request maintains no context between requests: each request is interpreted equally. Any context required to process the request must be provided with the request itself (for instance, an authorization token).
Good REST APIs maintain a uniform interface. Meaning that the same shape of request which is made against a particular resource can reasonably be expected to act the same way against another resource (for instance, the request modifying an attribute on a Photo resource is uniform to that of modifying a similar attribute on an Album resource).
Another characteristic of a REST API is that server responses are cacheable. This means that based on context returned with the request’s response by the server you can cache the item. The server may return explicit instructions for how long a resource may be cached for (perhaps it instructs not to cache, or provides a recommended length of time to cache before refreshing).

Routing
Express.js is great for constructing a REST API because it provides an easy interface to segregate your resources by both type and action.
If you’ve previously built a web application with Express, you’ll find that the steps for creating an API using the same framework are very similar.
Let’s open index.js in your code editor.
This file is as bare bones as you can get when defining an Express application. We have created an application object and exported it for use.
```javascript
var express = require(‘express’);
var app = express();
module.exports = app;
```
The concept of Routes is used in Express for defining application behaviour to run when a particular request is received.
A route in Express is made up of three main parts:
The HTTP method associated the request we want to capture.
```javascript
app.get()
```
The URI (or path) of the request we want to capture.
```javascript
app.get('/');
```
A handler function (which accepts a request and response object as args)
```javascript
app.get('/', function(req, res) { });
```
This is an example of handling a GET request:

```javascript
var express = require(‘express’);
var app = express();
// Our handler function is passed a request and response object
app.get('/', function(req, res) {
  // We must end the request when we are done handling it
  res.end();
});
module.exports = app;
```

When constructing a REST API each HTTP method corresponds to an action against a resource served by the API.
* GET — retrieve a particular resource’s object or list all objects
* POST — create a new resource’s object
* PATCH — make a partial update to a particular resource’s object
* PUT — completely overwrite a particular resource’s object
* DELETE — remove a particular resource’s object

We can start laying out our API by specifying the routes for a single resource. This draws from the uniform interface characteristic of REST APIs. We are able to define the routes for one resource, then essentially copy and paste them for additional resources.
To specify our routes we’ll use an Express Router for each resource. We create the router object, specify the routes we wish to reply to, and then attach the router for a particular path.

```javascript
var express = require(‘express’);
var app = express();
// Create the express router object for Photos
var photoRouter = express.Router();
// A GET to the root of a resource returns a list of that resource
photoRouter.get(‘/’, function(req, res) { });
// A POST to the root of a resource should create a new object
photoRouter.post(‘/’, function(req, res) { });
// We specify a param in our path for the GET of a specific object
photoRouter.get(‘/:id’, function(req, res) { });
// Similar to the GET on an object, to update it we can PATCH
photoRouter.patch(‘/:id’, function(req, res) { });
// Delete a specific object
photoRouter.delete('/:id', function(req, res) { });
// Attach the routers for their respective paths
app.use(‘/photo’, photoRouter);
module.exports = app;
```

So now our API is ready to perform actions when we receive any of the following HTTP requests:

* GET /photo — Retrieve all photos
* GET /photo/:id — Retrieve a photo by its ID
* POST /photo — Create a new photo
* PATCH /photo/:id — Update properties of a photo by its ID
* DELETE /photo/:id — Delete a photo by its ID

This is what I will be using for my website development

If I restart my application and try to access /photo or /photo/123 I’ll find that the request hangs and my browser eventually times out. This is because the handler functions we specified do not end the request yet.
Your index.js file should now resemble the following code:

```javascript
var express = require(‘express’);
var app = express();
var photoRouter = express.Router();
photoRouter.get(‘/’, function(req, res) { });
photoRouter.post(‘/’, function(req, res) { });
photoRouter.get(‘/:id’, function(req, res) { });
photoRouter.patch(‘/:id’, function(req, res) { });
photoRouter.delete(‘/:id’, function(req, res) { });
app.use(‘/photo’, photoRouter);
var albumRouter = express.Router();
albumRouter.get(‘/’, function(req, res) { });
albumRouter.post(‘/’, function(req, res) { });
albumRouter.get(‘/:id’, function(req, res) { });
albumRouter.patch(‘/:id’, function(req, res) { });
albumRouter.delete(‘/:id’, function(req, res) { });
app.use(‘/album’, albumRouter);
module.exports = app;
```

## Resource Lookup
When we receive a request through a particular route we want to access that resource’s information from the database. This is so that we can return the data to the client performing the request.

Our code is getting verbose now and we want to reduce code duplication. This is where Express Middleware comes into play. Middleware are functions which perform specific actions based on request information, but can be re-used throughout your routers. These functions get passed to the route after the path, and before the handler function, as such:

```javascript

req.get(‘/photo/:id’, lookupPhoto, function(req, res) { });

```
We are going to be repeating quite frequently is looking up a particular resource object by its ID. So we can create a specific lookup function that is used on multiple routes.

```javascript
function lookupPhoto(req, res, next) {
  // We access the ID param on the request object
  var photoId = req.params.id;
  // Build an SQL query to select the resource object by ID
  var sql = ‘SELECT * FROM photo WHERE id = ?’;
  postgres.client.query(sql, [ photoId ], function(err, results) {
    if (err) {
      console.error(err);
      res.statusCode = 500;
      return res.json({ errors: [‘Could not retrieve photo’] });
    }
    // No results returned mean the object is not found
    if (results.rows.length === 0) {
      // We are able to set the HTTP status code on the res object
      res.statusCode = 404;
      return res.json({ errors: [‘Photo not found’] });
    }
    // By attaching a Photo property to the request
    // Its data is now made available in our handler function
    req.photo = results.rows[0];
    next();
  });
}
```

Now lets have a look at the lookup middleware function applied to our photo routes:

```javascript
var photoRouter = express.Router();
photoRouter.get(‘/’, function(req, res) { });
photoRouter.post(‘/’, function(req, res) { });
photoRouter.get(‘/:id’, lookupPhoto, function(req, res) { });
photoRouter.patch(‘/:id’, lookupPhoto, function(req, res) { });
photoRouter.delete(‘/:id’, lookupPhoto, function(req, res) { });
app.use(‘/photo’, photoRouter);
```
## Responding to requests
When building a RESTful API there are a few concepts we want to be mindful of when responding with data:
1. HTTP status codes should describe the response
2. Data returned should be formatted in JSON (preferred) or XML

## HTTP status codes
There are a multitude of HTTP status codes, here is just a few of the pertinent ones (which we will be using):
1. 200 — OK, The request was successful
2. 201 — CREATED, A new resource object was successfully created
3. 404 — NOT FOUND, The requested resource could not be found
4. 400 —BAD REQUEST, The request was malformed or invalid
5. 500 — INTERNAL SERVER ERROR, Unknown server error has occurred
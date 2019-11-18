This is the last week before our Milestone 2. I am still struggling to figure out my work.
I guess I am not built for webdeveloment.
More or less, I am not built for coding. However, I still managed to do some tasks. 
![Image of components](1.png)
This is what I created so far.
![Image of src components](2.PNG)
![Image of server components](3.png)

The images above shows the list of files I created for the development of the assignment. 

I created a file in server named as: restful.js
```javascript
// We are going to access the Express and Cors Modules
const express = require('express');
const app = express()
let cors = require('cors')

// We are going to access the Router, Config, and Middleware Code
const router = express.Router()
const config = require('./config')
const middleware = require('./middleware')

// We are using Body Parser to convert our Posted data to Json format
const bodyParser = require('body-parser')
const jsonParser = bodyParser.json()

// We are going use the KNEX to connect with our MySQL database
const knex = require('knex')({
  client: 'mysql',
  connection: config.database
})

// We are going to add the KNEX Database connection to the app.locals
app.locals.knex = knex

// We are going to use the route between the Database queries and the request.This will point to the route it is connecting
const routes = require('./routes')

//We are now going to create route for each request type. We are going to use the ID to retreive the data.

// We are going to use the routes to get all the Graphics
route.get('/Graphics', routes.graphicsList.listAllGrpahics);

// We are going to obtain single Graphics based on the GraphicsID
router.get('/Graphics/:GraphicsID', middleware.checkID, routes.graphicsList.listAllGrpahics);

// We are going to create a route to POST a new Graphics by creating  a new record in the database
router.post('/Graphics', jsonParser, routes.graphicsList.postGraphics);

// We are going to Update or patch the existing Graphics in the database if needed
router.patch('/songs/:GraphicsID', jsonParser, middleware.checkID, routes.graphicsList.updateGraphics)

// We are going to Delete a graphics from the database
router.delete('/Graphics/:GraphicsID', middleware.checkID, routes.graphicsList.deleteGraphics)

// We are going to route to POST a new Support Team
router.post('/supportTeam', jsonParser, routes.supportTeam.postSupportTeam)

// We are going to route to POST to the newly connected accounts
router.post('/users', jsonParser, routes.users.postUsers)

// We are going to use Express to route between the requested host and route
app.use('/api', cors(), router);

// We are going let the server to start listening to the port that has been specified in the config.js file
app.listen(config.APIServerPort, () => {
  console.log('Server has been lost at port  ${config.APIServerPort}');
});
```

And I created a route.js file to connect my database with the website.
```javascript
//This is connect the Request and the KNEX query that I created for the database, which 
// will be used in the development of this Website
const graphicsList = require('./dbGraphics.js')
const supportTeam = require('./dbSupportTeam')
const users = require('./dbUsers')

module.exports = {
    graphicsList,
    supportTeam,
    users
}
```
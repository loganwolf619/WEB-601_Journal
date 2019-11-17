Today we wil be workin on building the react app from the scrap.

We will start our project by initially installing our dependecies.
Once we installed the dependencies (run npm install), we can build the project with a single command:
npm run build.
The build script adds two more scripts to the package.json. They are ready to use!

* npm run {your-project-name} starts your React-app locally (hot-dev mode, without backend and database)
* npm run start-{your-env-name} starts the whole software stack locally.
However accoring to Ali's lecture and my learning's from video, these steps are needed to be mainatained. These include:
1. Creating an index.html file
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <link rel="apple-touch-icon" href="logo192.png" />
   
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
   
    <!--Bootstrap react-->
    <link
  rel="stylesheet"
  href="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
  integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T"
  crossorigin="anonymous"
/>
    <!--Google Fonts-->
    <link href="https://fonts.googleapis.com/css?family=Montserrat:400,700" rel="stylesheet" type="text/css">
    <link href='https://fonts.googleapis.com/css?family=Kaushan+Script' rel='stylesheet' type='text/css'>
    <link href='https://fonts.googleapis.com/css?family=Droid+Serif:400,700,400italic,700italic' rel='stylesheet' type='text/css'>
    <link href='https://fonts.googleapis.com/css?family=Roboto+Slab:400,100,300,700' rel='stylesheet' type='text/css'>
<!--Font Aweseome-->
<link href="vendor/fontawesome-free/css/all.min.css" rel="stylesheet" type="text/css">

<!-- Custom styles for this template -->
<link href="css/agency.min.css" rel="stylesheet">

<!--Bootsrap 4 CDN-->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">
  
  <!--Fontawesome CDN-->
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.3.1/css/all.css" integrity="sha384-mzrmE5qonljUremFsqc01SB46JvROS7bZs3IO2EmfFsd15uHvIt+Y8vEf7N7fWAU" crossorigin="anonymous">

<!--Custom styles-->
<link rel="stylesheet" type="text/css" href="css/agency.min.css">
    <title>Apex ShutterBug</title>
  </head>
  <body>

  </body>
</html>
```
2. Create the body
3. Create an index.css file to change the contents of the whole website
4. Then add a live server and this can be installed with the help of 'npm i -g live-server'
5. Test the live server
6. Next install Babel. User: npm init -y
7. To set the babel use: 'npm install --save babel-preset-env@latest babel-preset-react@latest'
8. In the react class we are going to cretae a src folder.
9. In the src folder we are going to create files which includes:
* App.js
* App.css
* index.js
* index.css
10. In the index.js we can use this format:
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import {BrowserRouter as Router} from 'react-router-dom';
import * as serviceWorker from './serviceWorker';
import 'bootstrap';
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap/dist/js/bootstrap.js';
// import $ from 'jquery';
import Popper from 'popper.js';

ReactDOM.render(
<Router>
    <App />
</Router>, 
document.getElementById('root'));
```

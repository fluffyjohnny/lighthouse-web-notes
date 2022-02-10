# W3D1 - Node JS

## What is Node Js?
it is javasscript extracted to be used for the backend 


## HTTP package vs. NPM Express

### Writing a `Web Server` from scratch from HTTP Package
```javascript 
const http = require('http');
const fs = require('fs'); // way to interact with the file system 
const path = require('path'); // interact with the file system in an operating system independent way
const todos = require('./db/todos'); // bring in a array of todo objects 

const port = 3001; // port to listen to 

// defined inside the http package, which this function takes a callback, which the CB will take a resposse and request object
const server = http.createServer((request, response) => {
  consoel.log('createServer callback request event listener was called');

  const route = `${request.method} ${request.url}`; //
  console.log('method', request.method); // what type of request 
  console.log('path', request.url); // what path is requested

  //response to a request for a particular route using the switch case syntax
  switch (route) {
    case 'GET /':

      filePath = path.join(_dirname, 'views', 'index.html')
      console.log('retrieving view from:' + filePath);
      fs.readFile(filePath, 'utf8', (err, fileContent) => {
        if (err) {
          response.statusCode = 500;
          response.write(erroMsg);
          response.end();
        } else {
          response.statusCode = 200
          response.write(fileContent);
          response.end();
        }
      })

      const htmlString = 
      `<html>
      <head></head>
      <body>
      <h1>Chickenbutt is Alive!!</h>
      </body>
      </html>`

      response.statusCode = 200; //main purpose is to give information to the browser about the status of the code 
      response.write(htmlString); // return a HTML when requested '/' path
      response.end(); // if we don't include a .end, the client will just stay there keep waiting for us to send more .write

      break;
    case 'GET /todos':

      const todoList = JSON.stringify(todos); // turn the array of objects into a string, so we can send this string back to the client

      response.statusCode = 200; // success response
      response.write(todoList); // output this string onto the web server
      response.end(); // gather everything and send off to the client

      break;
    default:
      response.statusCode = 404;
      response.write(`Not Found! <img scr="link">`);
      response.end();
      break;
  }
}) 

server.listen(port, () => {} ) // allows the server to take in requests from the specific port, hanging out in the event loop, and everytime a request is make it calls back the server function
``` 

-----------

###  Writing a web server with `Express`
```javascript
// need to install npm install express
const express = require('express'); // make an express object which is a function valued variable
const todos = require('./db/todos')
const port = 3002; 
const app = express()

// template engine, takes two strings
// npm install ejs --save
app.set('view engine', 'ejs');

// takes a path and a callback with request and response
// didn't need to define a route, all done within express
// ** the order of the match matters
// this callback is being configured by express to be executed when it matches this route, in this case the route = 'GET /'
app.get('/', (req, res) => {
  // res.write('Welcome to express'); // without app.set
  res.render('index'); // looks into the 'views' directory by default that contains index.ejs
  res.end();
});

// route = GET /todos
app.get('/todos', (req, res) => {

  // pass in the dynamic value as a parameter into the render function
  const templateVars = {
    foobar: JSON.stringify(todos);
  };


  // res.json(todos);
  res.render('todoList', templateVar) // from 'views' directory
  // in todoList.ejs, <%= foobar %> which will just take the value within the aligator clips, <% function() %> 
  res.end();
});

// wildcard, like a default in a swtich statement
// this one needs to be at the bottom of the list 
app.get('*', (req, res) => {
  res.status(404).write('404 NOT FOUND');
  res.end();
})

// express will look through our directories, and execute the one that matches

app.listen(port, () => {
  console.log(`Server is listening on port ${port}`)
});



```

ejs template 
```html
<%= foobar %>

<ul>
  <% for (let i = 0; i < foobar.length; i++) { %>
    <li><%= foobar[i].description %> </li>
  <% } %>
</ul>


// <% 'Scriptlet' tag, for control-flow, no output
// <%= Outputs the value into the template (HTML escaped)
// <%- Outputs the unescaped value into the template
```


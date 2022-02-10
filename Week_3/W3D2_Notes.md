# W3D2 Notes 

## CRUD VS. BREAD 

CRUD
- Creat
- Read
- Update
- Delete 

BREAD
- Browse 
- Read
- Edit
- Add
- Delete

We will be focusing on BREAD today since it is more complete 

```javascript
const express = require('express');
const app = express();
const PORT = 8085;
const bodyParser = require('body-parser');
app.set('view engine', 'ejs');


// MIDDLEWARE
  // forever request, something that occurs to every request no matter what 
app.use(morgan('dev'));
  // used for app.post
app.use(bodyParser.urlencoded({extended: false}));


// DATA 
const objectives = [
  {question: 'what EJS templates?', answer: 'we use templates to separate bisiness logic from the presentation layer.'},
  {question: 'How do we implement EJS Templates?', answer: "npm i ejs, mkdir views, app.set('view engine', 'ejs');"},
  {question: 'what does CRUD stand for?' answer: 'Create, Read, Update, Delete'},
  {question: `where are the URL parameters stored?`, answer: 'req.params'},
  {question: `Where are <form> values stored?`, answer: `req.body`}
]

// ROUTES


// BROWSE 
app.get('/', (req, res) => {
  // code here only run for that specific route 
  const templateVars = {
    objectives: objectives,
  }
  res.render('index', templateVars);
})


// READ 
  // click on a botton and get more information on that thing 
  app.get('/read/:index', (req, res) => {
    // req.params is an object, whatever value after /read/(here), becomes req.params
    const index = req.params['index'];
    const templateVars = {
      objective: objectives[index]
    }
    res.render('read', templateVars);
  })

  //read.ejs
  <%= objective.question %>
  <%= objective.answer %>


// EDIT 

app.get('/edit/:iii', (req, res) => {
  const index = req.params['iii'];
  const templateVar = {
    objective: objectives[index],
    index: index
  }
    res.render('edit', templateVars);
  })

  app.post('/edit/:jjj', (req, res) => {  
    const index = req.params['jjj'];

    objectives[index].question = req.body.question;
    objectives[index].answer = req.body.answer;

    res.redirect('/');
  })

  //edit.ejs

  <form method="POST" action="/edit/<%= index %>">
    <label for="question">Question</label> 
    <input 
      name="question" 
      id="question" 
      type="text" 
      value="<%= objective.question %>"
    />

    <label for="answer">Answer</label> 
    <input 
      name="answer" 
      id="answer" 
      type="text" 
      value="<%= objective.answer %>"
    />

    <input 
      name="index"
      id="index"
      type="hidden"
      value="<%= index %>"
    />
    <input 
      name="Edit" 
      id="submit" 
      type="submit"
      value="Edit"
    />
  <form>



// ADD
   app.get('/add', (req, res) => {
    res.render('add');
  })

  app.post('/add', (req, res) => {  
    // from Data 
    objectives.push({
      question: req.body.question,
      answer: req.body.answer
    });

    //after submitting, redirect the user to the home page
    res.redirect('/');
  })

  //add.ejs
  <form method="POST" action="/add">
    <label for="question">Question</label> 
    <input name="question" id="question" type="text"/>

    <label for="answer">Answer</label> 
    <input name="answer" id="answer" type="text"/>

    <input name="Submit" id="submit" type="submit"/>
  <form>


// DELETE


app.listen(PORT, () => {
  console.log(`Server is listening on Port ${PORT}`)
});
```
`nodemon` is a useful npm package that runs the server and moderates it 
 - `rs` // restart server 
 - it restarts the server whenever the server is changed 


 ### Different scriptlet/aligator clips 
 ```javascript
 <%= /* take the output and print it onto the template */ %>
 <% /* permits JavaScript without outputting the code (dynamic value) */ %>
 ```

 ### Rest API 
 application programming interface

 a convention for the naming of these routes

 widget -> widgets 

verb path 

GET /widgets  // get a list 

GET /widgets/:id // get individual widget

POST /widgets // creating new one 
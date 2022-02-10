# W3D3 Cookies
- HTTP statelessness 
- Cookies 
- Login/register process with cookies 

## HTTP is stateless 
http itself does not come with any form of identification or state, the server does not remember any information from the request

- pros 
  - scalability 
  - less comupation


## Browser cookies 
- with cookies we can shareinformation between the sever and the broeswer with each request 
- provides a way for servers to recognize the user brtween requests 
- cookies are used to store a user ID

```javascript 
npm install express morgan boday-parcer cookie-parcer ejs nodemon --save

const express = require('express');
const PORT = 8081;
const bodyParser = require('body-parser'); // for POST
const cookieParser = require('cookie-parser'); // to display cookie info
const app = express()
app.set('view engine', 'ejs');
```

```javascript
///  DATA  ///
const users = {
  1: {id: 1, user: 'johnusername@email.com', password: 'initpassword'}
};


//middleware
app.use(bodyParser.urlencoded({ extended: false})); // use simple text parsing
app.use(cookieParser()); // see what is retured by the require
``` 

///  Routes  ///
```javascript
// home page

app.get('/', (req, res) => {
  res.render('home');
  res.end();
})
```
```javascript
// login

app.get('/login', (req, res) => {
  res.render('login');
  res.end();
})

function verifiedUser(email, password) {
  for (let id in users) {
    if (users[id].email === email && users[id].password === password) {
      return users[id];
    }
  }
  return false;
}

app.post("/login", (req, res) => {
  const candidteEmail = req.body.email;
  const candidatePassword = req.body.password;
  // check if the input password is the same as the database
  if (verifiedUser(candidateEamil, candidatePassword)) {
    // allows log in, set a cookie and send them to the profile page
    console.log('Login Successful')
    res.cookie('user', userObj.id);
    res.redirect('/profile');
  } else {  
    // need an else here since it is asynchronous, so it only runs one or the other 
    console.log('login INVALID')
    res.redirect('/login');
  }
})
```

```javascript
// register

app.get('/register', (req, res) => {
  res.render('register');
  res.end();
})

app.post("/register", (req, res) => {
  const newEmail = req.body.email;
  const newPassword = req.body.password;

  const generateRandomString = (len) => {
	  let outputStr = "";
	  for (let i = 0; i < len; i++) {
		let rndm = Math.floor(Math.random() * 62);
		  if (rndm <= 9) {
			  outputStr += String.fromCharCode(rndm + 48);
		  } else if (rndm >= 36) {
			  outputStr += String.fromCharCode(rndm + 61);
		  } else {
			  outputStr += String.fromCharCode(rndm + 55);
		  }
	  }
	  return outputStr;
  };

  // check if the email is already in database
  if (users[newEmail]) {
    console.log('email already in use')
    res.redirect('/register');
  } else {  
    // login the new user
    console.log(`users`, users) // to see debug what the user is like after adding the new user
    const newId = generateRandomString(4)
    user[newId] = {id: newId, email: newEmail, password: newEmail};
    res.redirect('/login');
  }
})
```

```javascript
// profile

app.get('/profile', (req, res) => {
  console.log('req of cookies', req.cookies) // see the cookie object {user: email}
  const userId = req.cookies.user;

  const templateVars = {
    secret: 'this is a secret',
  };

  // check if they are logged in with cookies
  if (user[userId]) {
    res.render('profile', templateVars);
    res.end();
  }
  res.redirect('/login');
});
```
```javascript
// logout
app.get('/logout', (req, res) => {
  res.clearCookies('user');
  res.redirect('home');
  res.end();
})
```

```javascript
// catch all else

app.get('*', (req, res) => {
  res.render('404');
  res.end();
})
```

```javascript
// PORT
app.listen(PORT, () => {
  console.log(`Server is listening on ${PORT}`)
})

```
 --------------------------   // EJS //   -----------------------------
```javascript
// home ejs
<title>HOME</title>
  <ul>
    <li><a href='/login'>Login</a></li>
    <li><a href='/register'>Register</a></li>
    <li><a href='/profile'>Profile</a></li>
    <li><a href='/logout'>Logout</a></li>
  </ul>


```

```javascript
// 404 ejs

<p>Not found! code 404</p>

```

```javascript
// login ejs

<title>LOGIN</title>
<h2>Please Login</h2>
<form method="POST" action="/login">
  <label for="email">Email:</lable>
  <input name="email" id= "email" type="text"/>

  <label for="password">Password:</lable> 
  <input name="password" id= "password" type="password"/>

  <input name="login" id= "login" type="submit" value="Login"/> 
</form>


```

```javascript
// register ejs

<title>REGISTER</title>
<h2>Please Register</h2>
<form method="POST" action="/login">
  <label for="email">Email:</lable>
  <input name="email" id= "email" type="text"/>

  <label for="password">Password:</lable> 
  <input name="password" id= "password" type="password"/>

  <input name="login" id= "login" type="submit" value="Register"/> 
</form>


```
```javascript
// profile ejs

<title>PROFILE</title>

  <h2>Welcome 2 profile</h2>

  <h4><%= secret %></h4>

```
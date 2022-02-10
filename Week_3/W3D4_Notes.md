# W3D4 - Cookies & Security 



```javascript 
app.set('view engine', 'ejs') // <-- engine is the render machine 
app.use() //  <-- use what we imported (middleware)

middleware // middleware is the process function that happens between a request and a response 

```

encryption : we scramble a value, but is unscrambable --> return to original 
hashing: we scramble a value, but we never know the original after 

bcryptjs to hash our passwords 


```javascript

const salt = bcrypt.genSaltSync(10) // add hash flavor to cookie, prevents collision between hashes

app.post(('/register') => { 
  const { name: newNameVariable, email, password, secret } = req.body
  // one of the field is empty
  if (!email || !name || !password || !secret) {
    return res.redirect('/register')
  }
  // if email already exists
  if (userDatabase.hasOwnProperty(email)) {
    return res.redirect('/register')
  }
  // success
  const hashedPassword = bcrypt.hashSync(password, salt);
  const newUser = {name, email, hashedPassword, secret}
  userDatabase[email] = newUser
  req.session.email = email
  return res.redirect('/secret')
})





// in register ejs, input = required, but can be easily changed from developer mode 

 ```

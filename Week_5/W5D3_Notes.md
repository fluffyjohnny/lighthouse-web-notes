# W5D3 

## CLIENT   
```javascript
const pg = require('pg');
const Client = pg.Client;

const configObj = {
  user: 'postgres',
  host: 'localhost',
  database: 'spot',
  password: 'postgres',
  port: '5433'
}

const client = new Client(configObj);

client.connect()
.then(() => {
  console.log('connected')
})
.catch((error) => {
  console.log)('error', error)
});

const verb = process.argv[2];

switch (verb) {
  case 'browse':
    client.query('SELECT * FROM objectives ORDER BY id;')
    .then((response) => {
      console.log('response: ', response);
      response.rows.forEach((row) => {
        console.log(`${row.id} :: ${row.question}`)
      })
    })
    .catch((error) => {
      console.log('db browse error: ', error);
    });
    break;
  case 'read':
    const id = process.argv[3];
    client.query(`SELECT * FROM objectives WHERE id = ${id};`)
    .then((response) => {
      console.log('response: ', response);
      response.rows.forEach((row) => {
        console.log(`${row.id} :: Question: ${row.question}`)
        console.log(`Type: ${row.type}`)
        console.log(`Answer: ${row.answer}`)
      })
    })
    .catch((error) => {
      console.log('db browse error: ', error);
    });
    break;
  default:
    console.log('usage: node cli.js <browse || read || ..>');
    break;
}
```

```javascript
| grep [thing] // to chain commands in the command line
```


!!!!!  THE CODE ABOVE IS VERY VULNERABLE TO HACKING  !!!!!

need to check the type of data being stored 

how to make a copy of the database, "`pg_` double tap" then select pg_dump
```
pg_dump -U postgres -p 5433 spot > db-spot-snapshot... 
```

instead of putting in a hard coded string, we will put it into an array as a second parameter for the query function call

```javascript
client.query(`SELECT * FROM objectives WHERE id = $1;`, [id])
```
$1 is a token that query will recognzie as a token and use it as the first index of the array 



## SERVER 

``` javascript
const express = require('express');
const PORT  = 7889;
const APP = express();

app.set('view engine', 'ejs')

// SET UP 

const client = new Client(configObj);

client.connect()
.then(() => {
  console.log('connected')
})
.catch((error) => {
  console.log)('error', error)
});

// MIDDLEWARE


// ROUTES 

app.get('/', (req, res) => {
  client.query('SELECT * FROM objectives ORDER BY id;')
    .then((response) => {
      console.log('response: ', response);
      response.rows.forEach((row) => {
        console.log(`${row.id} :: ${row.question}`)
      })
    })
    .catch((error) => {
      console.log('db browse error: ', error);
    });
  res.render('home');
})

app.listen(PORT, () => {
  console.log(`Server is listening on PORT ${PORT}`)
})
```


## NPM package dotenv
- prevent password from showing up on github in our database
- create a .env file
  - require('dotenv').config();
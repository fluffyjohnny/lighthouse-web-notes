# W2D3 - Web & Net connections 

the internet is a network of networks that connects devices together, and the web is the interface of the internet 

in 1969 there are only 4 computer connected to the internet, and a lot has grown from there.


##  Transport Control Protocol

created to send data from one to the other as long as the internet is established. It is originally created to survive the nuclear attack if one city's server was destroyed; as long as the recieving city's server isn't affected, the data can stilll be transferred.

## Internet 

runs on a client-server pair

## Server 

```javascript
// built into node to allow us to interact with the internet
const net = require('net');
// port that the clinets will be connected to
const port = 8009;
const server = net.createServer();


// list of all the clinets
const connectedClients = [];

// function that outouts the message to everyone other than the sender in the connectedClient list
const broadcast = (message, sender) => {
  connectedClients.forEach((client) => {
    if (client !== sender) {
      client.write(`${sender.name}: ${message}`);
    }
  });
};



// when a connection is established
server.on('connection', (client) => {

  console.log('New client connected!');

  // interpret data as text
  client.setEncoding('utf8');

  // add the client into the client list
  connectedClients.push(client);

  // what the server will output to the client when connected
  client.write('Hello there!');

  // logs out what the client sends to the server
  client.on('data', (message) => {
    console.log('Message recieved from client: ', message);

    // setting client name to clientName
    if (message.startsWith('setName ')) {
      const clientName = message.replace(/setName /, '');
      client.name = clientName;
    }
    // broadcast the message recieved
    broadcast(message);
  });
});

server.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});

// these servers will be set up asynchronously, and the clients will become allowed to join into the event loop

```

## Client

```javascript
const net = require('net');
const stdin = process.stdin;

const connectionConfig = {
  host: 'localhost', // change to IP address of computer or ngrok host if tunneling
  port: 8009 //// or change to the ngrok port if tunneling
};


// CLIENT

const client = net.createConnection(connectionConfig);

client.setEncoding('utf8'); // interpret data as text

client.on('data', (message) => {
  console.log('Server says: ', message);
});

// when connection is established between client and server
client.on('connect', () => {
  client.write('Hello from client!');
});

client.on('end', () => {
  console.log('clinet disconnected from server');
});


// Stdin

// type on the client, and that will send to the server
process,stdin.on('data', (message) => {
  client.write(message);
});
```


## HTTP protocol 


in order to reques resources from an HTTP server, we need to know its URL, which it
stores a lot of information.

* `https://` - protocol
* `www ` - sub-domain
* `google.come ` - domain name 
* `.com ` - top-level domain
* `:80 ` - port (only if you're using a non-standard port number)
* `/search ` - path 
* `? `- query
* `q=bootcamp ` - parameters (can have multiple)
* `#montreal ` - fragment/anchor (go into the page and automatically scroll down to the section of the page)



### 4 HTTP request methods 
  - `GET ` - used to 'get' some data from the server 
  - `POST ` - usually used to create some new data
  - `PUT ` - generally used for editing existing data on the server 
  - `DELETE ` - used to delete some existing data


### HTTP Responses

- Status code 
  - Error codes 
    - if a requested resource wasn't found, or if the server itself is simply unable to perform the action at the moment.
    - `200 ` - Everything went great
    - `201 ` - The request has succeeded and a new resource has been created as a result.
    - `404 ` - Resource was not found. 
    - `500 ` - The server had an error.
- Body
  - contain some data the client originally requested 
    - often contani webpages (HTML) pr data encoded in `JSON`


### npm Request library 

the `request` module makes HTTP requests easy! Behind the scenes, it uses http which in turn uses `net`, in the way that we did recently 

```javascript
const request = require('request');

request('http://www.google.com', (error, response, body) => {

  console.log('error:', error); // Print the error if one occurred

  console.log('statusCode:', response && response.statusCode); // Print the response status code if a response was received

  console.log('body:', body); // Print the HTML for the Google homepage.
  
});
```

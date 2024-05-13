<h1 style="color:#99bf9a">Node.js</h1>

> - <a style="color:#000000">Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It allows you to run JavaScript code on the server-side.</a>

<h3 style="color:#99bf9a">Installation</h3>

> - <a style="color:#000000">Download from official website and check if node and npm are installed with what commands?</a>
> <br> A: node -v ; npm -v

<h3 style="color:#99bf9a">Basic Node.js App</h3>

> - <a style="color:#000000">Create a project directory</a>

```javascript
mkdir my-node-app
cd my-node-app
```

> - <a style="color:#000000">Initialize Node.js project</a>

```javascript
npm init -y
```
> What will this command do? (Particularly, what file does this command create?
>
> - <a style="color:#000000">Create a JS file and call it index.js with following content</a>

```javascript
console.log("Hello, Node.js!");
```

> - <a style="color:#000000">Now run the app by executing the following command in the terminal</a>

```javascript
node index.js
// it will output in the terminal: Hello, Node.js!
```

> - <a style="color:#000000">You can manage dependencies with npm using the following command</a>

```javascript
npm install express
// This command installs the express package and adds it to your package.json file as a dependency.
```

> When you install dependencies using npm, they are saved in the node_modules directory within your project. You don't need to manually include this directory in version control as npm will generate a package-lock.json file that specifies the exact versions of dependencies installed.

> - <a style="color:#000000">Using installed packages and a basic express.js application is provided below. Paste below code in index.js file</a>

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send('Hello, Express!');
});

app.listen(3000, () => {
    console.log('Server is running on http://localhost:3000');
});

// Start your application by running 'node index.js' in terminal
// and now, if you navigate to http://localhost:3000 in your web browser,
// you should see the message: 'Hello, Express!'
```

<h3 style="color:#99bf9a">Core Node.js Modules</h3>

<h4 style="color:#99bf9a">File System (fs) - Interacting with file system on your computer</h4>

> - <a style="color:#000000">Reading and writing to files</a>

```javascipt
const fs = require('fs');

// Reading a file
fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(data);
});

// Writing to a file
fs.writeFile('example.txt', 'Hello, Node.js!', (err) => {
    if (err) throw err;
    console.log('File written successfully.');
});

```

> - <a style="color:#000000">Creating, deleting and, renaming files and directories</a>

```javascript
const fs = require('fs');

// Create a directory
fs.mkdir('./example_directory', (err) => {
    if (err) {
        console.error('Error creating directory:', err);
    } else {
        console.log('Directory created successfully.');
        
        // Create a file inside the directory
        fs.writeFile('./example_directory/example.txt', 'Hello, Node.js!', (err) => {
            if (err) {
                console.error('Error creating file:', err);
            } else {
                console.log('File created successfully.');
                
                // Read the content of the file
                fs.readFile('./example_directory/example.txt', 'utf8', (err, data) => {
                    if (err) {
                        console.error('Error reading file:', err);
                    } else {
                        console.log('File content:', data);
                        
                        // Rename the file
                        fs.rename('./example_directory/example.txt', './example_directory/new_example.txt', (err) => {
                            if (err) {
                                console.error('Error renaming file:', err);
                            } else {
                                console.log('File renamed successfully.');
                                
                                // Delete the file
                                fs.unlink('./example_directory/new_example.txt', (err) => {
                                    if (err) {
                                        console.error('Error deleting file:', err);
                                    } else {
                                        console.log('File deleted successfully.');
                                        
                                        // Delete the directory
                                        fs.rmdir('./example_directory', (err) => {
                                            if (err) {
                                                console.error('Error deleting directory:', err);
                                            } else {
                                                console.log('Directory deleted successfully.');
                                            }
                                        });
                                    }
                                });
                            }
                        });
                    }
                });
            }
        });
    }
});

```

> - <a style="color:#000000">Modifying file permissions</a>

```javascript
const fs = require('fs');

// Path to the file
const filePath = 'example.txt';

// Define the new permissions (in octal notation) (read = 4, write = 2, execute = 1)
const newPermissions = 0o644; // Example: Read and write for owner, read-only for others 

// Modify the file permissions
fs.chmod(filePath, newPermissions, (err) => {
    if (err) {
        console.error('Error modifying file permissions:', err);
    } else {
        console.log('File permissions modified successfully.');
    }
});

```

<h4 style="color:#99bf9a">HTTP - To create HTTP servers and make HTTP requests</h4>

> - <a style="color:#000000">Create an HTTP server and handle requests and responses</a>

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    // Set the response headers
    res.writeHead(200, { 'Content-Type': 'text/plain' });

    // Determine the requested URL
    const url = req.url;

    // Handle different URLs
    if (url === '/') {
        res.write('Hello, World!');
    } else if (url === '/about') {
        res.write('About Page');
    } else {
        res.write('404 Not Found');
    }

    // End the response
    res.end();
});

// This is how you start the server
server.listen(3000, () => {
    console.log('Server is running on port 3000');
});

```

> The req parameter represents the request object, which contains information about the incoming HTTP request, such as the request method, URL, headers, and any data sent with the request (e.g., request body for POST requests)

```javascript
// Here's an example of what the body of the req object might look like for a typical HTTP request
{
  "method": "GET",
  "url": "/example",
  "headers": {
    "host": "localhost:3000",
    "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36",
    "accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
    "accept-encoding": "gzip, deflate, br",
    "accept-language": "en-US,en;q=0.9",
    "cookie": "example_cookie=example_value",
    // Other headers...
  },
  "body": "example body content",
  "query": {
    // Query parameters (if any)
  },
  "params": {
    // Route parameters (if any)
  }
}

```

> - <a style="color:#000000">Not sure where this below code would be placed in an application?</a>

```javascript
// What http client side might look like
const http = require('http');

const options = {
    hostname: 'www.example.com',
    port: 80,
    path: '/',
    method: 'GET'
};

const req = http.request(options, (res) => {
    console.log(`Status Code: ${res.statusCode}`);
    
    res.on('data', (chunk) => {
        console.log(chunk.toString());
    });
});

req.end();

```

<h4 style="color:#99bf9a">Paths - Handling file paths in a cross-platform way</h4>

> - <a style="color:#000000">Joining and Normalizing file paths</a>

```javascript
const path = require('path');

const filePath = path.join(__dirname, 'folder', 'file.txt');
console.log(filePath); // Output: /path/to/your/current/directory/folder/file.txt

// In Node.js, __dirname is a special variable that represents the directory name of the current module.
// It provides the absolute path to the directory containing the currently executing script file.
```

> So, the 'filePath' variable will contain the absolute path to the file 'file.txt' located within the 'folder' directory relative to the directory of the current module.
>
> For example, if the current module is located at /path/to/your/current/directory/module.js, then __dirname would be /path/to/your/current/directory. Therefore, the filePath would be /path/to/your/current/directory/folder/file.txt.


> - <a style="color:#000000">Parsing file paths into Segments</a>

```javascript
const path = require('path');

const filePath = '/path/to/your/current/directory/folder/file.txt';
const pathInfo = path.parse(filePath);
console.log(pathInfo);
/*
Output:
{
  root: '/',
  dir: '/path/to/your/current/directory/folder',
  base: 'file.txt',
  ext: '.txt',
  name: 'file'
}
*/

```

<h4 style="color:#99bf9a">Operating System - To gather information about the operating system</h4>

> - <a style="color:#000000">Retrieve information such as CPU architecture, total memory, platform, and network interfaces</a>

```javascript
const os = require('os');

// Retrieving cpu architecture
console.log('CPU Architecture:', os.arch());

// Retrieving platform
console.log('Platform:', os.platform());

// Retrieving total memory
console.log('Total memory:', os.totalmem());

// Retrieving Network Interfaces
console.log('Network Interfaces:', os.networkInterfaces());

// Some others
// console.log(os.freemem());         // Free system memory
// console.log(os.cpus());            // Information about CPUs
```

> Here's a sample output

```
CPU Architecture: x64
Platform: linux
Total memory: 16263266304
Network Interfaces: {
  lo: [
    {
      address: '127.0.0.1',
      netmask: '255.0.0.0',
      family: 'IPv4',
      mac: '00:00:00:00:00:00',
      internal: true,
      cidr: '127.0.0.1/8'
    },
    {
      address: '::1',
      netmask: 'ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff',
      family: 'IPv6',
      mac: '00:00:00:00:00:00',
      internal: true,
      cidr: '::1/128'
    }
  ],
  wlp2s0: [
    {
      address: '192.168.1.10',
      netmask: '255.255.255.0',
      family: 'IPv4',
      mac: 'xx:xx:xx:xx:xx:xx',
      internal: false,
      cidr: '192.168.1.10/24'
    ],
    {
      address: 'fe80::xxxx:xxxx:xxxx:xxxx',
      netmask: 'ffff:ffff:ffff:ffff::',
      family: 'IPv6',
      mac: 'xx:xx:xx:xx:xx:xx',
      internal: false,
      cidr: 'fe80::xxxx:xxxx:xxxx:xxxx/64'
    }
  ]
}

```

<h3 style="color:#99bf9a">Streams</h3>

> - <a style="color:#000000">Streams are objects that let you read data from a source or write data to a destination in a continuous fashion. They're particularly useful for handling large amounts of data efficiently.</a>

```javascript
const fs = require('fs');

// Creating a readable stream
const readableStream = fs.createReadStream('input.txt');

// Creating a writable stream
const writableStream = fs.createWriteStream('output.txt');

// Piping data from readable to writable stream
readableStream.pipe(writableStream);

// Handling 'end' event
readableStream.on('end', () => {
    console.log('File reading complete.');
});

// Handling 'error' event
readableStream.on('error', (err) => {
    console.error('Error:', err);
});

```

<h3 style="color:#99bf9a">Basics of Express.js</h3>

> Use Express.js when building web applications or APIs with Node.js
<br>

> - <a style="color:#000000">Install Express</a>

```javascript
npm install express
```

> - <a style="color:#000000">Basic Express.js setup</a>

```javascript
const express = require('express');
const app = express();

// Define routes and middleware here

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});

```

> - <a style="color:#000000">Routing</a>
> Express allows you to define routes to handle different HTTP methods and URL paths.

```javascript
// Example of handling request for http methods
app.get('/', (req, res) => {
    res.send('Hello, World!');
});

app.post('/users', (req, res) => {
    // Handle POST request to create a new user
});

app.put('/users/:id', (req, res) => {
    // Handle PUT request to update a user by ID
});

app.delete('/users/:id', (req, res) => {
    // Handle DELETE request to delete a user by ID
});

```


<h3 style="color:#99bf9a">Middleware</h3>

> - <a style="color:#000000">Purpose of Middleware</a>
>    - <a style="color:#000000">Pre-processing Requests & Error Handling of incoming requests</a>
>    <br> Can preprocess incoming HTTP requests before they reach the route handlers. This preprocessing might include parsing request bodies, validating authentication tokens, or logging request details.
>    - <a style="color:#000000">Post-processing Responses</a>
>    <br> Can post-process outgoing HTTP responses before they are sent back to the client. This post-processing might include adding headers, compressing response bodies, or formatting data.
>    - <a style="color:#000000">Chain of Responsibility</a>
>    <br> If a middleware function doesn't complete the handling, it can pass control to the next middleware function in the stack.

```javascript
const express = require('express');
const app = express();

// Request Processing Middleware
/* When a request comes in, it first encounters the request processing middleware defined using app.use() */
app.use((req, res, next) => {
    console.log(`[${new Date().toISOString()}] ${req.method} ${req.url}`);
    next(); // Call the next middleware function in the stack
});

// Response Processing Middleware
/* After the request processing middleware, the request encounters the response processing middleware defined using app.use() */
app.use((req, res, next) => {
    // The response processing middleware adds a custom header (X-Custom-Header) to the outgoing response
    res.setHeader('X-Custom-Header', 'Hello from Express');
    next(); // Call the next middleware function in the stack
});

// Chained Middleware Functions
/* Depending on the route specified in the request, the request is then routed to the corresponding middleware function. */

app.get('/', (req, res, next) => {
    // This middleware function handles the '/' route
    res.send('Welcome to the homepage!');
});

app.get('/about', (req, res, next) => {
    // This middleware function handles the '/about' route
    res.send('About Us');
});

/* After the middleware functions have executed, the response is sent back to the client with any modifications made by the middleware.
For example, the response might include the custom header added by the response processing middleware. */

// Error Handling Middleware
/* If an error occurs during the request processing, it can be handled by an error handling middleware defined using app.use() with four parameters (err, req, res, next) */
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send('Internal Server Error');
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});

```

> - <a style="color:#000000">Middleware functions are executed sequentially in the order they are defined. When a request is made to your Express.js application, it passes through each middleware function in the stack, allowing each function to perform its designated tasks.</a>
>
> - <a style="color:#000000">Middleware functions can choose to:</a>
>     - Modify the request (req) object
>     - Modify the response (res) object
>     - End the request-response cycle by sending a request back to the client
>     - Call the next middleware function in the stack using next()

<br>

> - <a style="color:#000000">Request and Response Handling</a>

```javascript
app.get('/users/:id', (req, res) => {
    const userId = req.params.id; // Get parameter from URL
    const queryParams = req.query; // Get query parameters
    const userAgent = req.headers['user-agent']; // Get request header
    // Handle request and send response
});

```

> - <a style="color:#000000">Some examples of built-in Middleware</a>

```javascript
const express = require('express');
const cookieParser = require('cookie-parser');
const app = express();

// Serve static files from the 'public' directory
app.use(express.static('public'));

// Access static files using their relative path from the 'public' directory
// For example, if there's a file named 'styles.css' in 'public/css' directory,
// it can be accessed at '/css/styles.css'

// Parse JSON-encoded request bodies
// JSON data can be sent as the body of a POST request, for example, when submitting a form on a website
app.use(express.json());

// example of json encoded request body: { "name": "John Doe", "age": 30, "email": "john@example.com" }

// Route to handle POST requests
app.post('/api/data', (req, res) => {
    console.log(req.body); // Access parsed JSON data from request body
    res.send('Data received successfully');
});

// Parse URL-encoded request bodies
app.use(express.urlencoded({ extended: true }));
// example of url encoded request body: name=John+Doe&age=30&email=john%40example.com

// Route to handle POST requests
app.post('/submit-form', (req, res) => {
    // Access parsed URL-encoded data from request body
    const name = req.body.name;
    const age = req.body.age;
    const email = req.body.email;

    // Perform actions with the parsed data
    console.log('Name:', name);
    console.log('Age:', age);
    console.log('Email:', email);

    // Send response back to the client
    res.send('Form submitted successfully');
});

// Parse cookies attached to the request
app.use(cookieParser());

/* When a client sends an HTTP request to a server,
it includes any relevant cookies in the request headers.
The server can then access and process these cookies to maintain session state,
personalize content, or perform other tasks as needed. */

// Route to handle incoming requests
app.get('/', (req, res) => {
    // Access parsed cookies from the request object
    const name = req.cookies.name;
    const age = req.cookies.age;
    const sessionID = req.cookies.sessionID;

    // Perform actions with the parsed cookies
    console.log('Name:', name);
    console.log('Age:', age);
    console.log('Session ID:', sessionID);

    // Send response back to the client
    res.send('Cookies parsed successfully');
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});

```

> Express.js uses a middleware architecture that allows you to modularize your application's functionality into small, reusable components called middleware functions. These functions can be added to the request-response pipeline to perform tasks such as logging, authentication, authorization, request parsing, error handling, and more.

<br>

<h3 style="color:#99bf9a">RESTful API</h3>

> - <a style="color:#000000">RESTful APIs are stateless. This means each request from a user contains all the information needed for the server to fulfill it. The server doesn't keep track of previous requests or interactions.</a>
>
> Imagine you have a friend who wants to borrow a toy from your toy box (resource / database). They ask nicely (a request) for a toy by its name (URI), you decide if they can borrow it (server processes the request), and you give them the toy (server sends a response). This back-and-forth interaction between your friend (client) and you (server) is similar to how RESTful APIs work.
>
> <br> Actions: You can do different things with toys, like play, share, or organize them. Similarly, in a RESTful API, we can perform actions on resources using HTTP methods: GET, PUT, PATCH, POST, DELETE. The HTTP method is sent in part with the request, not in URI.
>

<br>

> - <a style="color:#000000">Status Codes</a>
> <br> HTTP methods define the actions that clients can perform on resources, while status codes indicate the outcome of a request.
>
>     - <a style="color:#000000">2xx: Success codes indicating that the request was successful</a>
>         - <a style="color:#000000">200 OK: Successful GET request</a>
>         - <a style="color:#000000">201 Created: Successful POST request resulting in the creation of a new resource</a>
>
>     - <a style="color:#000000">3xx: Redirection codes indicating that further action is required to complete the request</a>
>
>     - <a style="color:#000000">4xx: Client error codes indicating that the client's request cannot be fulfilled</a>
>         - <a style="color:#000000">400 Bad Request: Malformed request syntax or invalid request message</a>
>         - <a style="color:#000000">404 Not Found: Resource not found on the server</a>
>
>     - <a style="color:#000000">5xx: Server error codes indicating that the server failed to fulfill a valid request</a>


```javascript
const express = require('express');
const app = express();

/* Each route corresponds to a specific HTTP method and performs the necessary logic (e.g., database operations) */

// Define route for retrieving all users
app.get('/users', (req, res) => {
    // Logic to retrieve all users from the database
    res.json({ users: [...] }); // Send JSON response with users
});

// Define route for creating a new user
app.post('/users', (req, res) => {
    // Logic to create a new user in the database
    res.status(201).json({ message: 'User created successfully' });
});

// Define route for updating a user
app.put('/users/:id', (req, res) => {
    const userId = req.params.id;
    // Logic to update the user with the specified ID in the database

    /* We use res.json() to send JSON responses and res.status() to set the HTTP status code */
    res.json({ message: `User with ID ${userId} updated successfully` });
});

// Define route for deleting a user
app.delete('/users/:id', (req, res) => {
    const userId = req.params.id;
    // Logic to delete the user with the specified ID from the database
    res.json({ message: `User with ID ${userId} deleted successfully` });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});

```

<br>

<h3 style="color:#99bf9a">Data Validation & Sanitization</h3>

> - <a style="color:#000000">Validation</a>
> <br> Validation involves ensuring that input data meets specific criteria or constraints. For example, validating that an email address is in the correct format, or that a password meets certain complexity requirements.
>
> - <a style="color:#000000">Sanitization</a>
> <br> Sanitization involves cleaning or filtering input data to remove potentially harmful or unwanted content. For example, removing HTML tags from user input to prevent cross-site scripting (XSS) attacks, or trimming whitespace from strings.

<br>

> Utilizing validation libraries like Joi or express-validator can streamline the validation process by providing a robust set of validation rules and functions.

<h4 style="color:#99bf9a">Joi</h4>

```javascript
const express = require('express');
const Joi = require('joi');

const app = express();

// Middleware for parsing JSON request bodies
app.use(express.json());

// Validation schema using Joi
const userSchema = Joi.object({
    username: Joi.string().alphanum().min(3).max(30).required(),
    email: Joi.string().email().required(),
    password: Joi.string().pattern(new RegExp('^[a-zA-Z0-9]{3,30}$')).required(),
});

// Route for handling POST requests to '/signup'
app.post('/signup', (req, res) => {
    // Validate request body against schema
    const { error, value } = userSchema.validate(req.body);

    // Check for validation errors
    if (error) {
        return res.status(400).json({ error: error.details[0].message });
    }

    // If validation passes, process the data
    const { username, email, password } = value;
    // Further processing logic...
    
    res.send('User registered successfully');
});

// Start the server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});

```

<h4 style="color:#99bf9a">express-validator</h4>

```javascript
const express = require('express');
const { body, validationResult } = require('express-validator');

const app = express();

// Middleware for parsing JSON request bodies
app.use(express.json());

// Route for handling POST requests to '/signup'
app.post('/signup', [
    // Validate email field
    body('email').isEmail().normalizeEmail(),
    // Validate password field
    body('password').isLength({ min: 6 }),
], (req, res) => {
    // Check for validation errors
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
        return res.status(400).json({ errors: errors.array() });
    }

    // If validation passes, process the data
    const { email, password } = req.body;
    // Further processing logic...
    
    res.send('User registered successfully');
});

// Start the server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});

```






















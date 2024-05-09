<h1 style="color:#a2ff00">Node.js</h1>

> - <a style="color:#000000">Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It allows you to run JavaScript code on the server-side.</a>

<h3 style="color:#a2ff00">Installation</h3>

> - <a style="color:#000000">Download from official website and check if node and npm are installed with what commands?</a>
> <br> A: node -v ; npm -v

<h3 style="color:#a2ff00">Basic Node.js App</h3>

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

<h3 style="color:#a2ff00">Core Node.js Modules</h3>

<h4 style="color:#a2ff00">File System (fs) - Interacting with file system on your computer</h4>

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

<h4 style="color:#a2ff00">HTTP - To create HTTP servers and make HTTP requests</h4>

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

<h4 style="color:#a2ff00">Paths - Handling file paths in a cross-platform way</h4>

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

<h4 style="color:#a2ff00">Operating System - To gather information about the operating system</h4>

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

<h3 style="color:#a2ff00">Streams</h3>

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














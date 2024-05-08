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

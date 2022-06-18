<h1 align="center">Node.js</h1>

<div align="center">
  <img src="https://github.com/ksalokya/node.js_modules/blob/main/nodejs.gif" width="400px"/>
</div>

## OS Module

```js
const os = require('os');

// current user info
const user = os.userInfo();
console.log(user);

// system uptime
const uptime = os.uptime();
console.log(uptime)

// OS info
const currentOs = {
    name : os.type(),
    release : os.release(),
    version : os.version(),
    cpu  : os.cpus(),
    totalMemory : os.totalmem(),
    freeMemory : os.freemem()
}
console.log(currentOs)
```

## Path Module

```js
const path = require('path');

// returns the last portion of a path
const last = path.basename("/foo/bar/index.html");
console.log(last)

// returns the directory name of a path
const dir = path.dirname("/foo/bar/index.html");
console.log(dir)

//  returns the extension of the path
const ext = path.extname("/foo/bar/index.html");
console.log(ext)

// Provides the platform-specific path segment separator
const sep = path.sep;
console.log(sep)

// joins all given path segments together
const filePath = path.join('untitled','temp.txt');
console.log(filePath)

// resolves a sequence of paths or path segments into an absolute path
const absolute = path.resolve(__dirname, 'untitled','temp.txt');
console.log(absolute)
```


## File System Module (Sync)

```js
const {readFileSync, writeFileSync} = require('fs');

// read file
const myFile = readFileSync('./temp.txt', 'utf8');
console.log(myFile)

// write into file
writeFileSync('./temp.txt', 'Hello World!')
console.log(myFile)
```

## File System Module (Async)

```js
const {readFile, writeFile} = require('fs');

// read file
readFile('./temp.txt', 'utf8', (err, result) => {
    if (err) {
        console.log("Error");
    } else {
        console.log(result);

        // write into file
        writeFile('./temp.txt', 'Hello World...', (err) => {
            if (err) {
                console.log(err)
            } else {
                readFile('./temp.txt', 'utf8', (err, result) => {
                    console.log(result)
                })
            }
        })
    }
});
```

## HTTP

```js
const http = require('http');

const server = http.createServer((req, res) => {
    if (req.url === '/') {
        res.end("Welcome to Home");
    }
    else if(req.url === '/about'){
        res.end("Welcome to About");
    }
    else{
        res.end("Oops!");
    }
});

server.listen(5000)
```

## Async Patterns

```js
const {readFile} = require("fs");

const getText = (path) => {
    return new Promise((resolve, reject) => {
        readFile(path, 'utf8', (err, data) => {
            if (err)
                reject(err)
            else
                resolve(data)
        });
    });
};

// Using nested callbacks
getText("./temp.txt")
    .then((res) => { console.log(res); })
    .catch((err) => { console.log(err); });

// Using async await
const start = async () => {
    try{
        const first = await getText("./temp.txt");
        console.log(first)
    } catch (error){
        console.log(error.message)
    }
}

start();
```

## Middleware

```js
const express = require("express");

const port = process.env.PORT || 5000;
const app = express();

// req => middleware => res
const logger = (req, res, next) => {
    const method = req.method;
    const url = req.url;
    const time = new Date().getFullYear();
    console.log(method, url, time);

    next();
}

app.get('/', logger, (req, res) => {
    res.send("Home");
})

app.get('/about', logger, (req, res) => {
        res.send("About");
    }
)

app.listen(port, function () {
    console.log(`Serve at http://localhost:${port}`);
});
```

## app.use

```js
const logger = (req, res, next) => {
    const method = req.method;
    const url = req.url;
    const time = new Date().getFullYear();
    console.log(method, url, time);

    next();
}

module.exports = logger
```

```js
const express = require("express");

const port = process.env.PORT || 5000;
const app = express();

const logger = require('./logger')

// applies to all routes
app.use(logger)

// applies to routes starting with /about
app.use('/about', logger)

app.get('/', (req, res) => {
    res.send("Home");
})

app.get('/about', (req, res) => {
    res.send("About");
})

app.get('/about/prod', (req, res) => {
    res.send("About Product");
})

app.listen(port, function () {
    console.log(`Serve at http://localhost:${port}`);
});
```

## Multiple Middlewares

```js
const express = require("express");

const port = process.env.PORT || 5000;
const app = express();

const logger = require('./logger')
const authorize = require('./authorize')

// multiple middlewares
// executes sequentially
app.use([logger, authorize])

app.get('/', (req, res) => {
    res.send("Home");
})

app.listen(port, function () {
    console.log(`Serve at http://localhost:${port}`);
});
```

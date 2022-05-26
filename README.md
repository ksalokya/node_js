# node.js_modules

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


## Path Module (Sync)

```js
const {readFileSync, writeFileSync} = require('fs');

// read file
const myFile = readFileSync('./temp.txt', 'utf8');
console.log(myFile)

// write into file
writeFileSync('./temp.txt', 'Hello World!')
console.log(myFile)

```




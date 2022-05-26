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

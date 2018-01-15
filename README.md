# Config-Envify
Some of the older nodejs config management packages do not support
overwriting via environmental variables.

## How to use
Just include (will make npm package soon) the file in your lib and use it inside your config file. Example:

```
const envify = require('./config-envify');

module.exports = envify.envify({
  // Your normal config
});
```

## How it works
 It wraps your current config without effecting its values. When you run your application, it checkes env variables and convert your current configs to env friendly variables (Uppercased Underscored). It loops over your config and see if it finds any similar key in `process.env`. If found, will update it and if not, will skip.


## Specification
This module, accepts an object and trys to match keys inside it with
environmental variables. So if our object contains `{myKey: 'my value'}`
It looks for `MYKEY` in env variables and if found, it overwrites the value
of that env variable with our object's key.
It also has supoort for nested variables and arrays:
`{myKey: {mySecondKey: 'my value'}} => MYKEY_MYSECONDKEY='my value'`
`{myKey: ['val1', 'val2']} => MYKEY_0='val1' MYKEY_1='val2'`
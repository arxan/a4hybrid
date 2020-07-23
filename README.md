# Arxan for Hybrid Installation Manager

Integrate Arxan protection into your npm or webpack workflow.

## Prerequisites

Before you can install or use this package, you must:

1. Be a current Arxan customer.
2. Review the platform requirements in the most recent version of the *Arxan for Hybrid* online help, which is available from Arxan.
3. Obtain an API Key, API Secret, and License Token from Arxan.
    * Make sure the API Key has the "Product download" checkbox checked.
4. Add the following environment variables:

```
A4HYBRID_API_KEY="myapikey"
A4HYBRID_API_SECRET="mysecret"
A4HYBRID_LICENSE_TOKEN="mylicensetoken"
```

**NOTE:** This package should not be installed globally.

## Protect

This package offers production-ready essential protection that quickly and automatically adds additional security and tamper detection to your code without any manual configuration.

To run protection, add the following code at the end of your build:

```
const {protect} = require('a4hybrid');
const blueprint = {
    targets: {
        main: {
            "input": "./dist",
            "outputDirectory": "./dist_protected"
        }
    }
}
protect(blueprint).then((output) => {
    console.log(output.stdout);
    console.error(output.stderr);
}).catch((err) => {
    console.error(err.message);
});
```

Notice the object called `blueprint`. To apply essential protection, you only need to modify the values of `"input"` and `"outputDirectory"`, where `"./dist"` is the directory that contains your input files and `"./dist_protected"` is the directory where the final protected files will appear.

However, you can further customize your protection by modifying the `blueprint` object. For instructions, see the *Arxan for Hybrid* online help, which is available from Arxan.


### Protect with Webpack

To run protection within a webpack bundle, add the protection code to `webpack.config.js`.

This example applies essential protection:

```
const {WebpackPlugin} = require('a4hybrid');
module.exports = {
    plugins : [
        new WebpackPlugin()
    ]
}
```

This example uses a blueprint. If you leave the code as is, it will apply essential protection. However, you can also modify the blueprint as described previously:

```
const {WebpackPlugin} = require('a4hybrid');
const blueprint = {
    guardConfigurations: {
        config : {
            "debugDetection": {
                "disable": true
            }
        }
    }
}
module.exports = {
    plugins : [
        new WebpackPlugin(blueprint)
    ]
}
```

To see the protection summary, add the ```stats``` field, as follows:

```
const {WebpackPlugin} = require('a4hybrid');
module.exports = {
    stats: {
        logging: 'log'
    },
    plugins : [
        new WebpackPlugin()
    ]
}
```

You can set the following values for ```logging```:
- none - disable logging
- log - displays errors, warnings, info messages, and log messages

## Learn More

Visit www.arxan.com to learn more about Arxan's protection solutions.

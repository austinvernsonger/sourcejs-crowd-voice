Crowd Voice
===============

[![Gitter chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/sourcejs/Source)

Crowd Voice [SourceJS](http://sourcejs.com) plugin for adding user custom info on spec page from browser.

![Crowd Voice](https://monosnap.com/image/5Kh7zC879twOFA0Q8YzqcsDKnHvwIZ.png)

___

To install, run npm in `sourcejs/user` folder:

```
npm install sourcejs-crowd-voice --save
```

Then run Grunt update in SourceJS root:

```
cd sourcejs
grunt update
```

After installation, all your Specs pages will have "Add description" tumbler in inner menu, that will active the plugin.

## Dependencies

### MongoDB

As [MongoDB](http://www.mongodb.org/) is not essential dependency for SourceJS, you must install it separately, to work with plugins that expect data storage.

[Install it](http://docs.mongodb.org/manual/installation/), run locally or remotely and configure your SourceJS in `sourcejs/user/options.js`:

```json
core: {
  "production": {
    "host": "localhost",
    "dbName": "sourcejs"
  }
}
```

Host could point to remote service. Database name could be custom as well.

#### Connect to DB from app

Then prepare `mongoose` dependency - as it must be common for every plugins, install it in `sourcejs/user`

```
npm install mongoose --save
```

And edit `/sourcejs/user/core/app.js`, that extends main SourceJS application. Just add this code snippet, for connection to database:

```js
/* Connect to DB */
var mongoose = require('mongoose');

var dbAdress = 'mongodb://' + global.opts.core.production.host + '/' + global.opts.core.production.dbName;

mongoose.connection.on("connecting", function() {
    return console.log("Started connection on " + (dbAdress).cyan + ", waiting for it to open...".grey);
});
mongoose.connection.on("open", function() {
    return console.log("MongoDB connection opened!".green);
});
mongoose.connection.on("error", function(err) {
    console.log("Could not connect to mongo server!".red);
    return console.log(err.message.red);
});

mongoose.connect(dbAdress);
/* /Connect to DB */
```

## Updates

**0.3.0** release:
 - markdown syntax support based on [Pagedown converter](https://code.google.com/p/pagedown/);
 - migration from CouchDB to MongoDB;
 - some design improvements

___

Compatible with SourceJS v0.4+, for v0.3.* use [previous release](https://github.com/sourcejs/sourcejs-crowd-voice/archive/v0.1.0.zip).

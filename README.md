# levelup database adapter for [Yjs](https://github.com/y-js/yjs)

Use the levelup database adapter to store your shared data persistently in NodeJs applications. The changes will persist after restart.

## Works with any levelup backend.  

For more info see:

* https://github.com/Level/levelup/wiki/Modules#storage
* https://github.com/Level/awesome

## How it works

This is a fork of y-leveldb, which uses leveldown to store data in the filesystem.

In order to support remote databases via levelup, a couple of changes have been made:

* Rather than creating a DB per room, use a single database for all rooms and implement rooms as sublevels.
* For optimal room startup, run the OS as an in-memory database whose operations are also streamed to the remote database.

### Caveats

* This was an experiment that has turned out to work pretty well.
* so YMMV.
* This is just source code adapted from its original app. 
* I haven't worked out the YJS build system yet so there is no dist or NPM package.
* SS and DS are not run in-memory as OS is.  It might be worth exploring.

## Example

### 1.  Create/connect to levelup root database
```
var db = require('levelup')(process.env.MONGODB_URI || 'localhost/yjs-rooms', { db: require('mongodown') })
```

### 2.  Initialize y-levelup with database
```
require('y-levelup')(Y, db)
```

### 3.  Create Y instance
```
Y({
  db: {
    name: 'levelup',
    namespace: 'textarea-example' (optional - defaults to connector.room),
  },
  connector: {
    name: 'websockets-client', // use the websockets connector
    room: 'textarea-example'
  },
  share: {
    textarea: 'Text' // y.share.textarea is of type Y.Text
  }
}).then(function (y) {
  // bind the textarea to a shared text element
  y.share.textarea.bind(document.getElementById('textfield'))
}
```

## License
Yjs is licensed under the [MIT License](./LICENSE).

<kevin.jahns@rwth-aachen.de>
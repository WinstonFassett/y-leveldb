# LevelUp database adapter for [Yjs](https://github.com/y-js/yjs)

Use the levelup database adapter to store your shared data persistently in NodeJs applications. The changes will persist after restart.

Works with any LevelUp backend
https://github.com/Level/levelup/wiki/Modules#storage
https://github.com/Level/awesome


### Example

```

// create levelup root database
var db = require('levelup')(process.env.MONGODB_URI || 'localhost/yjs-rooms', { db: require('mongodown') })
// initialize y-levelup
require('y-levelup')(Y, db)

// create Y instance
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
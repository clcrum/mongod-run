# mongod-run2
Simplifies running mongod within MEAN / Express projects. It can also be useful when testing APIs.

This is a fork of [gtramontina/mongod-run](https://github.com/gtramontina/mongod-run) where all the real work was done. Unfortunately, there were some changes in Node 7.x that broke the original package.

## Express Example

```javascript
var mongodRun2 = require('mongod-run2');

if(!isProduction) {
  mongodRun2.start(() => {
    this.doAfterMongoStart();
  })
}
else {
  this.doAfterMongoStart();
}
```

## Testing Example

```javascript
var mongod = require('mongod-run');

before(mongod.start);
after(mongod.stop);
afterEach(mongod.cleanup('mongodb://localhost:27017/example.test'));

describe('my app', function () {
  // ...
});
```

## API
* `start(callback)`: runs mongod and call the callback once it is up and running.
* `stop()`: kills the mongod process. This is automatically called if/when the test process exits.
* `cleanup(url)`: performs a cleanup on the database specified by the given url.

## Notes
The `mongod` process is being ran with the following command:
```bash
$ mongod -f --rest
```

## License
This is licensed under the feel-free-to-do-whatever-you-want-to-do license – [http://unlicense.org](http://unlicense.org)

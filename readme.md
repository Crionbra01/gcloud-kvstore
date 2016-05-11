# gcloud-kvstore
> Use Datastore as a Key/Value store.


## Install
```sh
$ npm install --save gcloud-kvstore
```


## Example
```js
var kvstore = require('gcloud-kvstore');
var gcloud = require('gcloud')(/*...*/);
var datastore = gcloud.datastore();

var store = kvstore(datastore);

// Set an item.
store.set('todos', ['eat', 'sleep', 'repeat'], function(err, key) {});

// Get an item.
store.get('todos', function(err, todos) {
  // todos:
  //   ['eat', 'sleep', 'repeat']
});

// Delete an item.
store.delete('todos', function(err) {});
```


## How
[Google Cloud Datastore](https://cloud.google.com/datastore) is a managed, NoSQL, schemaless database for storing non-relational data. Datastore [entities](https://cloud.google.com/datastore/docs/concepts/entities) are complex objects. However, we can wrap this complexity to mimic a simple key/value store by storing a numeric or string "key" as the id of an entity.

The example below shows the complexity that is hidden with `gcloud-kvstore`.

#### With `gcloud-node`:
```js
var key = datastore.key(['KeyValue', 'key']);

datastore.save({
  key: key,
  value: 'value'
}, function() {});

datastore.get(key, function() {});

datastore.delete(key, function() {});
```

#### With `gcloud-node` + `gcloud-kvstore`:
```js
var store = require('gcloud-kvstore')(datastore);

store.set('key', 'value', function() {});

store.get('key', function() {});

store.delete('key', function() {});
```


## API

### kvstore(datastore)

#### datastore

A gcloud-node [Datastore](http://googlecloudplatform.github.io/gcloud-node/#/docs/master/datastore) instance.

### kvstore#delete(key, callback)

#### key
Type: `String|Number`

#### callback
Type: `Function`
Executed with the same signature as [Datastore#delete](http://googlecloudplatform.github.io/gcloud-node/#/docs/master/datastore?method=delete).

### kvstore#get(key, callback)

#### key
Type: `String|Number`

#### callback
Type: `Function`
Executed with (`err`, `value`)

### kvstore#set(key, value, callback)

#### key
Type: `String|Number`

#### value
Type: `*`

#### callback
Type: `Function`
Executed with the same signature as [Datastore#save](http://googlecloudplatform.github.io/gcloud-node/#/docs/master/datastore?method=save).


## Credit

Concept originally created by [Patrick Costello](https://github.com/pcostell): https://github.com/GoogleCloudPlatform/gcloud-node/issues/256#issuecomment-58962323.


## License

MIT © Stephen Sawchuk

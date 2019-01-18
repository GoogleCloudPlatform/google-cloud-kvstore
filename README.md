# google-cloud-kvstore
> Use Datastore as a Key/Value store.


## Install
```sh
$ npm install google-cloud-kvstore
```

## Example
```js
const {KVStore} = require('google-cloud-kvstore');
const {Datastore} = require('@google-cloud/datastore');

const datastore = new Datastore();
const store = new KVStore(datastore);

// Set an item.
store.set('todos', ['eat', 'sleep', 'repeat'], (err, key) => {});

// Get an item.
store.get('todos', (err, todos) => {
  // todos:
  //   ['eat', 'sleep', 'repeat']
});

// Delete an item.
store.delete('todos', (err) => {});
```


## How
[Google Cloud Datastore](https://cloud.google.com/datastore) is a managed, NoSQL, schemaless database for storing non-relational data. Datastore [entities](https://cloud.google.com/datastore/docs/concepts/entities) are complex objects. However, we can wrap this complexity to mimic a simple key/value store by storing a numeric or string "key" as the id of an entity.

The example below shows the complexity that is hidden with `google-cloud-kvstore`.

#### With `@google-cloud/datastore`:
```js
const key = datastore.key(['KeyValue', 'key']);

datastore.save({
  key: key,
  value: 'value'
}, () => {});

datastore.get(key, () => {});

datastore.delete(key, () => {});
```

#### With `@google-cloud/datastore` + `google-cloud-kvstore`:
```js
const {KVStore} = require('google-cloud-kvstore');
const store = new KVStore(datastore);
store.set('key', 'value', () => {});
store.get('key', () => {});
store.delete('key', () => {});
```

## API

### kvstore(datastore)

#### datastore

A [@google-cloud/datastore](https://cloud.google.com/nodejs/docs/reference/datastore/latest/Datastore) instance.

### kvstore#delete(key, callback)

#### key
Type: `String|Number`

#### callback
Type: `Function`
Executed with the same signature as [Datastore#delete](https://cloud.google.com/nodejs/docs/reference/datastore/latest/Datastore#delete).

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
Executed with the same signature as [Datastore#save](https://cloud.google.com/nodejs/docs/reference/datastore/latest/Datastore#save).


## Credit
Concept originally created by [Patrick Costello](https://github.com/pcostell): https://github.com/GoogleCloudPlatform/google-cloud-node/issues/256#issuecomment-58962323.

## License
MIT

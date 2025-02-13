# The Evolution of the Asynchronous Programming

## Convert Callbacks to Promises to Generator to async/await

### Callbacks

The function itself

```javascript
function getData(callback, errorCallback) {
  try {
    // Do some network/api stuff...
    callback("https://api.fake.data"/*Data Source here*/)
  } catch (e) {
    errorCallback(e);
  }
}

// Here is how you would use it:
getData(result => console.log(result/*?*/), error => console.error(error));
```

### Promise

Here is how to create a Promise-based function from it:

```javascript
function getDataAsync() {
  return new Promise((resolve, reject) => {
    getData(resolve, reject);
  });
}

getDataAsync("https://api.fake.data"/*Data Source here*/)
  // use `then` to call callback function
  .then(result => console.log(result))
  // use `catch` to call error function
  .catch(error => console.error(error));
```

### Generator

Return value as a iterator

```javascript
const generator = function* () {
  const result = yield getDataAsync();
}
const runG = generator()
runG.next();
```

### Async/Await

Return a promised based object

```javascript
const asyncAwait = async function () {
  const result = await getDataAsync();
}

const runAA = asyncAwait() .
```

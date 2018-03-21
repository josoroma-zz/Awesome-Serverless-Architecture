# Node.JS Best Practices

- https://github.com/i0natan/nodebestpractices

## Microservices architecture / Components

- https://github.com/i0natan/nodebestpractices/blob/master/sections/projectstructre/breakintcomponents.md

Divide the whole stack into self-contained components that don't share files with others, each constitutes very few files (e.g. API, service, data access, test, etc.) so that it's very easy to reason about it. Some may call this 'microservices' architecture — it's important to understand that microservices is not a spec which we must follow, but rather a set of principles. We may adopt many principles into a full-blown microservices architecture or adopt only few. Both are good as long as you keep the software complexity low.

The very least we should do is create basic borders between components, assign a folder in our project root for each business component and make it self contained - other components are allowed to consume its functionality only through its public interface or API.

This is the foundation for keeping your components simple, avoid dependency hell and pave the way to full-blown microservices in the future once your app grows.

## Structure your solution by components

- https://github.com/i0natan/nodebestpractices/blob/master/sections/projectstructre/thincomponents.md

```
- components
  - orders
  - products
  - users
    - index.js
    - user.js
    - usersAPI.js
    - usersController.js
    - usersDAL.js
    - usersErrors.js
    - usersService.js
    - userTesting.js
- lib
```

## Layers

Separate component code into layers:

- Web

- Services

- DAL (Data Access Layer) and more.

- https://github.com/i0natan/nodebestpractices/blob/master/sections/projectstructre/createlayers.md

**Business logic and DAL:**

- https://raw.githubusercontent.com/i0natan/nodebestpractices/master/assets/images/keepexpressinweb.gif

**Issue:**

API passes `Express` objects to DAL and logic layers:

```
const express = require('express');
const util = require('util');
const router = express.Router();
const usersDBAccess = require('./usersDAL'); // Data Access Layer.

router.get('/', (req, res, next) => {
  userDBAccess.getByID(req);
});

module.exports = router;
```

The entire system becomes dependant and accesible only by `Express`:

```
class UserDAL {
  // Data access layer, expects an Express object.
  getByID(req) {
    if (req.user.roles) {
      this.invokeAnotherFunction(req);
    }
  }

  invokeAnotherFunction(req) {
    // Do something.
  }
}
```

**Solution:**

Keep Express in the Web Layer. Just create and pass a custom `Context Object`:

```
const express = require('express');
const util = require('util');
const router = express.Router();
const usersService = require('./usersService');
const usersDBAccess = require('./usersDAL'); // Data Access Layer.
const logger = require('logger');

router.get('/', (req, res, next) => {
  const contextObject = {
    user: req.user,
    transactionId: UUID.new(),
    otherProperties: 'Some other properties'
  };

  new DAL(contextObject);

  userDBAccess.getByID(1);
});

module.exports = router;
```

## Use environment aware, secure and hirearchical config

- https://github.com/i0natan/nodebestpractices/blob/master/sections/projectstructre/configguide.md

Hirearchical config helps to find entries and maintain huge config files, for example:

```
{
  // Customer module configs 
  "Customer": {
    "dbConfig": {
      "host": "localhost",
      "port": 5984,
      "dbName": "customers"
    },
    "credit": {
      "initialLimit": 100,
      // Set low for development 
      "initialDays": 1
    }
  }
}
```

## Separate Express 'app' and 'server'

- https://github.com/i0natan/nodebestpractices/blob/master/sections/projectstructre/separateexpress.md

The latest Express generator comes with a great practice that is worth to keep - the API declaration is separated from the network related configuration (port, protocol, etc). This allows testing the API in-process, without performing network calls, with all the benefits that it brings to the table: fast testing execution and getting coverage metrics of the code. It also allows deploying the same API under flexible and different network conditions. Bonus: better separation of concerns and cleaner code.

Test the API in-process using supertest (popular testing package).

- https://github.com/visionmedia/supertest

```
const request = require('supertest');
const express = require('express');

const app = express();

app.get('/user', function(req, res) {
  res.status(200).json({ name: 'tobi' });
});

request(app)
  .get('/user')
  .expect('Content-Type', /json/)
  .expect('Content-Length', '15')
  .expect(200)
  .end(function(err, res) {
    if (err) throw err;
  });
```

Here's an example with `mocha`, note how you can pass done straight to any of the `.expect()` calls:

```
describe('GET /user', function() {
  it('respond with json', function(done) {
    request(app)
      .get('/user')
      .set('Accept', 'application/json')
      .expect('Content-Type', /json/)
      .expect(200, done);
  });
});
```

## Wrap common utilities as NPM packages

Now, all your code base can import that code and benefit free dependency management tool. It's possible to publish NPM packages for your own private use without sharing it publicly using private modules, private registry or local NPM packages.

- https://github.com/i0natan/nodebestpractices/blob/master/sections/projectstructre/wraputilities.md
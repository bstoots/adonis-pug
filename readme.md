# adonis-pug

[Pug](https://github.com/pugjs/pug) templating provider for AdonisJs framework.

## Installation

In order to use adonis-pug

```
npm install adonis-pug --save
```

## Setup

Once you have installed the provider from the [npm](https://npmjs.org/packages/adonis-pug), make sure to follow these steps to setup the provider.

##### bootstrap/app.js

```javascript
const providers = [
  ...,
  'adonis-pug/providers/PugProvider'
]
```

Also, set up an alias to avoid typing the complete namespace.

##### bootstrap/app.js
```javascript
const aliases = {
  ...,
  Pug: 'Adonis/Addons/Pug'
}
```

## Config

Pug options can be added to `config.app.js`:

```javascript
  ...,
  pug: {
    basedir: 'resources/views',
    pretty: false,
    doctype: undefined,
    filters: undefined,
    self: false,
    debug: false
    inject: {
      moment: use('moment')
    }
  }
```

### Injection

You can add variables into pug globally using the inject object (see above)

## Middleware (Shield and Flash)

Methods and variables from the Adonis Shield and Flash middleware can be injected as pug variables by registering this module as middleware in `app/Http/kernel.js`:

```javascript
const globalMiddleware = [
  ...,
  'Adonis/Addons/Pug'
]
```

The available methods/variables are `flashMessages`, `old()`, `cspNonce` and `csrfToken`. The Flash and Shield middleware must also be enabled and loaded before Adonis-pug. Also the `Config.get()` method is also available as `config()` and `request.input()` is available as `input()`.

## Usage

##### Send a rendered pug template as a response
`use('Pug')` must be inserted somewhere to add the pug method to the response object. A good place for this is in `bootstrap/http.js`

```javascript
Route.get('/', function * (request, response) {
  response.pug('myPugTemplate', {
    message: 'Hello World'
  });
});
```

##### Output html from a rendered pug string
```javascript
const Pug = use('Pug')
Pug.renderString('p Hello World', options)
```

##### Output html from a rendered pug template
```javascript
const Pug = use('Pug')
Pug.render('myPugTemplate', {
  message: 'Hello World'
})
```

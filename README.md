# Fluxible

[![npm version](https://badge.fury.io/js/fluxible.svg)](http://badge.fury.io/js/fluxible)
[![Build Status](https://travis-ci.org/yahoo/fluxible.svg?branch=master)](https://travis-ci.org/yahoo/fluxible)
[![Dependency Status](https://david-dm.org/yahoo/fluxible.svg)](https://david-dm.org/yahoo/fluxible)
[![devDependency Status](https://david-dm.org/yahoo/fluxible/dev-status.svg)](https://david-dm.org/yahoo/fluxible#info=devDependencies)
[![Coverage Status](https://coveralls.io/repos/yahoo/fluxible/badge.png?branch=master)](https://coveralls.io/r/yahoo/fluxible?branch=master)

Pluggable, singleton-free container for isomorphic [flux](https://github.com/facebook/flux) applications.

[![Gitter chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/yahoo/fluxible)

## Install

`npm install --save fluxible`

## Usage

```js
var Fluxible = require('fluxible');
var fluxibleApp = new Fluxible({
    component: React.createFactory(require('./components/App.jsx'))
})
```

For each request:

```js
var context = fluxibleApp.createContext();
context.executeAction(action, payload, function () {
    var markup = React.renderToString(context.createElement());
    var state = fluxibleApp.dehydrate(context);

    // ... send markup and state to the client ...
});
```

For a more extensive example of usage both on the server and the client, see [flux-examples](https://github.com/yahoo/flux-examples).

### Dehydration/Rehydration

Fluxible uses reserved methods throughout called `rehydrate` and `dehydrate` which are responsible for taking a snapshot of server-side state so that it can be sent to the browser and rehydrated back to the same state in the browser.

There are two kinds of state within Fluxible:

 * **Application State**: Settings and data that are registered on server start
 * **Context State**: Settings and data that are created per context/request

Application level rehydrate method is allowed asynchronous operation in case it needs to load JavaScript or data on demand.


## APIs

- [Fluxible](https://github.com/yahoo/fluxible/blob/master/docs/api/Fluxible.md)
- [FluxibleContext](https://github.com/yahoo/fluxible/blob/master/docs/api/FluxibleContext.md)


## License

This software is free to use under the Yahoo Inc. BSD license.
See the [LICENSE file][] for license text and copyright information.

[LICENSE file]: https://github.com/yahoo/fluxible/blob/master/LICENSE.md

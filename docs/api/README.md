# Documentation

var Fluxible = require('fluxible') exports the following:

 * [`Fluxible`](https://github.com/yahoo/fluxible/blob/master/docs/api/Fluxible.md)
 * [`Fluxible.FluxibleComponent`](https://github.com/yahoo/fluxible/blob/master/docs/api/FluxibleComponent.md)
 * [`Fluxible.FluxibleMixin`](https://github.com/yahoo/fluxible/blob/master/docs/api/FluxibleMixin.md)


or if you're using ES6:

```js
import {Fluxible, FluxibleComponent, FluxibleMixin} from 'fluxible';
```

## Addons

`var FluxibleAddons = require('fluxible/addons')` also provides helper utilities for creating stores:

 * [`FluxibleAddons.BaseStore`](https://github.com/yahoo/fluxible/blob/master/docs/api/Stores.md#BaseStore)
 * [`FluxibleAddons.createStore`](https://github.com/yahoo/fluxible/blob/master/docs/api/Stores.md#createStore)

 or if you're using ES6:

 ```js
 import {BaseStore, createStore} from 'fluxible/addons';
 ```

 These libraries are not bundled with the main Fluxible export because stores are classes that are decoupled from Fluxible entirely.

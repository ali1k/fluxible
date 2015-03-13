# Documentation

`var Fluxible = require('fluxible')`` exports the following:

 * [`Fluxible`](Fluxible.md)
 * [`Fluxible.FluxibleComponent`](FluxibleComponent.md)
 * [`Fluxible.FluxibleMixin`](FluxibleMixin.md)


or if you're using ES6:

```js
import {Fluxible, FluxibleComponent, FluxibleMixin} from 'fluxible';
```

## Addons

`var FluxibleAddons = require('fluxible/addons')` also provides helper utilities for creating stores:

 * [`FluxibleAddons.BaseStore`](Stores.md#BaseStore)
 * [`FluxibleAddons.createStore`](Stores.md#createStore)

 or if you're using ES6:

 ```js
 import {BaseStore, createStore} from 'fluxible/addons';
 ```

 These libraries are not bundled with the main Fluxible export because stores are classes that are decoupled from Fluxible entirely.

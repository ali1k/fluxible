# FluxibleMixin

The mixin (accessible via `require('fluxible').FluxibleMixin`) will add the contextTypes `getStore` and `executeAction`
to your component.

The mixin can also be used to statically list store dependencies and listen to them automatically in componentDidMount. This is done by adding a static property `storeListeners` in your component.

You can do this with an array, which will default all store listeners to call the `onChange` method:

```js
var FluxibleMixin = require('fluxible').FluxibleMixin;
var MockStore = require('./stores/MockStore'); // Your store
var Component = React.createClass({
    mixins: [FluxibleMixin],
    statics: {
        storeListeners: [MockStore]
    },
    onChange: function () {
        this.setState(this.getStore(MockStore).getState());
    },
});
```

Or you can be more explicit with which function to call for each store by using a hash:

```js
var FluxibleMixin = require('fluxible').FluxibleMixin;
var MockStore = require('./stores/MockStore'); // Your store
var Component = React.createClass({
    mixins: [FluxibleMixin],
    statics: {
        storeListeners: {
            onMockStoreChange: [MockStore]
        }
    },
    onMockStoreChange: function () {
        this.setState(this.getStore(MockStore).getState());
    },
});
```

This prevents boilerplate for listening to stores in `componentDidMount` and unlistening in `componentWillUnmount`.

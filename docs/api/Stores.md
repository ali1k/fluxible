# Stores

Flux stores

Stores in Fluxible are classes that adhere to a simple interface. Because we want stores to be able to be completely decoupled from Fluxible, we do not provide any store implementation in our default exports, however you can use the [utilities](#Helper Utilities) for creating your stores.

## Interface

### Constructor

The store should have a constructor function that will be used to instantiate your store using `new Store(dispatcherInterface)` where the parameters are as follows:

  * `dispatcherInterface`: An object providing access to the following methods:
    * `dispatcherInterface.getContext()`: Retrieve the [StoreContext](StoreContext.md)
    * `dispatcherInterface.getStore(storeClass)`
    * `dispatcherInterface.waitFor(storeClass[], callback)`

  The constructor is also where the initial state of the store should be initialized.

```js
function ExampleStore(dispatcher) {
    this.dispatcher = dispatcher;
    if (this.initialize) {
        this.initialize();
    }
}
```

It is also recommended to extend an event emitter so that your store can emit `change` events to the components.

```js
util.inherits(ExampleStore, EventEmitter);
```

### Static Properties

#### `storeName`

The store should define a static property that gives the name of the store. This is used internally and for debugging purposes.

```js
ExampleStore.storeName = 'ExampleStore';
```

#### handlers

The store should define a static property that maps action names to handler functions or method names. These functions will be called in the event that an action has been dispatched by the Dispatchr instance.

```js
ExampleStore.handlers = {
    'NAVIGATE': 'handleNavigate',
    'default': 'defaultHandler' // Called for any action that has not been otherwise handled
};
```

The handler function will be passed two parameters:

  * `payload`: An object containing action information.
  * `actionName`: The name of the action. This is primarily useful when using the `default` handler

```js
ExampleStore.prototype.handleNavigate = function (payload, actionName) {
    this.navigating = true;
    this.emit('change'); // Component may be listening for changes to state
};
```

If you prefer to define private methods for handling actions, you can use a static function instead of a method name. This function will be bound to the store instance when it is called:

```js
ExampleStore.handlers = {
    'NAVIGATE': function handleNavigate(payload, actionName) {
        // bound to store instance
        this.navigating = true;
        this.emit('change');
    }
};
```

### Instance Methods

#### dehydrate()

The store should define this function to dehydrate the store if it will be shared between server and client. It should return a serializable data object that will be passed to the client.

```js
ExampleStore.prototype.dehydrate = function () {
    return {
        navigating: this.navigating
    };
};
```

#### rehydrate(state)

The store should define this function to rehydrate the store if it will be shared between server and client. It should restore the store to the original state using the passed `state`.

```js
ExampleStore.prototype.rehydrate = function (state) {
    this.navigating = state.navigating;
};
```

#### shouldDehydrate()

The store can optionally define this function to control whether the store state should be dehydrated by the dispatcher. This method should return a boolean. If this function is undefined, the store will always be dehydrated (just as if true was returned from method).

```js
ExampleStore.prototype.shouldDehydrate = function () {
    return true;
}
```

## Helper Utilities

### BaseStore

A base class that you can extend to reduce boilerplate when creating stores.

```js
var BaseStore = require('fluxible/addons').BaseStore;
```

### createStore

```js
var createStore = require('fluxible/addons').createStore;
```

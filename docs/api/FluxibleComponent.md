# FluxibleComponent

The `FluxibleComponent` is a wrapper component that will provide all of its children with access to the Fluxible component
context via React's context. This should be used to wrap your top level component. It provides access to the following methods on the [ComponentContext](ComponentContext.md):

 * `getStore(storeClass)`
 * `executeAction(action, payload)`

 You can get access to these methods by setting the correct `contextTypes` within your component or including the [`FluxibleMixin`](FluxibleMixin.md) which will add them for you.

## Usage

If you have a component that needs access to the [`ComponentContext`](ComponentContext.md) methods:

 ```js
var Component = React.createClass({
    contextTypes: {
        getStore: React.PropTypes.func.isRequired,
        executeAction: React.PropTypes.func.isRequired
    },
    getInitialState: function () {
        return this.getStore(FooStore).getState();
    }
});

you can wrap the component with `FluxibleComponent` to provide the correct context:

```js
var FluxibleComponent = require('fluxible').FluxibleComponent;
var html = React.renderToString(
    <FluxibleComponent context={context.getComponentContext()}>
        <Component />
    </FluxibleComponent>
);
```

 If you are using [`FluxibleContext.createElement()`](FluxibleContext.md#createElement) this will happen for you automatically:

```js
var html = React.renderToString(context.createElement());
```

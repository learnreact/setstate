# setstate
Set local state in a React.Component

[setstate on github](https://github.com/learnreact/setstate)

## Installation
```js
yarn add react setstate
```

## Example
setState keeps local state on an instance of `React.Component` or `React.PureComponent`.

In practice, it looks like so:

```js
import React from "react";
import setState from "setstate";

class Counter extends React.Component {
  constructor() {
    super();
    this.state = { count: 0 };
  }

  render() {
    return (
      <div>
        <h1>{this.state.count}</h1>

        <button
          type="button"
          onClick={() => this.setState(({ count }) => ({ count: count + 1 }))}
        >+</button>

        <button
          type="button"
          onClick={() => this.setState(({ count }) => ({ count: count - 1 }))}
        >+</button>
      </div>
    );
  }
}

```

## Use in Create React App
`create-react-app` ships with  [`transform-class-properties`](https://babeljs.io/docs/plugins/transform-class-properties/) installed.

This can make working with local state faster and less ceremonious.

```js
class Counter extends React.Component {
  // don't mess with the constructor to initialize state.

  state = { count: 0 }

  // create instance methods for better perf and re-use.

  increment = () => this.setState(({ count }) => ({ count: count + 1 }))
  decrement = () => this.setState(({ count }) => ({ count: count - 1 }))

  // the clean code you've always dreamed of.

  render() {
    return (
      <div>
        <h1>{this.state.count}</h1>

        <button type="button" onClick={this.increment}>+</button>
        <button type="button" onClick={this.decrement}>+</button>
      </div>
    );
  }
}
```

## API
`setstate` ships with 2 APIs.
I know that sounds complicated but it's not.

### Object form
This is best used when setting a new value or blowing away a previous value:

```js
this.setState({ name: "Michael" })
```

Here's what it looks like in response to an input's change event.

```js
// this.state.name gets replaced for every onChange
<input
  type="text"
  value={this.state.name}
  onChange={({ target }) => this.setState({ name: target.value })}
/>
```

### Function form
This is best used when transitioning existing state (like the counter above).

```js
this.setState(previousState => ({ count: previousState.count + 1 }));
```

This is what it looks like in response to a button press:

```js
<button
  type="button"
  onClick={() =>
    this.setState(previousState => ({ count: previousState.count + 1 }))
  };
```

### Optional callback
`setState` is asynchronous.

You can use the optional callback to fire code after state is updated.

```js
this.setState(
  { name: "chantastic" },
  () => console.log("the new name is: ", this.state.name)
)
```

This is handy but not as powerful as using `setstate` with a React component's lifecycle methods.

### Works with React's lifecycle methods
```js
class Counter extends React.Component {
  // look, ma! no callbacks.
  componentDidUpdate(prevProps, prevousState) {
    console.log("current state: ", this.state)
    console.log("previous state: ", previousState)
  }  

  render() { return <div>{this.state.count}</div> }
}
```

## Future
I'm hopeful that this will end up in React proper.
When it does, you'll be able to remove the `setstate` import and everything will work the same.

## LICENSE
MIT &reg; Michael Chan, 2017

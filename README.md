# setstate
Set local state in a React.Component

## Installation
```js
yarn add react setstate
```

## API
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
    </div>;
  }
}

```

## Future
I'm hopeful that this will end up in React proper.
When it does, you'll be able to remove the `import setstate` import and everything will work the same.

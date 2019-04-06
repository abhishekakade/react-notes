# React Notes -

- Names like `onClick`, `onHover` only create event listeners if they're used on HTML-like JSX elements. Otherwise, they're just ordinary prop names as they are inside of a component instance (and NOT HTML-like JSX element).

- If a component has **more than one child** between its JSX tags, then `this.props.children` **will return those children in an array**. However, if a component has **only one child**, then `this.props.children` **will return the single child, not wrapped in an array**.

- Any time that you call `this.setState()`, `this.setState()` AUTOMATICALLY calls `.render()` as soon as the state has changed. Think of `this.setState()` as actually being two things: `this.setState()`, immediately followed by `.render()`. That is why you can’t call `this.setState()` from inside of the `.render()` method! `this.setState()` automatically calls `.render()`. If `.render()` calls `this.setState()`, then an infinite loop is created.

## React Lifecycle Methods -

### constructor(props) -

**If you don’t initialize state and you don’t bind methods, you don’t need to implement a constructor** for your React component. The `constructor` for a React component is called before it is mounted. When implementing the constructor for a **`React.Component` subclass**, you should call **`super(props)`** before any other statement. Otherwise, **`this.props` will be undefined** in the constructor, which can lead to bugs.

Typically, in React constructors are only used for two purposes:

- Initializing local state by assigning an object to `this.state`.
- Binding event handler methods to an instance.

You **should not call `setState()` in the `constructor()`**. **Instead**, if your component needs to use local state, **assign the initial state to `this.state` directly in the constructor**:

    constructor(props) {
      super(props);
      // Don't call this.setState() here!
      this.state = { counter: 0 };
      this.handleClick = this.handleClick.bind(this);
    }

### componentWillMount -

This method is called before the `render()` method when a component is being mounted to the DOM.

### componentDidMount -

**The best way to place API calls or any calls to your server**. This method is called after a component is mounted to the DOM. Any calls to **`setState()`** here will trigger a **re-rendering** of your component. When you call an API in this method, and set your state with the data that the API returns, it will automatically trigger an update once you receive the data.

**This is also the best place to attach any event listeners** you need. React provides a synthetic event system which wraps the native event system present in browsers. This means that the synthetic event system behaves exactly the same regardless of the user's browser - even if the native events may behave differently between different browsers. `onClick()` is an example of such synthetic event system. **_However, if you want to attach an event handler to the `document` or `window` objects, you will have to do so directly._**

### componentWillReceiveProps -

This method is called whenever a component is receiving new props. This method **receives the new props as an argument**, which is usually written as nextProps. You can use this argument and compare with `this.props` and perform actions before the component updates. This argument is usally called as `nextProps`.

### componentDidUpdate -

This method is **called immediately after a component re-renders**. Note that rendering and mounting are considered different things in the component lifecycle. When a page first loads, all components are mounted and this is where methods like `componentWillMount()` and `componentDidMount()` are called. After this, components re-render themselves as state changes.

### shouldComponentUpdate -

If any component receives new `state` or new `props`, it re-renders itself and all its children. This is usually okay. But React provides a lifecycle method you can call when child components receive new state or props, and declare specifically if the components should update or not. This method takes `nextProps` and `nextState` as parameters. This method is a useful way to optimize performance.

The default behavior is that your component re-renders whenever it receives new `props`, even if the `props` haven't changed. You can use `shouldComponentUpdate()` to prevent this by comparing the props. **The method must return a `boolean` value that tells React whether or not to update the component. You can compare the current props (`this.props`) to the next props (`nextProps`) to determine if you need to update** or not, and return `true` or `false` accordingly.

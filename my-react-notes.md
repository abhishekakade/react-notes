# React Notes -

- Names like `onClick`, `onHover` only create event listeners if they're used on HTML-like JSX elements. Otherwise, they're just ordinary prop names as they are inside of a component instance (and NOT HTML-like JSX element).

- If a component has **more than one child** between its JSX tags, then `this.props.children` **will return those children in an array**. However, if a component has **only one child**, then `this.props.children` **will return the single child, not wrapped in an array**.

- Any time that you call `this.setState()`, `this.setState()` AUTOMATICALLY calls `.render()` as soon as the state has changed. Think of `this.setState()` as actually being two things: `this.setState()`, immediately followed by `.render()`. That is why you can’t call `this.setState()` from inside of the `.render()` method! `this.setState()` automatically calls `.render()`. If `.render()` calls `this.setState()`, then an infinite loop is created.

## React Lifecycles -

### componentWillMount -

This method is called before the `render()` method when a component is being mounted to the DOM.

### componentDidMount -

**The best way to place API calls or any calls to your server**. This method is called after a component is mounted to the DOM. Any calls to **`setState()`** here will trigger a **re-rendering** of your component. When you call an API in this method, and set your state with the data that the API returns, it will automatically trigger an update once you receive the data.

**This is also the best place to attach any event listeners** you need. React provides a synthetic event system which wraps the native event system present in browsers. This means that the synthetic event system behaves exactly the same regardless of the user's browser - even if the native events may behave differently between different browsers. `onClick()` is an example of such synthetic event system. **_However, if you want to attach an event handler to the `document` or `window` objects, you will have to do so directly._**

# Redux Notes

- The whole state of your app is stored in an object tree inside a single **store**. The only way to change the state tree is to emit an **action**, an object describing what happened. To specify how the actions transform the state tree, you write pure **reducers**. That's it!

- Instead of mutating the state directly, you specify the mutations you want to happen with plain objects called **actions**. Then you write a special function called a **reducer** to decide how every action transforms the entire application's state.

- In a typical Redux app, there is just a single store with a single root reducing function. As your app grows, you split the root reducer into smaller reducers independently operating on the different parts of the state tree. This is exactly like how there is just one root component in a React app, but it is composed out of many small components.

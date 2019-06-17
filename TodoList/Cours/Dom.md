# The Dom
So we saw how to create one component and create a second one in the others but we still don't know how to display them.

React uses a principle called "virtual DOM": it will create a page virtually and display it only when asked.

Here, in index.js, we importe the app components where there is a ````JSReactDOM.render(<App />, document.getElementById('root'));````

To make it simple, it creates our view and displays it where the root ID is located in index.html.


Next lesson is : [props](./PropsEtState.md).

#Interaction between Components
Thanks to the props and the state we can increment the value of the number of todos of our app and display them with another component. Now we will make sure to display their names and change them from "resolved" or "to do".

The first thing to do is to change the behavior of the List component. There are several ways to do this:

Make a loop to display each time the title and date of our todos.
Make a function that will return the values of the props and therefore the properties of the todos.
Instead, we will work with the second method. In the JSX, we will call a showTodos function and pass it the parameters (props). In the function, we will map the object that is returned to us and return a div containing the title.

````jsx harmony
  showTodos(todos){
    return (
      todos.map((todo) => {
        return (
          <div className="todo">{todo.title}</div>
        )}
    ))
  }
````

In order to manage the fact that a todo is completed or not, we will add to the pattern of the todo object the attribute done and assign it false base. Add in the "AddTodo" function, a new props with the title and the createdAt, which will be:

````jsx harmony
  AddTodo(event) {
    event.preventDefault();
    const txt = this.toDoTitle.value;
    this.props.onNewTodo({
        title : txt,
        done: false,
        createDate : new Date()
    })
}
````

Then, when you click on the, you want to change the done attibut and switch it from false to true and vice versa.

````jsx harmony
  showTodos(todos){
    return (
      todos.map((todo) => {
        return (
          <div className="todo">{todo.title}{todo.done ? 'true': 'false '}</div>
        )}
    ))
  }
````

Let's add an onClick event on the div that points to a toggleTodo() function. A function called by an onClick has an event that must be stopped, so preventDefault(). We will pass as a parameter in the function call; todo.done.

In the function we will just make a console.log and normally we get false in the browser console.
````jsx harmony
toggleTodo(todoDone){
    console.log(todoDone)
}  

showTodos(todos){
  return(
    todos.map((todo) => {
      return (
        <div className="todo" onClick={() => this.toggleTodo(todo.done)}>
          {todo.title} {todo.done ? 'true': 'false'}
        </div>
      )}
  ))
}
````

In the console, there is also another error: Each child in an array or iterator should have a unique "key" prop. This means that each array that we pass as props must have a unique key. We will pass a key in the same way as our props by giving it as value the title of the props, in theory, we will not have the same thing twice (If we do the same todo several times we will fall back on the same error).

````jsx harmony
 <div key={} className="todo" onClick={() => this.toggleTodo(todo.done)}>
   {todo.title} {todo.done ? 'true': 'false'}
 </div>
````

We're going to go back to App.js, which sends the data. What we will do is send the todoToggleState function from App to List via the props (onTodoToggle) and this function will make the changes.

````jsx harmony
todoToggleState(todo, index){
  console.log(todo, index)
}

<List todos={this.state.todos} onTodoToggle={this.todoToggleState.bind(this)}/>
````

So how do I get the List todo and send it to the parent component? We know that we have to call the function sent by the props at the time of click and give it a parameter, but it won't work. We're going to need his index which is created in the map:

you have to add a parameter in the map,
it is necessary to retrieve the index in the toggleTodo function
send it to the parent component
Assign a value to key by the index to be able to make several identical todos. The index will identify which todo to modify in the parent component.
````jsx harmony
todos.map((todo,index) => {
  return (
    <div key={index} className="todo" onClick={() => this.toggleTodo(todo,index)}>
      {todo.title} {todo.done ? 'true': 'false '}
    </div>
)}


toggleTodo(todoDone, index){
  this.props.onTodoToggle(todoDone, index);
}  
````

So in the parent component, if we console.log todo and index, we can see our todo and its index which will allow us to modify everything in the state. So we have all the elements we need to do that.

In the App component we will just create a variable (with let) to instantiate todo, then invert its value for todo.done from todo.done (so we toggle). Logically, then, we modify the state with the new values.

````jsx harmony
todoToggleState(todo, index){
    let _todo = todo;
    _todo.done = ! todo.done;
    let newTodos =  this.state.todos; 
    newTodos[index] = _todo;
    this.setState({todos: newTodos})
  }
````

To recap, if you want to modify the state from another component, you can create a function in the parent that allows the modification (setState()), pass it in props to the child, pass in parameter of this function the necessary information for the modifications.

At first we said that a component had props and a state. The state is the set of data that is internal and specific to the component itself. He can change the information as he sees fit. The props, are information that other components pass to it, the component cannot modify them. If you want to modify a todo or todos, you must ask the component that gave them to you to make the change itself. Which means we can't make the changes directly.

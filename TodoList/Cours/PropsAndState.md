# Props and State
The props (property) is a parameter that allows us to pass information from one element to another.

The basic syntax for sending a props:
````JS
var value = 'hello';
<List PropsName={valeur}/>
````
We call the component and then pass parameters to it like an HTML tag. Here the name of the props is: "NameDuProps" and its value is the content of the value variable.

to retrieve the props value, once in the component List called just above, anywhere in the class, we will use :

 ````JS
 var test = this.props.PropsName;
 console.log(test);
 ````
 
 Finally, in the console, it displays "hello".
 
 For our application, we will create a ToDoList. To do this, in the App component we will add a List component in the Component folder. For the moment, it doesn't display much.
````JS
export default class List extends React.Component {
  render() {
    return (
        <div className="liste">

        </div>
    );
  }
}
````
To pass values from one component to another, you simply need to add one or more props:
 
````JS
<List todos={['vaiselle','cuisiner']} NomDeMaProps2={valeur2} />
````

To decompose:

todos={{['dish','cook']} -> a props called todos in which we send an array with two elements
NameDeMaProps2={value2} -> a props called NameDeMaProps2 in which we send a variable value2 which contains the value we want. (this is an example)
To display the data that have passed from one component to another, it is necessary to return to the component List:

````JS
export default class List extends React.Component {
  render() {
    return (
        <div className="list">
            {this.props.todos.length} // égale 2
        </div>
    );
  }
}
````

Here we have displayed something dynamic in the render with HTML. When we want to display the content of a variable in the return, we use "{ }" otherwise, we can create functions in our component to process the information that is sent to us.
````JS
export default class List extends React.Component {
  test(){
    return 'bonjour';
  }

  render() {
    return (
        <div className="list">
            {this.props.todos.length}
            {this.test()}
        </div>
    );
  }
}
````

The information passed in parameters is accessible with the props attribute.

For our App, we have a component to display the number of tasks to be performed (todos), currently it only displays the size, but we also need a component to create them and keep a logic of separation of the components. Let's call it <TodoForm /> in App.

Create a new component called TodoForm, in which you will make a form in a div in which there will be two things (an input type text and a button).

````html
<div className="liste">
    <form>
        <input type="text" />
        <button>Ajouter</button>
    </form>
</div>
````

You should see a form appear with a button and an input. Ideally, every time we run our button, it adds a todo, so it adds it to our App. We'll give him a props also called onNewTodo. In this props, we can pass functions.
````jsx harmony
class App extends Component {
  onNewTodo(todo){
    console.log(todo);
  }
  render() { 
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">Bonjour</h1>
        </header>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
        <TodoForm onNewTodo={this.onNewTodo} />
        <List todos={["vaiselle", "cuisine"]} />
      </div>
    );
  }
}
````

In the TodoForm component, we have an input and a button to add "todo". What we want is that when we click on the button, we get the value from the input and pass it to the parent component. Use the "ref" in the input, it is an attribute that will receive a function, an object, a simple character string,... And will give a name to allow it to be used later.

````jsx harmony
<input type="text" ref={(input) => this.ToDoTitle = input} />
````
We create a ToDoTitle property, to take the value that we enter in the input. But for the moment, it is not displayed anywhere, we use this ToDoTitle to be able to access the variable in the parent component.

(input)=> is a new syntax for doing a function in JavaScript ES6, doing the function input(){this.ToDoTitle = input} is like doing the same thing. We will add a function to the button that will stop the current event and display the content of the console.

````JS
AddTodo(event){ 
    event.preventDefault();
    console.log(this.ToDoTitle.value);
}
````

````jsx harmony
<button onClick={this.AddTodo.bind(this)} >Ajouter</button>
````
If this works, we replace the console.log by a "const" txt in which we give it the value of the input, in this case, this.ToDoTitle.value. Now we will send to the parent function (onNewTodo) the values we have retrieved as an object.
````jsx harmony
AddTodo(event){
    event.preventDefault();
    const txt = this.ToDoTitle.value;
    this.props.onNewTodo({
        title: txt,
        createdAt: new Date()
    })
}
````
So we go to our page and test the form. If all goes well, it should display: {title: "test", createdAt: Kill Nov 14 2017 15:30:56 GMT+0100 (CET)}.

To summarize:

The onNewTodo function is sent in props to the TodoForm component.
TodoForm receives the function
We update our txt variable when we click on the button using the AddTodo function
The onNewTodo function is called from the props
We give him the necessary parameters
We execute the function so the console.log
Well, that's for sure, it's too cool, but in reality it's useless. Now the goal is to send everything to our component List.

A simple trick would have been to send a table to the other component (nosTodo.push(todo)) but React did something else for us. One component has 2 types of data:

Component-specific data -> State
The data that are passed to it -> Props
What we're going to do instead is update this famous state. The state is therefore an internal object of our component and to use it we must use a constructor to declare it and the setState() function to modify it. The constructor is a function that will set up the first parameters of our component. So in the App. js:


````jsx harmony
constructor(props){
    super(props);
    this.state = {
        todos:[]
    };
}

onNewTodo(todo){
    let newTodoList = this.state.todos;
    newTodoList.push(todo);
    this.setState({ todos: newTodoList });
}
````

But then why did we do newTodoList.push right away? The only way to modify the state is to use the setState() function.

And now that we have a state, we can pass it in the component List in props: <List todos={this.state.todos} /> If we test, we will notice that it does not work because it does not work... Cannot read property "todos" of undefined. We do not send the right "this" to our function and to do so, we need bind(this) for the function. (A little weird, I'll give you that, but it works)

````jsx harmony
<TodoForm onNewTodo={this.onNewTodo.bind(this)} />
````
The state and props are 2 very very very important elements in React. The props allows to pass information from one component to another, no matter what an object, a variable, a function, the state,... The state is an object that remains within reach of our component and can only be modified with the setState().

Before moving on, there is a google extension for React that allows you to see how it makes our view. This is the react dev tools. Once installed, in the inspector, there is a new tab that appears (it is the last one so it may be hidden). With this, we can see the components of the view and the props that have passed to it and also the state of the state without having to make a console.log :)


![Giphy](https://media.giphy.com/media/13CoXDiaCcCoyk/giphy.gif)

Next Lesson [Interaction between components P1](./InteractionBetweensComponentPart1.md).

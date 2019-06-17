#Introduction

React is a view library created by Facebook and Instagram, React only modifies the view and uses mainly a system with components.
## What is a component?
   A component is only a piece of code that can be a simple button or even an entire application.

![alt text](http://nitrajka.com/wp-content/uploads/2016/08/uimockscript.png)

In the image above, we can see the different components of our application, which goes from the simple EmployeeList to the app.
In this professional management interface: on the left there is a component with a button, a header and a list where each element is a component. The list of employees can be further broken down with the EmployeeListItem component, which contains three components: Photo profile, Name profile, Post profile. We'll see with React how we can go from a very simple small component to a complete interface.

React is not the only one in its category. Angular or Backbone which are "real" MVC frameworks, just like the new ELM.

##Create a React component
Create a React component
React allows you to create views dynamically rather than statically.

For our first component, we will create a class:

```JS
class Welcome extends React.Component {
  render() {
    return <h1>Hello</h1>;
  }
}
```
This is our first React component. It is an object that implements the method renders and returns something that looks like HTML but is not.

Normally in HTML, we use the class to give a name to our element and to be able to select it. Here we will use in HTML not class but className, because React already uses Class.

The HTML you see is called JSX (Javascript Extension). We will see in detail why React works in this way with HTML.

Create a Welcome.js file in the component folder previously created by you in the src folder, and put the little piece of code just above it in this file. Look what's going on in your browser.

Nothing is happening and that's normal! It must be displayed. To do this, we will call the Welcome component in App.js.
```JS

<Welcome/> 

```
At the place where we want it to be added (sort of like an include) but in the render. Everything that happens in the render will be everything it displays on the screen.

And that's the bug....

There are some basic rules to remember to put a component in our view:

A component must always contain a render method in which a return is located
We put the JSX in the return but there can only be one main div:
```html

<div className="main">
    <div className="container">
        bonjour
    </div>
    <div className="container">
        Aurevoir
    </div>
</div>
```
-> it's Okay
````html

<div className="main">
    Hello
</div>
<div className="container">
    Goodbye
</div>
````
-> c'est pas bon, car ici, il y a deux div principales (au même niveau)

-> it's not good, because here, there are two main dives (at the same level)

We also need to import our component into the file where we want it to appear
We have to export the component we have to display
So, in App.js we add

    import Welcome from './component/Welcome';
(en français : on importe notre class "Welcome" -> de -> ./ (dans le même dossier) -> Welcome (qui revient à dire Welcome.js (React comprend que c'est du JS mais si c'est un autre langage il faut lui présiser)))

Si on ajoute le import ça fait une erreur de moins mais il nous en reste encore deux.

Dans Welcome.js il faut qu'on lui dise qu'on veut exporter. Il y a 2 manières de faire :
```JS
class Welcome extends React.Component {
    render() {
      return <h1>Hello</h1>;
    }
}

export default Welcome;
```


or
````JS
export default class Welcome extends React.Component {
    render() {
      return <h1>Hello</h1>;
    }
}
````

And now we only have one step left which is simply to tell our project that our component is a component by adding it above in Welcome.js :
````js
import React from 'react';
````
You're going to say to me, "Oh, my God, how can you import React if you don't tell me where it is anywhere?" To make it simple, when we don't put ./ before, by default it will look in the node_modules that nodeJS to install with the react-create-app and one of these is called React and it will load it.

If everything went well, we should have our application running correctly with our very first component!


![Giphy](https://www.acsu.buffalo.edu/~cas7/gifs/react.gif)
See you in the next lesson : [Dom](./Dom.md).


Rendez-vous à la prochaine leçon : Dom.
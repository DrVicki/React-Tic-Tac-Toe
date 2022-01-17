Here are two ways to complete this tutorial: 
  - you can either write the code in your browser, or 
  - you can set up a local development environment on your computer.

## Setup Option 1: Write Code in the Browser

This is the quickest way to get started!

First, open this [Starter Code](https://codepen.io/drbealman/pen/WNZmgEx) in a new tab. 
  - The new tab should display an empty tic-tac-toe game board and React code. We will be editing the React code in this tutorial.

You can now skip the second setup option, and go to the Overview section to get an overview of React.

Setup Option 2: Local Development Environment
This is completely optional and not required for this tutorial!


**Optional: Instructions for following along locally using your preferred text editor**
Help, I’m Stuck!
If you get stuck, check out the community support resources. In particular, Reactiflux Chat is a great way to get help quickly. If you don’t receive an answer, or if you remain stuck, please file an issue, and we’ll help you out.

## Overview

Now that you’re set up, let’s get an overview of React!

### What Is React?

React is a declarative, efficient, and flexible JavaScript library for building user interfaces. 
  - It lets you compose complex UIs from small and isolated pieces of code called “```components```”.

React has a different kinds of components, but we’ll start with ```React.Component``` subclasses:

```
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

// Example usage: <ShoppingList name="Mark" />
```

We’ll get to the XML-like tags soon. We use components to tell React what we want to see on the screen. 
  - When our data changes, React will efficiently update and re-render our components.

Here, ```ShoppingLis```t is a **React component class**, or **React component type**. A component takes in parameters, called ```props``` (short for “properties”), and returns a hierarchy of views to display via the ```render``` method.

  - The ```render``` method returns a description of what you want to see on the screen. 
  - React takes the description and displays the result. 
  - In particular, ```render``` returns a **React element**, which is a lightweight description of what to render. Most React developers use a special syntax called “JSX” which makes these structures easier to write. The``` <div />``` syntax is transformed at build time to ```React.createElement('div')```. The example above is equivalent to:

```
return React.createElement('div', {className: 'shopping-list'},
  React.createElement('h1', /* ... h1 children ... */),
  React.createElement('ul', /* ... ul children ... */)
);
```
[See full expanded version.](https://babeljs.io/repl/#?presets=react&code_lz=DwEwlgbgBAxgNgQwM5IHIILYFMC8AiJACwHsAHUsAOwHMBaOMJAFzwD4AoKKYQgRlYDKJclWpQAMoyZQAZsQBOUAN6l5ZJADpKmLAF9gAej4cuwAK5wTXbg1YBJSswTV5mQ7c7XgtgOqEETEgAguTuYFamtgDyMBZmSGFWhhYchuAQrADc7EA)

If you’re curious, ```createElement()``` is described in more detail in the [API reference](https://reactjs.org/docs/react-api.html#createelement), but we won’t be using it in this tutorial. Instead, we will keep using **JSX**.

**JSX** comes with the full power of JavaScript. 
  - You can put any JavaScript expressions within braces inside JSX. Each React element is a JavaScript object you can store in a variable or pass around in your program.

The ```ShoppingList``` component above only renders built-in DOM components like ```<div />``` and ```<li />```. But you can compose and render custom React components too. For example, we can now refer to the whole shopping list by writing ```<ShoppingList />```. 
  - Each React component is encapsulated and can operate independently; this allows you to build complex UIs from simple components.

## Inspecting the Starter Code

If you’re going to work on the tutorial in your browser, open this code in a new tab: [Starter Code](https://codepen.io/drbealman/pen/WNZmgEx?editors=0010). 

This Starter Code is the base of what we’re building. We’ve provided the CSS styling so you only need to focus on learning React and programming the tic-tac-toe game.

By inspecting the code, you’ll notice that we have three React components:

  - ```Square```
  - ```Board```
  - ```Game```

The ```Square component``` renders a single ```<button>`` and the ```Board``` renders 9 squares. The ```Game``` component renders a board with placeholder values which we’ll modify later. There are currently no interactive components.

## Passing Data Through Props

Let’s try passing some data from our ```Board``` component to our ```Square``` component.

We strongly recommend typing code by hand as you’re working through the tutorial and not using copy/paste. 
  - This will help you develop muscle memory and a stronger understanding.

In Board’s ```renderSquare``` method, change the code to pass a prop called ```value``` to the ```Square```:

```
class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i} />;
  }
}
Change Square’s render method to show that value by replacing {/* TODO */} with {this.props.value}:

class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}
```

Before:

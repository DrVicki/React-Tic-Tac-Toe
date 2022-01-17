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

![](https://github.com/DrVicki/React-Tic-Tac-Toe/blob/main/tictac-images/tictac-empty.png)

After: You should see a number in each square in the rendered output.

![](https://github.com/DrVicki/React-Tic-Tac-Toe/blob/main/tictac-images/tictac-numbers.png)

**Congratulations!** You’ve just “passed a prop” from a parent ```Board``` component to a child ```Square``` component. Passing props is how information flows in React apps, from parents to children.

## Making an Interactive Component

Let’s fill the ```Square``` component with an “```X```” when we click it. First, change the ```button``` tag returned from the ```Square``` component’s ```render()``` function to this:

```
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={function() { console.log('click'); }}>
        {this.props.value}
      </button>
    );
  }
}
```

If you click on a Square now, you should see ‘click’ in your browser’s ```devtools``` console.

**Note**

To save typing and avoid the confusing behavior of this, we will use the ```arrow``` function syntax for event handlers here and further below:

```
class Square extends React.Component {
 render() {
   return (
     <button className="square" onClick={() => console.log('click')}>
       {this.props.value}
     </button>
   );
 }
}
```

Notice how with ```onClick={() => console.log('click')}```, we’re passing a function as the ```onClick``` prop. 
  - React will only call this function after a click. Forgetting ```() =>``` and writing ```onClick={console.log('click')}``` is a common mistake, and would fire every time the component re-renders.

As a next step, we want the ```Square``` component to “remember” that it got clicked, and fill it with an “```X```” mark. To “remember” things, components use ```state```.

React components can have **state** by setting ```this.state``` in their constructors. ```this.state``` should be considered as private to a React component it’s defined in. Let’s store the current value of the Square in ```this.state```, and change it when the Square is clicked.

First, we’ll add a constructor to the class to initialize the state:

```
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button className="square" onClick={() => console.log('click')}>
        {this.props.value}
      </button>
    );
  }
}
```

**Note**

In [JavaScript classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes), you need to always call ```super``` when defining the constructor of a subclass. All React component classes that have a ```constructor``` should start with a ```super(props)``` call.

Now we’ll change the Square’s ```render``` method to display the current state’s value when clicked:

  - Replace ```this.props.value``` with ```this.state.value``` inside the ```<button>``` tag.
  - Replace the ```onClick={...}``` event handler with ```onClick={() => this.setState({value: 'X'})}```.
  - Put the ```className``` and ```onClick``` props on separate lines for better readability.

After these changes, the ```<button>``` tag returned by the Square’s ```render``` method looks like this:

```
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button
        className="square"
        onClick={() => this.setState({value: 'X'})}
      >
        {this.state.value}
      </button>
    );
  }
}
```

By calling ```this.setState``` from an ```onClick``` handler in the Square’s ```render``` method, we tell React to re-render that Square whenever its ```<button>``` is clicked.
  - After the update, the Square’s ```this.state.value``` will be '```X```', so we’ll see the **X** on the game board. 
  - If you click on any Square, an X should show up.

When you call ```setState``` in a component, React automatically updates the child components inside of it, too.

## Developer Tools

The React ```Devtools``` extension for [Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) and [Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/) let you inspect a React component tree with your browser’s developer tools.

![](https://github.com/DrVicki/React-Tic-Tac-Toe/blob/main/tictac-images/devtools.png)

The React DevTools let you check the ```props``` and the ```state``` of your React components.

After installing React ```DevTools```, you can right-click on any element on the page, click “Inspect” to open the developer tools, and the React tabs (“⚛️ Components” and “⚛️ Profiler”) will appear as the last tabs to the right. Use “⚛️ Components” to inspect the component tree.

However, note there are a few extra steps to get it working with CodePen:



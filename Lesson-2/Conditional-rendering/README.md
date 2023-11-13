## Conditional rendering

### What is conditional rendering in React?

In React, conditional rendering refers to the process of delivering elements and components based on certain conditions.

There’s more than one way to use conditional rendering in React. Like with most things in programming, some things are better suited than others depending on the problem you’re trying to solve.

* How to write if...else in React?

Create a component with the following state:

```react
import React from "react"

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      text: "",
      inputText: "",
      mode: "view",
    };
  }
}
```

You’ll use one property for the saved text and another for the text that is being edited. A third property will indicate if you are in edit or view mode.

Next, add some methods for handling input text, then save and edit events as follows:

```react
class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {text: '', inputText: '', mode:'view'};

    this.handleChange = this.handleChange.bind(this);
    this.handleSave = this.handleSave.bind(this);
    this.handleEdit = this.handleEdit.bind(this);
  }

  handleChange(e) {
    this.setState({ inputText: e.target.value });
  }

  handleSave() {
    this.setState({text: this.state.inputText, mode: 'view'});
  }

  handleEdit() {
    this.setState({mode: 'edit'});
  }
}

```

Now, for the render method, check the mode state property to either render an edit button or a text input and a save button, in addition to the saved text:

```react
class App extends React.Component {
  // …
  render () {
    if(this.state.mode === 'view') {
      return (
        <div>
          <p>Text: {this.state.text}</p>
          <button onClick={this.handleEdit}>
            Edit
          </button>
        </div>
      );
    } else {
      return (
        <div>
          <p>Text: {this.state.text}</p>
            <input
              onChange={this.handleChange}
              value={this.state.inputText}
            />
          <button onClick={this.handleSave}>
            Save
          </button>
        </div>
      );
    }
}
```

Let’s simplify it by extracting all the conditional logic to two render methods: one to render the input box and another to render the button:

```react
class App extends React.Component {
  // …

  renderInputField() {
    if(this.state.mode === 'view') {
      return <div></div>;
    } else {
      return (
          <p>
            <input
              onChange={this.handleChange}
              value={this.state.inputText}
            />
          </p>
      );
    }
  }

  renderButton() {
    if(this.state.mode === 'view') {
      return (
          <button onClick={this.handleEdit}>
            Edit
          </button>
      );
    } else {
      return (
          <button onClick={this.handleSave}>
            Save
          </button>
      );
    }
  }

  render () {
    return (
      <div>
        <p>Text: {this.state.text}</p>
        {this.renderInputField()}
        {this.renderButton()}
      </div>
    );
  }
}
```

Let’s imagine that we have more than two branches that depend on the same variable to evaluate the condition. You might consider using a large if...else block, like in the code below:

```react
if(this.state.mode === 'a') {
  // ...   
} else if(this.state.mode === 'b') {
  // ...
} else if(this.state.mode === 'c') {
  // ...
} else {
  // ...
}
```

Instead, you can use a switch statement as follows:

```react
switch(this.state.mode) {
  case 'a':
    // ...
  case 'b':
    // ...
  case 'c':
    // ...
  default:
    // equivalent to the last else clause ...
}
```
The switch statement may add a bit more clarity, but it’s still too verbose, and it doesn’t work with multiple or different conditions. Just like an if...else statement, you can’t use a switch statement inside of a return statement with JSX unless you use immediately invoked functions, which we’ll cover later.

Let’s look at some additional techniques to improve this code. Notice that the method renderInputField returns an empty <div> element when the app is in view mode. However, this is not necessary.

* Prevent rendering with null

One advantage of returning null instead of an empty element is that you’ll improve the performance of your app a little bit because React won’t have to unmount the component to replace it.

```react
 renderInputField() {
    if(this.state.mode === 'view') {
      return null;
    } else {
      return (
          <p>
            <input
              onChange={this.handleChange}
              value={this.state.inputText}
            />
          </p>
      );
    }
  }
```

* The ternary operator in React

Instead of using an if...else block, we can use the ternary conditional operator:

```condition ? expr_if_true : expr_if_false```

The operator is wrapped in curly braces, and the expressions can contain JSX, which you can wrap in parentheses to improve readability. The operator can also be applied in different parts of the component.

Let’s apply it to the example to see this in action. I’ll remove renderInputField and renderButton, and in the render method, I’ll add a variable to know if the component is in view or edit mode:

```react
render () {
  const view = this.state.mode === 'view';

  return (
      <div>
      </div>
  );
}
```

Now, you can use the ternary operator to return null if the view mode is set, or set the input field otherwise:

```react
  // ...

  return (
      <div>
        <p>Text: {this.state.text}</p>

        {
          view
          ? null
          : (
            <p>
              <input
                onChange={this.handleChange}
                value={this.state.inputText} />
            </p>
          )
        }

      </div>
  );
```

Using a ternary operator, you can declare one component to render either a save or an edit button by changing its handler and label correspondingly:

```react
  // ...

  return (
      <div>
        <p>Text: {this.state.text}</p>

        {
          ...
        }

        <button
          onClick={
            view 
              ? this.handleEdit 
              : this.handleSave
          } >
              {view ? 'Edit' : 'Save'}
        </button>

      </div>
  );
```

* Short-circuit AND operator &&

There is a special case where the ternary operator can be simplified. When you want to render either something or nothing, you can only use the && operator. Unlike the & operator, && doesn’t evaluate the right-hand expression if only the left-hand expression can decide the final result.

For example, if the first expression evaluates to false, false && …, it’s not necessary to evaluate the next expression because the result will always be false.

In React, you can have expressions like the following:

```react
return (
    <div>
        { showHeader && <Header /> }
    </div>
);
```

If showHeader evaluates to true, then the ```<Header/>``` component will be returned by the expression. If showHeader evaluates to false, the ```<Header/>``` component will be ignored, and an empty <div> will be returned.

Consider the following expression:

```react
{
  view
  ? null
  : (
    <p>
      <input
        onChange={this.handleChange}
        value={this.state.inputText} />
    </p>
  )
}
```

The code above can be turned into the following code snippet, as seen in the code below:

```react
!view && (
  <p>
    <input
      onChange={this.handleChange}
      value={this.state.inputText} />
  </p>
)
```

## Useful Videos 

* [React conditional rendering in 7 minutes](https://www.youtube.com/watch?v=4oCVDkb_EIs)

### [Lesson 2. Homework](/Lesson-2/HW-Lesson-2)


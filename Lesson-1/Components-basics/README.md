### Components. Class and functional components

JavaScript supports functions allowing reusable pieces of business logic to be inserted into larger chunks of code. This hides complexity and illustrates the concept of a subroutine.

React components serve the same purpose, except React components effectively divide the UI into reusable components that return HTML. In a sense, React components are subroutines for user interfaces.

A brief introduction to React components from the documentation: 
_"The simplest way to define a component in React is to write a JavaScript function:_

```react
 function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
} 
```

_It’s just a function which accepts props and returns a React element._
_But you can also use the ES6 class syntax to write components:_ 

```react
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

_Both versions are equivalent and will give you the exact same output."_

Class components extend from the React.Component class. React.Component objects have state, meaning the object can hold information that can change over the lifetime of the object. They can also respond to lifecycle methods, like *ComponentDidMount()*, *ComponentDidUpdate()*, and *ComponentWillUnMount()*.

**Note:** Lifecycle methods enable updated state information to trigger a re-render, which updates the DOM with revised HTML markup.

### Differences between functional and class-Components

The most obvious one difference is the syntax. A functional component is just a plain JavaScript function which accepts props as an argument and returns a React element.

A class component requires you to extend from React.Component and create a render function which returns a React element. This requires more code but will also give you some benefits which you will see later on.

### But why should I use functional components at all?

You might ask yourself why you should use functional components at all, if they remove so many nice features. But there are some benefits you get by using functional components in React:

* Functional component are much easier to read and test because they are plain JavaScript functions without state or lifecycle-hooks
* You end up with less code
* They help you to use best practices. It will get easier to separate container and presentational components because you need to think more about your component’s state if you don’t have access to setState() in your component
* The React team mentioned that there may be a performance boost for functional component in future React versions

## Useful Links

* [Comparing class and functional components](https://www.educative.io/blog/react-component-class-vs-functional)
* [React lifecycle methods diagram](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

### [Lesson 1. Homework](/Lesson-1/HW-Lesson-1)
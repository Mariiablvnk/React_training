## Lesson 2

### Props & state

What are props?
Props is short for properties and they are used to pass data between React components. React’s data flow between components is uni-directional (from parent to child only).

How do you pass data with props?
Here is an example of how data can be passed by using props:

```react
class ParentComponent extends Component {    
    render() {    
        return (        
            <ChildComponent name="First Child" />    
        );  
    }
}
```

```react
const ChildComponent = (props) => {    
    return <p>{props.name}</p>; 
};
```

Firstly, we need to define/get some data from the parent component and assign it to a child component’s “prop” attribute.

```react
<ChildComponent name="First Child" />
```

“Name” is a defined prop here and contains text data. Then we can pass data with props like we’re giving an argument to a function. And finally, we use dot notation to access the prop data and render it:

```react
const ChildComponent = (props) => {  
  return (
    <p>{props.name}</p>
  )
};
```


What is state?
React has another special built-in object called state, which allows components to create and manage their own data. So unlike props, components cannot pass data with state, but they can create and manage it internally.

Here is an example showing how to use state:

```react
class Test extends React.Component {    
    constructor() {    
        this.state = {      
            id: 1,      
            name: "test"    
        };  
    }    
    
    render() {    
        return (      
            <div>        
              <p>{this.state.id}</p>        
              <p>{this.state.name}</p>      
            </div>    
        );  
    }
}
```

How do you update a component’s state?
State should not be modified directly, but it can be modified with a special method called setState( ).

```react
this.state.id = “2020”; // wrong

this.setState({         // correct  
    id: "2020"
});
```


What happens when state changes?
OK, why must we use setState( )? Why do we even need the state object itself? If you’re asking these questions, don't worry.

A change in the state happens based on user-input, triggering an event, and so on. Also, React components (with state) are rendered based on the data in the state. State holds the initial information.

So when state changes, React gets informed and immediately re-renders the DOM – not the whole DOM, but only the component with the updated state. This is one of the reasons why React is fast.

And how does React get notified? You guessed it: with setState( ). The setState( ) method triggers the re-rendering process for the updated parts. React gets informed, knows which part(s) to change, and does it quickly without re-rendering the whole DOM.

## Useful Videos (Highly recommend!)

* [React hooks explained](https://www.youtube.com/watch?v=O6P86uwfdR0)
* [Learn to use State in React](https://www.youtube.com/watch?v=kkuq0gTGRFQ)

### [Next part. Conditional rendering](/Lesson-2/Conditional-rendering/)

## Lesson-3
### React Hooks 

With React Hooks, we can isolate stateful logic and side-effects from a functional component. Hooks are JavaScript functions that manage the state's behaviour and side effects by isolating them from a component.

So, we can now isolate all the stateful logic in hooks and use (compose them, as hooks are functions, too) into the components.

The question is, what is this stateful logic? It can be anything that needs to declare and manage a state variable locally.
For example, the logic to fetch data and manage the data in a local variable is stateful. We may also want to reuse the fetching logic in multiple components.

**So, What Exactly Are React Hooks?**
So, how can we define React Hooks in plain English? Now that we understand functions, composability, components, states, and side-effects, here goes a definition of React Hooks:

React Hooks are simple JavaScript functions that we can use to isolate the reusable part from a functional component. Hooks can be stateful and can manage side-effects.
React provides a bunch of standard in-built hooks:

* ```useState:``` To manage states. Returns a stateful value and an updater function to update it.
* ```useEffect:``` To manage side-effects like API calls, subscriptions, timers, mutations, and more.
useContext: To return the current value for a context.
useReducer: A useState alternative to help with complex state management.
* ```useCallback:``` It returns a memorized version of a callback to help a child component not re-render unnecessarily.
useMemo: It returns a memoized value that helps in performance optimizations.
* ```useRef:``` It returns a ref object with a .current property. The ref object is mutable. It is mainly used to access a child component imperatively.
* ```useLayoutEffect:``` It fires at the end of all DOM mutations. It's best to use useEffect as much as possible over this one as the useLayoutEffect fires synchronously.
* ```useDebugValue:``` Helps to display a label in React DevTools for custom hooks.

You can read about these hooks in more detail from [here](https://legacy.reactjs.org/docs/hooks-reference.html). Please notice that each of these hook names start with use. Yes, this is a standard practice to identify a hook in the React codebase quickly.

We can also create custom hooks for our unique use cases like data fetching, logging to disk, timers, and many more.

So next time, if you encounter React Hooks in a codebase or are asked to write one, take it easy. It is just another JavaScript function to deal with state and side-effects outside of functional components.

If you are looking for a step-by-step guide to design and create a custom hook, you may find [this article](https://blog.greenroots.info/how-to-create-a-countdown-timer-using-react-hooks) helpful.

## Useful Links
* [An intro to React Hooks](https://www.youtube.com/watch?v=CvNvRaS3u60&ab_channel=tapaScriptbyTapasAdhikary)

### [Next part - React Forms](/Lesson-3/React%20Forms/)
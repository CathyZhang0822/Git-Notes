# Hooks and Function Components
**Hooks 不能用在classes里面！！！**
As a reminder, function components look like this:   
```javascript
const Exampole = (props) => {
  // You can use Hooks here!
  return <div />;
}
```

or this:   
```javascript
function Example(props) {
  // You can use Hooks here!
  return <div />;
}
```
**所以只能存在于function components里面！！ 但是注意function components不存在生命周期！！！！**
# useState()
官方文档：https://reactjs.org/docs/hooks-state.html   
一个example:
```js
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
**What does useState return?**    
It returns a pair of values: **the current state** and **a function that updates it**. This is why we write `const [count, setCount] = useState()`. This is similar to `this.state.count` and `this.setState` in a class, except you get them in a pair. If you’re not familiar with the syntax we used, we’ll come back to it at the bottom of this page.

**What do we pass to useState as an argument?**    
**The only argument to the `useState()` Hook is the initial state.** Unlike with classes, the state doesn’t have to be an object. We can keep a number or a string if that’s all we need. In our example, we just want a number for how many times the user clicked, so pass 0 as initial state for our variable. (If we wanted to store two different values in state, we would call useState() twice.)

# useSelector()    
在学习这条之前你需要了解reduxe store和它相关的dispatching functions!
```js
const result : any = useSelector(selector : Function, equalityFn? : Function)
```
这个是干啥的呢？就是从redux的store对象中提取数据(state)。   
`useSelector`会订阅`store`, 当`action`被`dispatched`的时候，会运行`selector`。    
一个简单的例子：   
```
import React from 'react'
import { useSelector } from 'react-redux'

export const CounterComponent = () => {
  const counter = useSelector(state => state.counter)
  return <div>{counter}</div>
}
```

# useDispatch()
```js
const dispatch = useDispatch()
```
This hook returns a reference to the dispatch function from the Redux store. You may use it to dispatch actions as needed.    
就是那个 `store.dispatch()`  
就是store它自己的那个basic dispatch function,可以拿过来用，来改变state？   

# useMemo()
```
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```
Returns a memoized value.   
Pass a “create” function and an array of dependencies. `useMemo` will only recompute the memoized value when one of the dependencies has changed. This optimization helps to avoid expensive calculations on every render. 

# useCallback
```javascript
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```
Returns a memorized callback.   
Pass an inline callback and an array of dependencies. `useCallback` will return a meomoized version of the callback that only changes if one of the dependecies has changed.    
`useCallback(fn, deps)` is equivalent to `useMemo(() => fn, deps)`.  

# useEffect 
**The function passed to useEffect will run after the render is committed to the screen.**   
```javascriipt
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    // Clean up the subscription
    subscription.unsubscribe();
  };
});  
```
也可以 Conditionally firing an effect！！ 
```javascript
useEffect(
  () => {
    const subscription = props.source.subscribe();
    return () => {
      subscription.unsubscribe();
    };
  },
  [props.source],
);
```
这样在 `props.source` 改变后才会fire useEffect里的函数！！！ 




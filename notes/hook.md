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

# useMemo()
```
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```
Returns a memoized value.   
Pass a “create” function and an array of dependencies. `useMemo` will only recompute the memoized value when one of the dependencies has changed. This optimization helps to avoid expensive calculations on every render.   

# Store
https://redux.js.org/api/store
A store holds the whole state tree of your application. The only way to change the state inside it is to dispatch an action on it.   
A store is not a class. It's just an object with a few methods on it. To create it, pass your *root reducing function* to *createStore()*.    
   
需要着重理解的几个概念：   
1. Redux Store 本身
2. Reducer functions
3. store.dispatch 和 Dispatch Functions之间的区别

## createStore()
https://redux.js.org/api/createstore
Creates a Redux store that holds the complete state tree of your app. **There should only be a single store in your app.**    
   
**Arguments:**  
1. Reducer (Function): A reducing function that returns the next state tree, given the current state tree and an action to handle.   
2. [perloadedState] (any): The initial state. 
3. [enhancer] (Function): The store enhancer. You may optionally specify it to enhance the store with third-party capabilities such as middleware, time travel, persistence, etc. The only store enhancer that ships with Redux is `applyMiddleware()` (这个好像在哪里看到过).

**Returns:**  
Store: An object that holds the complete state of your app. The only way to change its state is by `dispatching actions`. You may also `subscribe` to the changes to its state to update the UI.     
Example:    
```
import { createStore } from 'redux'

function todos(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return state.concat([action.text])
    default:
      return state
  }
}

const store = createStore(todos, ['Use Redux'])

store.dispatch({
  type: 'ADD_TODO',
  text: 'Read the docs'
})

console.log(store.getState())
// [ 'Use Redux', 'Read the docs' ]
```
## Reducer
https://redux.js.org/glossary#reducer
`type Reducer<S, A> = (state: S, action: A) => S`
A reducer (also called a reducing function) is a function that accepts an accumulation and a value and returns a new accumulation. They are used to reduce a collection of values down to a single value.    
Reducers 不是redux里面特有的，它是一个基础概念。    
In Redux, the accumulated value is the state object, and the values being accumulated are actions.

## store.dispatch vs Dispatch Functions
store.dispatch 用来dispatch an action. 这是改变store state的唯一方式。    

dispatch functions: https://redux.js.org/glossary#dispatching-function   没懂

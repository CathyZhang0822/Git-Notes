# Store
https://redux.js.org/api/store
A store holds the whole state tree of your application. The only way to change the state inside it is to dispatch an action on it.   
A store is not a class. It's just an object with a few methods on it. To create it, pass your *root reducing function* to *createStore()*.    
   
需要着重理解的几个概念：   
1. Redux Store 本身
2. Reducer functions
3. Dispatch action

### createStore()
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


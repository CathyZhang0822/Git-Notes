# Store
https://redux.js.org/api/store   
**A store holds the whole state tree of your application. The only way to change the state inside it is to dispatch an action on it.**   
A store is not a class. It's just an object with a few methods on it. To create it, pass your **root reducing function** to **createStore()**.    
   
需要着重理解的几个概念：   
1. Redux Store 本身
2. Reducer functions
3. store.dispatch 和 Dispatch Functions之间的区别   
（注意这里！！！ 每个reduxe store都有一个base dispatch functions! 在`createStore`的时候就定义好了。除此之外，还有广泛意义上的`dispatching functions`。）

## createStore()
https://redux.js.org/api/createstore
Creates a Redux store that holds the complete state tree of your app. **There should only be a single store in your app.**    
   
**Arguments:**  
就pass三个东西：
1. Reducer（就是reducing function），用来改变state（store.dispatch(...)就是运行这个reducing function!）和 return next state tree. 注意！即使我们说是 “state tree”，但是 `state`可以是any type!! 比如array   
2. The initial state.
3. The store enhancer. 跟middleware...之类的有关    
#### 以下是官网英文解释：   
1. Reducer (Function): A reducing function that returns the next state tree, given the current state tree and an action to handle.（可以理解store本身的reducer就是我们说的那个base reducing function吗）   
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
### Reducer    
这里详细解释下上面说的reducer (reducing function)
https://redux.js.org/glossary#reducer   
`type Reducer<S, A> = (state: S, action: A) => S`
A reducer (also called a reducing function) is a function that accepts an accumulation and a value and returns a new accumulation. They are used to reduce a collection of values down to a single value.    
Reducers 不是redux里面特有的，它是一个基础概念。    
In Redux, the accumulated value is the state object, and the values being accumulated are actions.
例子：    
就是上面介绍 `createStore` 里的   
```
function todos(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return state.concat([action.text])
    default:
      return state
  }
}
```

## store.dispatch vs Dispatch Functions
store.dispatch 用来dispatch an action. 这是改变store state的唯一方式。    

dispatch functions: https://redux.js.org/glossary#dispatching-function   没懂   

# Store Methods
## getStage()
Returns the current state tree of your application. It's equal to the last value returned by the store's reducer.   
顾名思义，就是return最新的state。也就是reducer 返回的最后一个value.

## dispatch(action)   
Dispatches an action. This is the only way to trigger a state change.   
注意！这里总结两种用法。一种是直接传入action arg,这种情况直接call store自己本身的dispatching functions。还有一只是传入别的dispatching functions。例子：   
```
import { createStore } from 'redux'
const store = createStore(todos, ["Use Redux"]);

//第一种
store.dispatch({
 type: "ADD_TODO",
 text: "Read the docs1"
});

function addTodo(text) {
 return {
   type: "ADD_TODO",
   text
 };
}

//第二种
store.dispatch(addTodo("Read the docs"));
store.dispatch(addTodo("Read about the middleware"));
// ["Use Redux", "Read the docs1", "Read the docs", "Read about the middleware"]
console.log(store.getState());
```

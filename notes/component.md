# Components and Props

## Function 和 class都可以构成 Component
```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

如何用Component!! （基本都是这个样子 `<ComponentExample prop1=xxx prop2=xxx />`    
```
const element = <Welcome name="Sara" />;
```

## React.Component
**我们还是更建议用ES6 class**

The only method you must define in a `React.Component` subclass is called `render()`. All the other methods described on this page are optional.

## Props are Read-Only
Whether you declare a component as a function or a class, it must never modify its own props.   
All React components must act like pure functions with respect to their props.   
可以把props理解成

# State and Lifecycle

## Adding local state to a Class
```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

## Lifecycle
There is a lifecycle cheatsheet: https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/   
![lifecycle](https://user-images.githubusercontent.com/36396754/100670138-4f22ad80-3313-11eb-8786-681cdf7d6ac7.png)
补充常用lifecycle methods: https://reactjs.org/docs/react-component.html#constructor ...

  ### Mounting
  These methods are called in the following order when an instance of a componenet is being created and inserted into the DOM:   
  * **constructor()**
  * static getDerivedStateFromProps()
  * **render()**
  * **componentDidMount()**

    #### constructor()
    ```
    contructor(props)
    ```
    **If you don't initialize state and you don't bind methods, you don't need to implement a constructor for your React component.**   
    ```javascript
    constructor(props) {
      super(props);
      // Don't call this.setState() here!
      this.state = { counter: 0 };
      this.handleClick = this.handleClick.bind(this);
    }
    ```
    #### componentDidMount()
    `componentDidMount()` is invoked immediately after a component is mounted **(inserted into the tree).**    
    If you need to load data from a remote endpoint, this is a good plance to instantiate the network request.
    This method is a good place to setup any subscription. If you do that, don't forget to unsubscrite in `componentWillUnmount()`.    
    
  ### Updating
  An update can be caused by changes to props or state. These methods are called in the following order when a component is being re-rendered:   
  * static getDerivedStateFromProps()
  * shouldComponentUpdate()
  * **render()**
  * getSnapshotBeforeUpdate()
  * **componentDidUpdate()**
    #### componentDidUpdate()
    ```javascript
    componentDidUpdate(prevProps, prevState, snapshot)
    ```
    This is also a good place to do network requests as long as you compare the current props to previous props. (eg. a network request may not be neccesaary if the propss has not changed)   
    ```javascript
    componentDidUpdate(prevProps) {
      // Typical usage (don't forget to compare props):
      if (this.props.userID !== prevProps.userID) {
        this.fetchData(this.props.userID);
      }
    }
    ```
  ### Unmounting
  This method is called when a component is being removed from the DOM.    
   #### componentWillUnmount()
   `compenentWillUnmount` is invoked immediately before a component is unmounted and . Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any subscriptions that were created in `componentDidMount`

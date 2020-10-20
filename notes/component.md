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

# State and Lifecycle

## Adding local state to a Class
```
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

补充常用lifecycle methods: https://reactjs.org/docs/react-component.html#constructor ...

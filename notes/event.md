# Event Handling
在这里我们定义一个function component，就是一个button 吧！   
```
function FunctionClick(){
  return(
    <div>
      <button onClick={clickHandler}>Click</button>
    </div>
  )
}
```
注意`{clickHandler}`不要写成 `{clickHandler{}}`

# Binding Event Handlers
根本原因：this在Javascript的Eventhandler里面是 `undefined`   
举个例子：比如说我想创建一个componet, 里面包含button和text，然后click button text就会变换文字    
```js
import React, { Component } from 'react'

class EventBind extends Component {
  constructor(props) {
    super(props)
    
    this.state = {
      message: 'Hello'
    }
    
   }
   clickHandler(){
      this.setState({
        message: 'Goodbye'
      })
   }
    
    render() {
      return (
        <div>
          <div> {this.state.message} </div>
          <button onClick={this.clickHander}> Click </button>
        </div>
      )
    }
  }
}
```
这样会得到error: Cannot read property 'setState' of undefined. 所以我们必须要bind event handlers!!    
(至于为什么this会是undefined, it's all about JS, not react related)   
有三种binding的方法：   
1. Binding in the render method
`<button onClick={this.clickHander.bind(this)}> Click </button>`
2. Arrow function
`<button onClick={() => this.clickHandker()}> Click </button>`
3. 在constructor里面bind
```
  constructor(props) {
    super(props)
    
    this.state = {
      message: 'Hello'
    }
    this.clickHandler = this.clickHander.bind(this)
   }
```
4. 也是Arrow function和2本质一样
```
   clickHandler = () => {
      this.setState({
        message: 'Goodbye'
      })
   }
```

什么时候需要bind?? **当我们用this keyword的时候**

# Basic Form Handling

Step1: add the html   
Step2: add a new component state and assign it to html(ie:input) value   
Step3: add onChange handler that update the state   

Example:
```javascript
import React, { Component } from "react";
/*
Step1: add the html
Step2: add a new component state and assign it to html(ie:input) value
Step3: add onChange handler that update the state
So onchange handler -> changes state -> update html component's value
 */
export class Form extends Component {
  constructor(props) {
    super(props);

    this.state = {
      username: "",
    };
  }
  // Let's call it a handler
  onUserNameChange = (event) => {
    this.setState({ username: event.target.value });
  };

  handleSubmit = event => {
    alert(`Hello ${this.state.username}`);
  };

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <div>
          <div>
            <label>Username</label>
            <input
              type="text"
              value={this.state.username}
              onChange={this.onUserNameChange}
            />
          </div>
        </div>
      </form>
    );
  }
}

export default Form;

```

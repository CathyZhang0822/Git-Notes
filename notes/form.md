# Basicis of Form Handling
基本思路：
![silu](https://user-images.githubusercontent.com/36396754/123601035-12853a80-d7ac-11eb-98be-c84bdd287d4f.png)


## Class Component
```javascript
import React, { Component } from "react";

export class Form extends Component {
  constructor(props) {
    super(props);

    this.state = {
      username: "",
    };
  }

  onUserNameChange = (event) => {
    this.setState({ username: event.target.value });
  };

  render() {
    return (
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
    );
  }
}

export default Form;
```

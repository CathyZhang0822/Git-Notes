# Condition Rendering

### if/else
1. Adding if/else statements within the JSX is not valid   
只能用于JS logic里面！比如：   
```javascript
  render() {
    if (this.state.isLoggedIn) {
      return <div>Hello Yuelin</div>;
    } else {
      return <div>Welcome Guest</div>;
    }
  }
  ```

### Ternary
```javascript
    return this.state.isLoggedIn ? (
      <div>Welcome Yuelin</div>
    ) : (
      <div>Welcome Guest</div>
    );
```
### special method: short circuit (短路）
`return this.state.isLoggedIn && <div>Welcome Yuelin</div>;`

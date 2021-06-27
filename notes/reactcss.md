# Styling React Components

1. CSS Stylesheets
就是创建css file，并且import 它。 比如：
```
import "./App.css";
```
2. Inline styling
使用html component里面的style parameter，传入一个object
比如：
```
import React from "react";

const heading = {
  // The key is CSS name but in camel case
  fontSize: "72px",
  color: "blue",
};
function Inline() {
  return (
    <div>
      <h1 style={heading}>Inline Styling</h1>
    </div>
  );
}

export default Inline;
```
3. CSS Modules
跟第一个类似，不过后缀名是 `xxx.module.css`. 优点就是locally 使用，避免conflicts.
比如：
```
import styles from "./components/appStyle.module.css";
...
<h1 className={styles.success}>Success</h1>
...
```

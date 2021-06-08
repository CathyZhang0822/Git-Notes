# List Rendering
1. `map()`传入的是method!
2. 在JSX (html)里面运用到JS的variables的时候要用括号！`{}`   
```javascript
import React from "react";

function NameList() {
  const persons = [
    { id: 1, name: "Bruce", age: 30, skill: "React" },
    { id: 2, name: "Clark", age: 25, skill: "Angular" },
    { id: 3, name: "Diana", age: 28, skill: "Vue" },
  ];
  const personList = persons.map((person) => <h2>{person.name}</h2>);
  return <div>{personList}</div>;
}

export default NameList;
```

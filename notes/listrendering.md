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
# List and Keys
有时候我们会看到这样的warning msg: "Each child in an array or iterator should have a unique 'key' prop"   
怎样理解：
1. 在array的每个item都要有一个 `key` prop. 而且是只能上游传入！不能下游access! 
2. 并且每个item的`key`value都要是unique的  
可以这样：`const personList = persons.map(person => <Person key={person.id} person={person} />)`

# Index as Key Anti-pattern
前面讲到传入`map()`的是个method，这个method就是takes in child，然后去对child进行操作。   
但是这个map method也可以传入index param, 并且我们可以用这个index param作为child的key. 比如：  
```
const names = ['A', 'B', 'C']
const nameList = names.map((name, index) => <h2 key={index}>{name}</h2>)
```
但是不建议这么用！会有问题。 https://www.youtube.com/watch?v=xlPxnc5uUPQ&list=PLC3y8-rFHvwgg3vaYJgHGnModB54rxOk3&index=19 for more info.  
When to use index as a key?   
1. The items in your list do not have a unique id. (If items have a unique id, always go with it)   
2. The list is as static list and will not change. (You are never adding items or removing items)
3. The list will never be reordered or filtered.

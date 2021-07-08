# Component Lifecycle
1. Life cycle methods only exist in the class components, BUT Hook can make this kind of method exist in Functional Components.
2. Mouting, Updating, Unmounting and Error Handling
3. List of functions of cycling methods


## Mounting Methods
主要有三个：
1. `constructor()`：
不允许side effects (比如Ajax calls)。可以直接通过 `this.state` 赋值。必须要有`super(props)`
2. `render()`
3. `componentDidMount()`:
Invoked immediately after a component and all its children components have been rendered to the DOM. 允许side effencts，比如ajax calls

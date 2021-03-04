# 一些基础知识点总结
https://www.youtube.com/channel/UC80PWRj_ZU8Zu0HSMNVwKWw - 看的这位宝藏博主的教学视频

# Create a new app
1. 记住React是一个js的library, 不是一个framework!
2. `npx create-react-app hello-world`

# Folder structure
1. public folder 里面有一个 `index.html`，这是整个app唯一(?)的一个Html。因为我们要全权让React来render html的body。   
在 `index.html` 里面有一个id为root的div:   
```
<div id="root"></div>
```
React在`index.js`来操作它：   
```
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```
# Functional Components
1. 就是javascript functions. Input: `Props`. Outpu: html (JSX)
2. 这里终于了解了import/export 名称不match的情况！
假如说我们有另一个file里面定义了一个 `Greet` component，但是有default export (id: `export default Greet`). 这时候我们在另一个file来Import它的时候，可以不用 `Greet`这个名字，也可以不用大括号，比如 `import Component2 from ./components/Greet`      
但是如果我们在`Greet.js`里面最后写了 `export const Greet`. 那我们import的时候必须也要用 `import { Greet } from "./components/Greet"`. 也要注意有括号和没括号的区别！   

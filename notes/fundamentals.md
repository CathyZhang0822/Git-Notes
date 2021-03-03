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

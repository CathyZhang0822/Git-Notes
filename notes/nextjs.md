# Pages
https://nextjs.org/docs/basic-features/pages   
In Next.js, a **page** is a React Component exported from a `.js`, `.jsx`, `.ts`, or `.tsx` file in the pages directory. Each page is associated with a route based on its file name.   

**Example**: If you create `pages/about.js` that exports a React component like below, it will be accessible at `/about`.
```
function About() {
  return <div>About</div>
}

export default About
```


# Routing
https://nextjs.org/docs/routing/introduction    
Next.js has a file-system based router built on the **concept of pages**.

When a file is added to the **`pages`** directory it's automatically available as a route.

The files inside the **pages** directory can be used to define most common patterns.

### Index routes
The router will automatically route files named `index` to the root of the directory.
```js
pages/index.js → /
pages/blog/index.js → /blog
```

### Nexted routes   
The router supports nested files. If you create a nested folder structure files will be automatically routed in the same way still.
```
pages/blog/first-post.js → /blog/first-post
pages/dashboard/settings/username.js → /dashboard/settings/username
```
还有Dynamic route segments这里就不说了

# next/router
通过了解以上两个，我们就可以继续学习 `useRouter` hook   
https://nextjs.org/docs/api-reference/next/router   
Nextjs提供了一个`next/router`的包，专门用来处理路由。Router便是其中一个对象，`Router.push('url')`进行跳转。
实践一下：
1. pages目录下，创建index.js文件   
```js
import React from 'react'     
import Router from 'next/router'

export default () => {
    return(
        <>
            <button onClick={()=>Router.push('/demo')} >送我去demo页</button>
            <div>这里是主页</div>
        </>
    )
}
```
2. 修改demo.js文件   
```
import React from 'react'    
import Router from 'next/router'

export default () => {
    return(
        <>
            <button onClick={()=>Router.push('/')} >送我去主页</button>
            <div>这里是demo页</div>
        </>
    )
}
```
这样就可以在两个页面直接互相跳转了~ 可以想象吧！ reference: https://zhuanlan.zhihu.com/p/95893775    

### router object 
The following is the definition of the router object returned by both useRouter and withRouter:
```
pathname: String - Current route. That is the path of the page in /pages
query: Object - The query string parsed to an object. It will be an empty object during prerendering if the page doesn't have data fetching requirements. Defaults to {}
asPath: String - Actual path (including the query) shown in the browser
```
比如说我们想在routes里面加入params。ie: `/post/:id`, `/post/:id/:comment`.这里就要用到Dynamic Routes (https://nextjs.org/docs/routing/dynamic-routes)   
很好的例子： https://github.com/vercel/next.js/tree/canary/examples/dynamic-routing  
    
Defining routes by using predefined paths is not always enough for complex applications. In Next.js you can add brackets to a page ([param]) to create a dynamic route (a.k.a. url slugs, pretty urls, and others).    
Consider the following page `pages/post/[pid].js`:
```js
import { useRouter } from 'next/router'

const Post = () => {
  const router = useRouter()
  const { pid } = router.query

  return <p>Post: {pid}</p>
}

export default Post
```
Any route like `/post/1`, `/post/abc`, etc. will be matched by pages/post/[pid].js. The matched path parameter will be sent as a query parameter to the page, and it will be merged with the other query parameters.   
For example, the route `/post/abc` will have the following query object:   
```js
{ "pid": "abc" }
```
Similarly, the route `/post/abc?foo=bar` will have the following query object:
```js
{ "foo": "bar", "pid": "abc" }
```

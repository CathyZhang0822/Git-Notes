## Pages
https://nextjs.org/docs/basic-features/pages   
In Next.js, a **page** is a React Component exported from a `.js`, `.jsx`, `.ts`, or `.tsx` file in the pages directory. Each page is associated with a route based on its file name.   

**Example**: If you create `pages/about.js` that exports a React component like below, it will be accessible at `/about`.
```
function About() {
  return <div>About</div>
}

export default About
```


## Routing
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

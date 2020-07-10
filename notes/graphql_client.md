# Hook up your graph to Apollo Client

## Apollo Client

**Server <-> Client <-> React**   
创建一个Apollo Client, 然后这个client 来 send GraphQL queries to Apollo Server (server就是教程上半部分讲的那个，我们写了很多 types 和 resolvers)。   
获得data之后，client再把

那些auto generated files:   
To generate TypeScript types for your queries and mutations, open another terminal window and run `npm run codegen`. This will watch for changes to your code and generate the client-side typings.

## The useQuery hook

In this section, we'll learn how to use the `useQuery` hook from `@apollo/react-hooks` to fetch more complex queries and execute features like pagination.   
To create a component with `useQuery`, `import useQuery from @apollo/react-hooks`, pass your query wrapped with `gql` in as the first parameter, then wire your component up to use the loading, data, and error properties on the result object to render UI in your app.    

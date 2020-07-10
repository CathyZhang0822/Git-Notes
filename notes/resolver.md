# Write query resolvers
https://www.apollographql.com/docs/tutorial/resolvers/   
A resolver is a function that's responsible for populating the data for a single field in your schema.    

Resolver function looks like this:   
```
fieldName: (parent, args, context, info) => data;
```
可以这么理解：   
对于我们定义的object types, query types等等。每一个field是怎么fetch data的。类似于 `KEY_MAP_FUNCTION`， resolver就是那个function!    
例子：
这里有一个定义好的Query type
```js
type Query {
  launches: [Launch]!
  launch(id: ID!): Launch
  me: User
}
```
对应的resolver:   
```js
Query: {
  launches: (_, __, { dataSources }) =>
    dataSources.launchAPI.getAllLaunches(),
  launch: (_, { id }, { dataSources }) =>
    dataSources.launchAPI.getLaunchById({ launchId: id }),
  me: (_, __, { dataSources }) => dataSources.userAPI.findOrCreateUser()
}
```

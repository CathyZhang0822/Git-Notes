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
对应的resolver: （**我觉得就可以把resolver理解成 `KEY_FUNCTION_MAP`!**）(定义的 `Query Type`可以理解为`KEY_RETURN-TYPE_MAP`)
```js
Query: {
  launches: (_, __, { dataSources }) =>
    dataSources.launchAPI.getAllLaunches(),
  launch: (_, { id }, { dataSources }) =>
    dataSources.launchAPI.getLaunchById({ launchId: id }),
  me: (_, __, { dataSources }) => dataSources.userAPI.findOrCreateUser()
}
```

**注意分清以上的 `Query` 和 graphql UI里输入的query的区别！！**   
`Query`是我们在schema里面定义的一个 `Query Type`
我在graphql UI里面输入一个query:   
```
query GetLaunchById {
  launch(id: 60) { # 注意这里的launch，是我们定义Query Type里面的一个field!!!!!!!  下面的data，就是这个field对应的resolver 来fetch的  
    id
    rocket {
      id
      type
    }
  }
}# Write your query or mutation here
```
得到：   
```
{
  "data": {
    "launch": {
      "id": "60",
      "rocket": {
        "id": "falcon9",
        "type": "FT"
      }
    }
  }
}
```

# 写 Graphql query 
如何填充 `gql'...'`?
```js
const { gql } = require('apollo-server');

const typeDefs = gql`
  # Your schema will go here
`;

module.exports = typeDefs;
```

## 第一种 Object Types   
```js
type Rocket {
  id: ID!
  name: String
  type: String
}

type User {
  id: ID!
  email: String!
  trips: [Launch]!
}

type Mission {
  name: String
  missionPatch(size: PatchSize): String
}

enum PatchSize {
  SMALL
  LARGE
}
```
`!` 感叹号代表不能为`null`

## 第二种 The `Query` type
```
type Query {
  launches: [Launch]!
  launch(id: ID!): Launch
  me: User
}
```
This `Query` type defines three available queries for clients to execute: `launches`, `launch`, and `me`.

- The `launches` query will return an array of all upcoming Launches.
- The `launch` query will return a single Launch that corresponds to the **`id` argument provided to the query**.
- The `me` query will return details for the User that's currently logged in.   
所以这个query type 和 object type 有啥区别?
1. query 支持传入argument
2. query（前者）是用来fetch object（后者）的？
## 第三种 The `Mutation` type
**Queries enable clients to fetch data, but not to modify data**. To enable clients to modify data, our schema needs to define some `mutations`.
```js
type Mutation {
  bookTrips(launchIds: [ID]!): TripUpdateResponse!
  cancelTrip(launchId: ID!): TripUpdateResponse!
  login(email: String): String # login token
}
type TripUpdateResponse {
  success: Boolean!
  message: String
  launches: [Launch]
}
```
This Mutation type defines three available mutations for clients to execute: `bookTrips`, `cancelTrip`, and `login`.
可以把mutations理解成functions吗？（update: 不可以，更像是只有首尾的function。去除掉了中间的逻辑。[因为中间的逻辑由resolver来写]）定义了take in和return的type.
# 深入理解 Query Type 和 Mutation Type
我乍一看它们两个觉得很像，都像是只有首尾的function,规定了输入和输出的type。
这里又涉及一个新的概念`Query`，GraphQL中使用`Query`来抽象数据的查询逻辑，当前标准下，有三种查询类型，分别是`query`（查询）、`mutation`（更改）和`subscription`（订阅）。   
- query（查询）：当获取数据时，应当选取Query类型
- mutation（更改）：当尝试修改数据时，应当使用mutation类型
 - subscription（订阅）：当希望数据更改时，可以进行消息推送，使用subscription类型
 发个对比：   
 ```
 query {
  articles(): [Article!]!
  article(id: Int): Article!
}

mutation {
  createArticle(): Article!
  updateArticle(id: Int): Article!
  deleteArticle(id: Int): Article!
}

```
我们可以看到mutation里面的fields都是动词。   

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
## The `Mutation` type
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
可以把mutations理解成functions吗？定义了take in和return的type.

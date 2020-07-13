# Hook up your graph to Apollo Client
https://www.apollographql.com/docs/tutorial/queries/

## Apollo Client

**Server <-> Client <-> React**   
创建一个Apollo Client, 然后这个client 来 send GraphQL queries to Apollo Server (server就是教程上半部分讲的那个，我们写了很多 types 和 resolvers)。   
获得data之后，client再把它们render出来

*那些auto generated files:   
To generate TypeScript types for your queries and mutations, open another terminal window and run `npm run codegen`. This will watch for changes to your code and generate the client-side typings.* （关于codegen，会专门写一篇Note）

## The useQuery hook

In this section, we'll learn how to use the `useQuery` hook from `@apollo/react-hooks` to fetch more complex queries and execute features like pagination.   
To create a component with `useQuery`, `import useQuery from @apollo/react-hooks`, pass your query wrapped with `gql` in as the first parameter, then wire your component up to use the loading, data, and error properties on the result object to render UI in your app.    
例子，首先写一个gql query:
```tsx
export const GET_LAUNCH_DETAILS = gql`
  query LaunchDetails($launchId: ID!) {
    launch(id: $launchId) {
      id
      site
      isBooked
      rocket {
        id
        name
        type
      }
      mission {
        name
        missionPatch
      }
    }
  }
`;
```
再完善Launch函数：   
```tsx
export default function Launch({ launchId }) {
  const { data, loading, error } = useQuery(
    GET_LAUNCH_DETAILS,
    { variables: { launchId } }
  );
  if (loading) return <Loading />;
  if (error) return <p>ERROR: {error.message}</p>;
```
## The useMutation 

## Using fragments to share code
很多gql语句可能会有重复的code, 我们就可以用fragment把重复的部分提取出来。
```tsx
export const LAUNCH_TILE_DATA = gql`
  fragment LaunchTile on Launch {
    id
    isBooked
    rocket {
      id
      name
    }
    mission {
      name
      missionPatch
    }
  }
`;
```
We define a GraphQL fragment by giving it a name (`LaunchTile`) and defining it on a type on our schema (`Launch`). The name we give our fragment can be anything, **but the type must correspond to a type in our schema**.   
运用:   
```tsx
const GET_LAUNCHES = gql`
  query launchList($after: String) {
    launches(after: $after) {
      cursor
      hasMore
      launches {
        ...LaunchTile
      }
    }
  }
  ${LAUNCH_TILE_DATA}
`;
```
对比之前:
```tsx
const GET_LAUNCHES = gql`
  query launchList($after: String) {
    launches(after: $after) {
      cursor
      hasMore
      launches {
        id
        isBooked
        rocket {
          id
          name
        }
        mission {
          name
          missionPatch
        }
      }
    }
  }
`;
```

# Graphql - Connect to data sources
Apollo provides a `DataSource` class that we can extend to fetch data.   
https://www.apollographql.com/docs/tutorial/data-source/    
### Connect a REST API
```js
const { RESTDataSource } = require('apollo-datasource-rest');
// 仔细看一下， OOD 啊！
class LaunchAPI extends RESTDataSource {
  constructor() {
    super();
    this.baseURL = 'https://api.spacexdata.com/v2/';
  }
}
async getAllLaunches() {
  const response = await this.get('launches');
  return Array.isArray(response)
    ? response.map(launch => this.launchReducer(launch))
    : [];
}

async getLaunchById({ launchId }) {
  const response = await this.get('launches', { flight_number: launchId });
  return this.launchReducer(response[0]);
}
module.exports = LaunchAPI;
```
The call to `this.get('launches')` sends a `GET` request to `https://api.spacexdata.com/v2/launches` and stores the array of returned launches in response.   
### Connect a database
略过，看doc吧。用的是`DataSource` 不是`RESTDataSource`    

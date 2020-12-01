# JavaScript Promise Object
A JS Promise object object contains both the producing code and calls to the consuming code:
(所以Promise是一种Object Class，需要给它feed functions？)
```javascript
let myPromise = new Promise(function(myResolve, myReject) {
// "Producing Code" (May take some time)

  myResolve(); // when successful
  myReject();  // when error
});

// "Consuming Code" (Must wait for a fulfilled Promise)
myPromise.then(
  function(value) { /* code if successful */ },
  function(error) { /* code if some error */ }
);
```
When the executing code obtains the result, it should call one of the two callbacks:
1. Success -> myResolve(result value)
2. Error -> myReject(error object)

## Promise Object Properties
A JavaScript Promise object can be:
* Pending
* Fulfilled
* Rejected

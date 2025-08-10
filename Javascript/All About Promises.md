

============================================

1. **`.then()` Method**: The `.then()` method is only available on a Promise object. It is used to handle the result of a Promise. The `.then()` method takes two optional parameters: a `resolve` callback for handling successful resolution and a `reject` callback for handling rejections. `.then()` returns a new Promise, which resolves or rejects based on the returned value of the `resolve` or `reject` callback.

The function `resolve1` in  example simply returns `'returnvalue'`. This value is automatically wrapped in a Promise by the `.then()` method, so `resolve1` does not directly return a value but rather returns a new Promise that resolves with `'returnvalue'`. And this was the promise that we were saying .then() returns.

3. **Parameters of `.then()`**: The `.then()` method takes two arguments:
   - **`resolve` Callback**: Called with the value from the resolved Promise.
   - **`reject` Callback**: Called with the reason for the rejection of the Promise.

4. **Handling Promise Values**: When a Promise is resolved or rejected, the attached `.then(resolve, reject)` methods will receive the resolved value or rejection reason as their parameters.

5. **Return Value of `resolve`**: The `resolve` callback in `.then()` can return either a new Promise or a non-Promise value:
   - **New Promise**: The next `.then()` will wait for this new Promise to resolve or reject.
   - **Non-Promise Value**: The next `.then()` will receive this value directly and use it as the resolved value.

6. **Parameter Source of the First `.then()`**: The `resolve` callback of the first `.then()` receives the value from the initial Promise's resolution or rejection.

7. **Parameter Source of Chained `.then()`**: The `resolve` callback of chained `.then()` methods receives the value returned by the previous `resolve` callback or the resolved value of the previous Promise.

8. **Error Handling in Chained `.then()`**: In a chain of `.then()` calls, if a previous `resolve` callback throws an error, returns a rejected Promise, or returns a value that implicitly represents an error (e.g., `undefined` in some cases), the subsequent `.then()` will receive this as a rejection and the `reject` callback will be triggered.

### Example in Context

Given the previous example:

```javascript
let promise1 = getWeather(); // Initial Promise

promise1
  .then(resolve1, reject1) // First .then()
  .then(resolve2, reject2); // Chained .then()

let resolve1 = () => { return 'returnvalue'; } // Returns a non-Promise value
let reject1 = (error) => { console.log('Reject1:', error); return Promise.reject('Error in Reject1'); } // Returns a rejected Promise
let resolve2 = (value) => { console.log('Resolve2:', value); } // Receives value from resolve1 or reject1
let reject2 = (error) => { console.log('Reject2:', error); } // Receives value from reject1
```

- **`.then()` method is only available on Promise objects**, and **`.then()` returns a new Promise** based on the value returned by the `resolve` or `reject` callback.
- **`.then()` takes two parameters**: a `resolve` callback and a `reject` callback.
- **If the Promise is resolved or rejected**, the `resolve` or `reject` callback in `.then()` will receive the Promise's resolved value or rejection reason.
- **The `resolve` callback can return a new Promise or a non-Promise value**.
- **The first `.then()`'s `resolve` receives the value from the initial Promise's resolution or rejection**.
- **In chained `.then()`, the `resolve` callback receives the value from the previous `resolve` callback**.
- **If the previous `resolve` callback throws an error, returns a rejected Promise, or implicitly represents an error (e.g., `undefined`), the next `.then()` will handle it as a rejection**.
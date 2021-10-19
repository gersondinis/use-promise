# @grd/usePromise()
Simple react hook to handle promises

#### Note: It works with any `Promise` implementation, but this documentation uses `axios` for demonstration.

#### Dependency: `react@>16.8.0`

## Get started:
### Install
```bash
yarn add @grd/use-promise;
```
### Import
```js
import usePromise from '@grd/use-promise';
```
### Use
```js
const [invokeFn, {result, error, isLoading}] = usePromise((arg) => Promise(arg))
```
<hr/>

### Example A - invoked on demand:
```js
import { usePromise } from '@grd/use-promise';


export const ExampleA = () => {
  
  const [getUser, {result, error, isLoading}] = usePromise(userId => axios.get(`/users/${userId}`));
  
  return (
    <>
      <button onClick={() => getUser(1)}>Retrieve User</button>
      {result && <p>Hello {result.data?.user?.name}</p>}
      {error && <p>Whoops: {error.message}!</p>}
      {isLoading && <p>loading...</p>}
    </>
  );
};
```

### Example B - invoked on load:
```js
import { usePromise } from '@grd/use-promise';
import { useEffect } from 'react';


export const ExampleB = () => {
  
  const [getUser, {result, error, isLoading}] = usePromise(userId => axios.get(`/users/${userId}`));

  useEffect(() => {
    getUser(1);
  }, [getUser]);
  
  return (
    <>
      {result && <p>Hello {result.data?.user?.name}</p>}
      {error && <p>Whoops: {error.message}!</p>}
      {isLoading && <p>loading...</p>}
    </>
  );
};
```

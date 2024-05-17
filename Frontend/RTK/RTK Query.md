Here's your text formatted as markdown:
Links - [[Custom BaseQuery func]], [[Conditional Fetching]], [[redux store namastereact.pdf]]
Redux Toolkit Main framework - [[redux store namastereact.pdf]]



---
tutorial link - [[Mastering Redux Toolkit Query: A Comprehensive Guide | What About Coding](https://whataboutcoding.com/rtk-query-toolkit/)]()
## What is RTK Query

![RTK Query](https://whataboutcoding.com/wp-content/uploads/2023/10/image-2-1024x164.png)

In simple words, RTK Query is an extension of Redux Toolkit that simplifies data fetching and caching in your application. It’s designed to make it easier to work with APIs (like fetching data from a server) while keeping the fetched data in sync with your Redux store. Let’s understand how it works.

## What Problem RTK Query Solves

**Problems:**

- Tracking loading state by showing the spinner.
- Avoiding duplicate requests for the same data.
- Managing cache as the user interacts with the UI.

Though **Redux** and **createAsyncThunk** API provide some or the other things, users still have to write significant amounts of reducer logic to manage the loading state and the cached data.

#### Bigger Concern

**“Data fetching and caching” is completely a different set of concerns than “state management”**

### Watch Video

## Step 1 – Install Packages

Initialize react app

```bash
npm create vite@latest
```

Install the packages

```bash
npm i @reduxjs/toolkit react-redux
```

## Step 2 – Setup json server/backend

Use [mockapi.io](https://mockapi.io/) to setup a dummy json server

## Step 3 – Create API Slice

Importing `createApi` and defining an “API slice” that lists the server’s base URL and which endpoints we want to interact with

**createAPI** –

It’s a function provided by Redux Toolkit Querty that helps to create an API slice.

It takes an object as an argument with 2 key properties –

- **baseQuery** – Here you define the base URL using `fetchBaseQuery` for making an HTTP request.
- **endpoints** – here you define the various endpoints for fetching and receiving data.

**Generated Hooks –**

Once the slice is defined, redux toolkit query automatically exposes a hook for each endpoint, that helps in fetching data in your component.

**How to write the hook name** ?

Just convert your endpoint name into camel case and add `_use_` keyword at the start and `_Query_` keyword at the end.

```typescript
use<_EndPointName_>Query
Eg - use_GetStudents_Query 
```

_src/components/features/studentApi.tsx_

```typescript
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

export const studentApi = createApi({
  baseQuery: fetchBaseQuery({ baseUrl: 'https://641dd63d945125fff3d75742.mockapi.io' }),
  endpoints: (builder) => ({
    getStudents: builder.query<Student[] , void>({
      query: () => '/crud',
    }),
  }),
});

export const { useGetStudentsQuery } = studentApi;
```

```
builder.query< type of data that api returns , type of argument used to call api >
```

The RTK query automatically exposes a hook `use<FunctionName>Query` which can be used for fetching data.

## Step 4 – Configure Store

Create a store

**src/app/store.tsx**

```typescript
import { configureStore } from "@reduxjs/toolkit";
import { studentApi } from "../services/api";

export const store = configureStore({
  reducer: {
    [studentApi.reducerPath]: studentApi.reducer,
  },
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware().concat(studentApi.middleware),
});
```

Note you can also use RTK query without store as well, in that case, you don’t need this step.

## Step 5 – Provide store to the App

src/index.tsx

```typescript
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.tsx";
import "./index.css";
import { Provider } from "react-redux";
import { store } from "./app/store.ts";

ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);
```

**Without store**

```typescript
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.tsx";
import "./index.css";
import { ApiProvider } from "@reduxjs/toolkit/dist/query/react/ApiProvider";
import { studentApi } from "./services/api.tsx";

ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <ApiProvider api={studentApi}>
      <App />
    </ApiProvider>
  </React.StrictMode>
);
```

## Step 6 – Accessing Data on the UI (GET Request)

The exposed hook automatically handles the loading, error and success state.

**_src/components/Read.tsx_**

```typescript
import { useStudentDataQuery } from "../services/api";
import { useState } from "react";
import "./common/style.css";

const Read = () => {
  const { data, error, isLoading, isFetching, isSuccess, isError } = useGetStudentsQuery();

  return (
    <div>
      <

h2>Read Data</h2>
      {isLoading && <span>Loading..</span>}
      {isFetching && <span>Fetching Data..</span>}
      {error && <span>Something went wrong</span>}
      <div className="main__container">
        {isSuccess &&
          data?.map((ele) => (
            <div key={ele?.id} className="read__container">
              <h2>{ele?.studentName}</h2>
            </div>
          ))}
      </div>
    </div>
  );
};

export default Read;
```

---

Certainly! Here's the continuation of the markdown formatted text:

---

## Step 7 – Create a new student (POST request)

Now since “POST or PUT OR PATCH” changes the data, we use the `mutation` keyword instead of `query`.

In this case, the query function takes an object with 3 properties:

- **URL** – the endpoint on which the post action will take place
- **method** – define the type of HTTP request
- **body** – The payload or request body which needs to be passed

```typescript
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

export const studentApi = createApi({
  baseQuery: fetchBaseQuery({ baseUrl: 'https://641dd63d945125fff3d75742.mockapi.io' }),
  endpoints: (builder) => ({
    // get request
    getStudents: builder.query<Student[], void>({
      query: () => '/crud',
    }),
    // post request
    addStudent: builder.mutation<void, Student>({
      query: (student) => ({
        url: "/crud",
        method: "POST",
        body: student,
      }),
    }),
  }),
});

export const { useGetStudentsQuery, useAddStudentMutation } = studentApi;
```

## Step 8 – Create a form

**unwrap()**

When you call a mutation function using Redux Toolkit Query, it returns a Promise that resolves to the full result object. The result object typically includes information about the status of the mutation (e.g., loading, error, or success), as well as the data returned from the server. To access the actual data returned by the server, you use `.unwrap()`.

**_Example:_**

```typescript
try {
  const result = await createArticle(newArticleData).unwrap();
  console.log('New article created:', result);
} catch (error) {
  console.error('Error creating article:', error);
}
```

**_src/components/Create.tsx_**

```typescript
import React, { useState } from "react";
import { useAddStudentMutation } from "../services/api";
import { Student } from "../models/student.model";
import { useNavigate } from "react-router-dom";

const Create = () => {
  const [addStudent] = useAddStudentMutation();
  const [students, setStudents] = useState<Student>(Object);
  const navigate = useNavigate();

  const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    setStudents({ ...students, [e.target.name]: e.target.value });
  };

  const handleSubmit = async (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
    await addStudent(students);
    navigate("/");
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <div>
          <input
            type="text"
            placeholder="name"
            name="studentName"
            onChange={handleChange}
          />
        </div>
        <div>
          <input
            type="email"
            placeholder="email"
            name="studentEmail"
            onChange={handleChange}
          />
        </div>
        <button type="submit">Submit</button>
      </form>
    </div>
  );
};

export default Create;
```

## Step 9 – Updating and re-fetching

Before understanding the re-fetching concept, let’s first understand the cache behaviour of RTK query.

**Cache Behaviour**

When data is fetched from the server or backend, RTK Query will store the data in the Redux store as a ‘cache’. When an additional request is performed for the same data, RTK Query will provide the existing cached data rather than sending an additional request to the server.

The cache behaviour and lifetime can be manipulated by `keepUnusedDataFor`.

**refetch()**

Calling the re-fetch function will forcefully re-fetch the associated query.

A few other re-fetch methods are `refetchOnMountOrArgChange`, `refetchOnFocus`, `refetchOnReconnect`.

### **Automated Re-fetching in RTK Query**

Apart from the above function we also have automated refetch in RTK which works so on the whole API level as well as individual endpoint level.

In Redux Toolkit Query, the concept of "refetching" refers to the ability to manually request or refresh data from an endpoint without relying on the automatic caching and invalidation. This can be useful in scenarios where you need to force a new request to update the data or when you want to provide a user-triggered refresh mechanism. Additionally, RTK Query allows you to use "tags" to help manage and control the data fetching process.

**TagTypes** –

Tags are just a label attached to the cached data for controlling caching and invalidation behavior for re-fetching purposes.

**ProvidesTags** –

The `providesTags` option is used to specify the tags that an endpoint provides. These tags represent the data that the endpoint fetches, and they are used for caching and managing data in your Redux store.

The `ProvidesTag` works on a query endpoint.

**InvalidatesTags** –

The `invalidatesTags` option is used to specify the tags that should be invalidated when a mutation is performed. Mutations are typically actions that change the data on the server, and you may want to invalidate the cached data in your Redux store to reflect the changes.

The `InvalidatesTags` works on a mutation endpoint.

```typescript
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query/react";
import { Student } from "../models/student.model";

export const studentApi = createApi({
  reducerPath: "studentApi",
  baseQuery: fetchBaseQuery({
    baseUrl: "https://641dd63d945125fff3d75742.mockapi.io",
  }),
  tagTypes: ["Student"],
  endpoints: (builder) => ({
    getStudents: builder.query<Student[], void>({
      query: () => "/crud",
      providesTags: ["Student"],
    }),
    addStudent: builder.mutation<void, Student>({
      query: (student) => ({
        url: "/crud",
        method: "POST",
        body: student,
      }),
      invalidatesTags: ["Student"],
    }),
  }),
});

export const { useStudentDataQuery, useAddStudentMutation } = studentApi;
```

In the above code, the `getStudents` endpoint is associated with the ‘Student’ tag. When data is fetched successfully by this endpoint, it’s stored in the Redux store with the ‘Student’ tag. Other parts of your application can then use this tag to manage the cached data.

In the above code, the `addStudent

` mutation is configured to invalidate the ‘Student’ tag when a new student is created. This means that when the mutation successfully creates a new student data, it triggers the invalidation of any cached data associated with the ‘Student’ tag in the Redux store, so that the next fetch will reflect the updated data.

## Step 10 – Transform Response

In RTK Query, the `transformResponse` option is used to manipulate the response received from an API before it is used or stored in the Redux store. This can be useful for extracting specific data or headers from the response and performing any necessary transformations.

The “transformResponse” takes 3 parameters:

- `response` – This contain the raw API response. It includes the response body and header.

```typescript
transformResponse: (response, meta, arg) => {
  // Access response data
  const responseData = response.data;
  
  // Access response headers
  const responseHeaders = response.headers;
  
  // You can also inspect other properties of the response object as needed.
  
  return response;
}
```

- `meta` – It is an object that container details about metadata of request ,response and other related information.

```typescript
transformResponse: (response, meta) => {
  const apiName = meta.apiName;
  const path = meta.path;
  const requestId = meta.requestId;
  
  // You can access other properties of the meta object as needed.
  
  return response;
}
```

- `args` – It contains the argument object that was passed in the query hook when it was dispatched. It if often used to filter the data or manipulated the response.

```typescript
endpoints: (builder) => ({
  studentData: builder.query<Student[], void>({
    query: () => "/crud",
    transformResponse: (res: Student[], meta, args) => {
      return res.sort((a, b) => a.studentName.localeCompare(b.studentName));
    },
    providesTags: ["Student"],
  }),
```

In the above example, we are sorting the response before storing it in the Redux store.

Depending on your specific use case, you may choose to use one or more of these parameters to perform transformations or other operations on the response before it is stored in the Redux store.

## Conclusion

RTK query is basically a redux toolkit with some more added features for data fetching and caching.

You can't avoid it because while building bigger application, one major concern is the optimization’s and scalability of an web apps, and feature like this definitely helps a lot at that time.

In short, if you are done with redux toolkit, this is your next step to learn, go for it.

---

Please let me know if you need further clarification or assistance!
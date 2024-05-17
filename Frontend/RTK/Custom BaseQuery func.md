
## Usage Summary: fetchBaseQuery vs. Custom Functions

- **FetchBaseQuery**
  - Function provided by RTK Query for network requests
  - Simplifies request process: handles headers, authentication tokens, etc.
  - Provides features like automatic error handling, request cancellation, etc.
  - Ensures consistency with RTK Query patterns

- **Custom Functions**
  - Allows customization of request behavior
  - Requires manual handling of tasks like headers, tokens, etc.
  - May miss out on RTK Query features if not implemented

## Custom BaseQuery Example

```typescript
const customBaseQuery = async (
    args: string | FetchArgs,
    api: BaseQueryApi,
    extraOptions: {},
) => {
    console.log('Custom base query function');

    // Add your custom logic here

    return await fetchBaseQuery({
        baseUrl: import.meta.env.VITE_BACKEND_URL,
        credentials: 'include',
        prepareHeaders: (headers, { getState }) => {
            const token = (getState() as RootState).authState.token?.toString();

            if (token) {
                headers.set('authorization', `Bearer ${token}`);
            }

            return headers;
        },
    })(args, api, extraOptions);
};
```

## Considerations Without fetchBaseQuery

- **Automatic Error Handling:** Needs manual implementation
- **Request Cancellation:** Requires custom logic for ongoing requests
- **Serialization of Request Arguments:** May need manual handling
- **Integration with DevTools:** Custom implementation may lack this feature
- **Consistency with RTK Query Patterns:** Using fetchBaseQuery ensures consistency and ease of understanding for developers familiar with RTK Query

## Conclusion

Using fetchBaseQuery simplifies API integration and provides built-in features for error handling, request cancellation, and more. While custom functions offer flexibility, they require more manual effort and may not fully leverage the benefits of Redux Toolkit Query.

---

```javascript
const user = useAppSelector((state) => state.user);
const { data = user } = useUserQuery(undefined, { skip: Boolean(user) });
```

now this would trigger only if there is no user, and data would be equal to user, if there is user
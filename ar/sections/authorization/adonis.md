كوّن دوال التفويض المرجعية في التكوين:

```typescript
authorization: {
  isAgent: async (user) => {
    return user.role === 'agent' || user.role === 'admin'
  },
  isAdmin: async (user) => {
    return user.role === 'admin'
  },
}
```

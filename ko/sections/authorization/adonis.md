설정에서 인가 콜백을 구성합니다:

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

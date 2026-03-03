在配置中设置授权回调：

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

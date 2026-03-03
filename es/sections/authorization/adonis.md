Configura los callbacks de autorizacion en tu configuracion:

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

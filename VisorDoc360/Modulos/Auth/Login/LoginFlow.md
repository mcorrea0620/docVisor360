```graph
graph TD
  A[Login] --> B[AuthService]
  B --> C{UmeService?}
  C -->|Éxito| D[Generar JWT]
```
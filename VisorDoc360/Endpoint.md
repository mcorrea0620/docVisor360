# Endpoints API

## `GET /users`
```python
@app.get("/users")
def get_users():
    return db.query(User).all()
```
**Params**:  
- `limit: int` (opcional)  
**Uso**:  
Ver [[Auth#login]] primero.
[[Componentes]]
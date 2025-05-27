# 🔐 Módulo de Autenticación

## 📌 Overview
Proceso completo de autenticación (login, registro, recuperación de contraseña).  
**Tecnologías**: Laravel 10, UME API (externo), JWT.

## 🧩 Submódulos
1. [[Login/LoginFlow]]  
2. [[PasswordReset/ResetFlow]]  
3. [[Services/AuthService]]  

## 🌐 Dependencias Externas
- **UME API**: [[Services/UmeService]] (para validación de identidad).  
- **Paquetes**: `laravel/sanctum`, `guzzlehttp`.

## 🗃️ Base de Datos
```sql
users (id, email, password_reset_token)
password_resets (email, token)
```

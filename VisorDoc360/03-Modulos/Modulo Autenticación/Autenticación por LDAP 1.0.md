## Descripción
El modulo de Autenticación con directorio activo nos permite acceder mediante la red si el usuario tiene acceso mediante su número de identificación y su contraseña.
Ahora tenemos dos vistas de autenticación (Vista principal para el ciudadano UME, Vista para funcionario Directorio activo) y dependiendo de la vista por la cual se haga el ingreso se creara una "session" global que nos ayudara a restringir roles y permisos mediante un middleware, esto nos ayuda a poder separar las opciones del ciudadano a las del funcionario.  

Por favor leer [[Guia Apache directory studio]] para implementar directorio activo local y puedas hacer las pruebas pertinentes de tus flujos en cuestión para el manejo de funcionarios.

## Requerimientos Funcionales
- Permitir acceso a usuarios internos con credenciales LDAP o base de datos
- Permitir acceso a usuarios externos (proveedores) con cedula y contraseña por medio del API de la UME
- Gestionar sesiones de forma segura

##  Librerías
- LdapRecords: "directorytree/ldaprecord": "^3.8"

## Bases de datos
---
### Migraciones
```bash
php artisan migrate --path=database/migrations/ldap/2025_06_09_144213_add_column_email_ldap.php
```

### Tablas Involucradas
- Users: Se requiere que el usuario este en base de datos guardado anteriormente para poder generar la sesión, se registrara unicamente por base de datos todo usurio que se registre con su correo alcaldia (@medellin.gov.co)

## Impacto a gran escala
- [[LeftMenu]]
- [[#Rutas]] y Middleware
- [[#User]]

### Rutas
El uso correcto del middleware sera indicarle si el modulo es para funcionarios `check.login:ldap` o esta abierto al ciudadano `check.login:ume` si tiene acceso a ambos se puede omitir este middleware.
```php
Route::middleware(['auth', 'check.login:ldap','role:SGHSC-SUPERADMIN EPP|SGHSC-ADMIN EPP'])->group(function () {
```

Habrá casos más específicos en que la ruta debe ser accesible para ciudadanos y otros públicos por lo que nos podremos ayudar de la función `withoutmiddleware` como en el siguiente ejemplo:

```php
Route::get('/actualizacionfirmaelectronica/confirmacion/{nombre}', [ActualizacionFirmaElectronicaController::class, 'indexConfirm'])->name('firmaelectronica.confirm')->withoutMiddleware(['auth', 'role:FUNCIONARIO', 'check.login:ldap']);
```
### User
En el modelo User se agrega la función `hasAccessTo` que recibe role como parámetro e identifica el usuario según el tipo de autenticación para identificar los permisos.

```php
public function hasAccessTo($role)
	$authType = session('auth_type');

	if ($authType === 'ldap') {
		return $this->hasRole($role); 	
	}
	if ($authType === 'ume') {
		return $this->hasRole('CONTRIBUYENTE') || $this->hasRole($role);
	}
	return false
}
```

## Clases y funciones clave
### Controladores
- AuthController
  - login()
  - logout()
  - showLoginForm()

### Modelos
- User
  - relationships: roles

### Requests
- LoginRequest
  - Validaciones personalizadas para tipo de login

### Servicios/Helpers
- AuthLdapService
  - verificarTipoUsuario()
  - autenticar()
- LdapService
  - getUserByDocument($document): Permitte obtener todos los datos de un usuario registrado en directorio activo usando el número de identificación.
  - getDataRegister($document): captura los datos relevantes del usuario disponibles en directorio activo para registro de usuario como lo son identification_nit, surname, name e email.
  - getAreaByDocument($document): Captura la secretaria, subsecretaria, cargo y equipo del usuario registrado en directorio activo.

---

## Cambios importantes / Historial
- 2025-06-20 (Mauricio Correa Celis ): Implementación de doble login (LDAP + UME)
  - ==Cambios en rutas== Importante validar sus rutas al momento de hacer merge
  - Middleware actualizado para verificar tipo_login `check.login:ldap` 

- 2025-06-27 (Diego Nuñez): Validación en el archivo web.php para permitir las pruebas de usuario en local

---

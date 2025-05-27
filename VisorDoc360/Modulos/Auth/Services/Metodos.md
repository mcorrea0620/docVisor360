### Login:
```php
public function login($user_identification, $password){
	return $this->request('inicioSesion', [
		'usuario' => $user_identification,
		'contra' => $password
		]);
}
```

Este motodo hará la función de inicio de sesión y nos da como respuesta:
**Salida:**
- success = 1 éxito, 0 fallo.
- message = indicador textual del resultado de la petición o vencimiento de token.
- code = "Códigos de estado HTTP"

**Ejemplo JSON salida:**
- En caso de que el token haya expirado:
```json
{
    "message": "Token de autenticación invalido",
    "code": 401,
    "success": 0
}
```

- En caso de que el usuario sea incorrecto:
```json
{
    "message": "El usuario o la contraseña son incorrectos. Número de intentos restantes: 1 ",
    "code": "200",
    "success": "0"
}
```

- En caso de que el usuario se encuentre bloqueado:
```json
{
    "message": "El usuario se encuentra bloqueado. Demasiados intentos fallidos",
    "code": "200",
    "success": "0"
}
```

- Inicio de sesión exitoso:
```json
{
    "message": "Inisio de sesión correcto",
    "usuario": {
        "direccion": "calle falsa 123",
        "ciudad": "05001-MEDELLÍN",
        "nombres": "Ficticio Prueba",
        "apellidos": "Listo ejemplo",
        "telefono": "5814766",
        "correo": "sergio.rojas@medellin.gov.co",
        "celular": "300102000"
    },
	"code": "200",
    "success": "1"
}

```


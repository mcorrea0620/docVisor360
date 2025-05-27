### **3. Ejemplo: Documentación de `UmeService.php` (API Externa)**

# 🌍 UmeService

**Path**: `app/Services/UmeService.php`

## 📌 Propósito
Integración con UME API para validación de identidad (2FA) esto nos dara facilidad en cuanto a las peticiones y respuestas en cuento a la autenticación de usuario por medio de diferentes [[Metodos]] .


## 🔌 Configuración
```env
# .env
UME_API_KEY=tu_key
UME_ENDPOINT=https://api.ume.com/v1/auth
```
## Requerimientos
Algunas funciones requieren que se haga una autenticación por medio de una auth key que se genera de la siguiente manera:
Este método de autenticación consiste en la construcción de una _**llave:**_

Construida concatenando en orden los siguientes datos: un **hexadecimal** de 40 caracteres, **fecha - hora** del consumo formato (yyyy-MM-dd'T'HH:mm:ssZ) y la **contraseña del** **usuario de comunicación** **en base64**. Esta cadena resultante deberá ser codificada por el algoritmo SHA256 y el resultado se convierte a mayúsculas y luego en Base64.

Esta llave se ingresa en la sección de autenticación del Json de la solicitud, junto los siguientes datos:

- Fecha: Fecha usada para la generación del token
- Usuario: usuario de comunicación en base 64
- Cadena: cadena 40 caracteres (hexadecimal) usada para la generación del token.

Construyendo de esta manera la sección de autenticación o token del Json de la solicitud:
```json
{'fecha': '2025-05-27T15:03:41-05:00', 'usuario': 'VVNSX1ZJU09SMzYwX1VNRQ==', 'cadena': '6a4ab7aedd624433d29f3601a7312561ba5c7300', 'llave': 'NEI1REFDRDI2OUI2N0ZENzU2QjIzMDU4RTAzNzJEMDY2NURFM0IyNUE1NDIyRTIwNDFCQkJCOTE0RTdGMzRBMw=='}
```


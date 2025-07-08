# 📘 Guía: [Título descriptivo aquí]
> _Breve descripción del objetivo de la guía. ¿Para qué sirve?_

---

## 🎯 Objetivo
- Instalar y configurar apache directory studio con el fin de simular un directorio activo en la maquina local para hacer simulaciones correctas de ingreso funcionario.

---

## ✅ Prerrequisitos
- Java 11.0.x -> Especificamente la 11
- Apache Directory Studio
- Runtime Enviroment

---

## 🗂️ Índice (opcional)
- [[#🎯 Objetivo]]
- [[#✅ Prerrequisitos]]
- [[#⚙️ Instalación]]
- [[#🛠️ Configuración inicial]]
- [[#✅ Pruebas / Verificación]]
- [[#⚠️ Notas y advertencias]]
- [[#🔗 Referencias]]

---

## ⬇️ Descarga
- [URL oficial ](https://directory.apache.org/studio/download/download-windows.html)
- Ultima version
- Si usas linux puedes usar SLAPD

```bash
# Comando de descarga opcional
```

## ⚙️ Instalación
### Paso 1
- Ingresa a la URL indicada en el apartado de descarga, allí inicialmente veras el link de descarga, recomendamos usar el .exe.
- Una vez instalado podemos dar clic derecho y ejecutar como administrador.
- Puede generar conflictos con el antivirus recomendamos desactivarlo para la instalación.

```bash
# Comando o instrucción
```
### Paso 2 - Crea un server
- En el menú inferior en **LdapServers** daremos clic derecho y 'new server'.
- Daremos clic en la parte de apacheDS 2.0 y finalizamos.

### Paso 3 - Crear la conexión
- Ejecuta apache directoy studio y en el menu inferior veras una opción que dice **LDAP** o **Connections** allí seleccionaremos new connection o nueva conexión

```bash
NAME: INGRESA-EL-NOMBRE-DE-TU-PREFERENCIA
HOSTNAME: localhost
PORT: 389 #recomendado
```
En Bind DN o User pondremos lo siguiente

```bash
uid=admin,ou=system
```
Esta sera la estructura del administrador y le definiremos la contraseña en **Bind password** 

### Paso 4 - Crear nuevo grupo o unidad organizada (OU)


--- 
## 🛠️ Configuración inicial
- Archivos o rutas importantes
- Variables de entorno
- Preferencias o parámetros clave

``` bash
# Ejemplo de configuración
```

## ✅ Pruebas / Verificación
- Cómo comprobar que está bien instalado
- Comando o pantalla de éxito esperada 
- Logs relevantes
--- 

## ⚠️ Notas y advertencias
- Errores comunes y soluciones
- Advertencias de seguridad
- Consideraciones de compatibilidad

- Puede que tengas un error al momento de abrir el .exe en ese caso debes comprobar que tengas java instalado `java --version` y comprueba que exista en tus **Variables de entorno** 
- ![[Pasted image 20250707143317.png]]

--- 

## 💡 Consejos opcionales
- Mejores prácticas
- Tips de uso avanzado

--- 
## 🔗 Referencias
- Documentación oficial
- Tutoriales externos
- Issues o tickets relacionados
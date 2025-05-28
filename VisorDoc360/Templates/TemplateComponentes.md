# 📦 Componente: FormularioDireccion

## 🧩 Descripción
Componente que permite registrar direcciones con campos de via, sufijo, etc relacionando el usuario con la tabla necesaria para el proyecto de geolocalización.

## 📁 Archivos relacionados
- Blade: `resources/views/components/formulario-direccion.blade.php`
- JS: `public/js/componentes/formulario-direccion.js`
- DB: Tabla `project_address`

## ⚙️ Parámetros
| Parámetro | Tipo | Descripción |
|----------|------|-------------|
| `modo`   | string | 'crear' o 'editar' |
| `direccion_id` | int | ID para edición |

## 📌 Dependencias
- Vue.js (si aplica)
- Bootstrap

## 🔄 Uso en otros módulos
- [[Formulario Dirección]]
- [[Módulo de Pedidos]]

## 📎 Ejemplo de uso
```php
@include('example.component.html')
```

### Visualización
![[Pasted image 20250527160647.png]]acá tenemos una muestra de la vista de dirección
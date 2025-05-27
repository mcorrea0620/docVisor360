# 📦 Componente: FormularioDireccion

## 🧩 Descripción
Componente que permite registrar direcciones con campos de país, ciudad y barrio.

## 📁 Archivos relacionados
- Blade: `resources/views/components/formulario-direccion.blade.php`
- JS: `public/js/componentes/formulario-direccion.js`
- DB: Tabla `direcciones`

## ⚙️ Parámetros
| Parámetro | Tipo | Descripción |
|----------|------|-------------|
| `modo`   | string | 'crear' o 'editar' |
| `direccion_id` | int | ID para edición |

## 📌 Dependencias
- Vue.js (si aplica)
- Bootstrap

## 🔄 Uso en otros módulos
- [[Módulo de Usuarios]]
- [[Módulo de Pedidos]]

## 📎 Ejemplo de uso
```blade
<x-formulario-direccion :direccion="$direccion" modo="editar" />
```

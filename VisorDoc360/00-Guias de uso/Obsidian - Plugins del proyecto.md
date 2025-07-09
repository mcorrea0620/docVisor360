## ¿Qué son los plugins?
Los plugins son extensiones que agregan funcionalidades extra a Obsidian. Permiten personalizar la experiencia y hacer cosas que no vienen “de fábrica”, como plantillas automáticas, diagramas, integración con Git y más.

## ¿Cómo usarlos?
1. Abre Obsidian.
2. Ve a **Settings > Community Plugins**.
3. Activa **Safe Mode** en off para permitir instalar plugins de la comunidad.
4. Haz clic en **Browse** (Explorar) para buscar plugins.
5. Haz clic en **Install** para descargar, luego **Enable** para activar.
6. Ajusta la configuración de cada plugin en **Options** o **Settings** si aplica.

> ⚠️ Recomendación: instala solo los plugins que tú o tu equipo necesiten para evitar conflictos y mantener la instalación limpia.

## Plugins 
### Git
- Sincroniza tu Vault con repositorios Git (GitHub, GitLab, etc.)
- Permite hacer pull, commit y push desde Obsidian.
- Ideal para trabajo en equipo: todos tienen la misma versión de la documentación.
- Incluye opciones de auto-commit y auto-pull para más comodidad.
- Puedes ver historial de cambios.
#### Configuración típica:
- Auto Pull al abrir
- Auto Commit con mensaje estándar
- Auto Push al guardar

### Templater
- Plugin de plantillas avanzadas.
- Permite crear templates reutilizables con variables y scripts.
- Muy útil para estandarizar: módulos, guías de instalación, changelogs.
- Ahorra tiempo y mejora la consistencia.

#### Uso sugerido:
- Crear una carpeta /Plantillas
- Escribir tus templates en markdown
- Invocar las plantillas al crear nuevas notas

### Paste URL into Selection
- Productividad para documentación.
- Selecciona texto y pega un enlace → automáticamente convierte en markdown [texto](url).
- Evita tener que escribir manualmente la sintaxis de enlaces.
- Muy útil para insertar documentación oficial, tutoriales externos, tickets.

**Ejemplo:**
- Selecciona “Obsidian” → pega https://obsidian.md
- Resultado: [Obsidian](https://obsidian.md)

### Admonition
- Agrega bloques visuales para advertencias, info, tips.
- Mejora la legibilidad de la documentación.
- Usa bloques como > [!note], > [!warning], > [!tip].

#### Ejemplo de uso:

> [!warning] Titulo
> Asegúrate de tener permisos de administrador para esta instalación.

### Advanced Tables
- Edición más cómoda de tablas en markdown.
- Permite navegar con el teclado, alinear columnas, insertar filas fácil.
- Muy útil para documentar esquemas, comparativas, requisitos.
### QuickAdd
- Para crear notas y tareas rápidamente con plantillas.
- Combina bien con Templater.
- Ayuda a mantener la estructura al crear nuevas guías.

### Calendar
- Visor de calendario dentro de Obsidian.
- Útil para planificar entregas de documentación.
- Ayuda a coordinar revisiones de equipo.

### Breadcrumbs
- Crea jerarquías y navegación entre notas.
- Muy útil para organizar documentación extensa.
- Permite ver el “mapa” de tus notas.

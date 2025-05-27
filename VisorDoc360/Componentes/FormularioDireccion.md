# 🧩 FormularioDireccion

**Descripción**: Componente reutilizable para capturar direcciones postales.  
**Dependencias**: `Vue 3`, `Tailwind CSS`, `validación-vuelidate`.

---

## 🛠️ Implementación
Para poder usar el componente basta con incluirlo en tu html, remendamos usarlo en forma de modal:
### HTML
```php
@include('example.component.html')
```

### HTML
```html
<div class="row">
	<div class="col-sm-2">
		<label class="form-label">Vía<span class="text-danger">*</span></label>
			<select id="id_via_type" name="id_via_type" class="form-select" required>
				<option value="">Seleccione</option>
				@foreach($via_types as $via)
					<option value="{{ $via['id'] }}" >{{ $via['name'] }}</option>
				@endforeach
			</select>
	</div>
	<div class="col-sm-1">
		<label class="form-label">Num<span class="text-danger">*</span></label>
		<input type="number"
			id="via_number"
			name="via_number"
			class="form-control"
			required
			maxlength="3"
			pattern="[0-9]+"
			oninput="this.value=this.value.replace(/[^0-9]/g,'');">
	</div>
	<div class="col-sm-1">
		<label class="form-label">Letra</label>
		<select class="form-select" name="id_via_suffix" id="id_via_suffix">
			<option value="">Seleccione</option>
			@foreach($suffixes as $suffix)
			<option value="{{ $suffix['id'] }}">{{ $suffix['name'] }}</option>
			@endforeach  
		</select>
	</div>
	<div class="col-sm-2">
		<label class="form-label">Orientación</label>
		<select id="id_via_orientation" name="id_via_orientation" class="form-select">
			<option value="">Seleccione</option>
			@foreach($orientations as $orientation)
			<option value="{{ $orientation['id'] }}">{{ $orientation['name'] }}</option>
			@endforeach
		</select>
	</div>
	
	  
	
	<div class="col-sm-1">
		<label class="form-label">Num<span
			class="text-danger">*</span></label>
		<input type="number"
			id="intersection_number"
			name="intersection_number"
			class="form-control"
			required
			maxlength="3"
			pattern="[0-9]+"
			oninput="this.value=this.value.replace(/[^0-9]/g,'');">
	</div>
	
	<div class="col-sm-2">
		<label class="form-label">Vía<span></label>
		<select id="id_intersection_suffix" name="id_intersection_suffix" class="form-select">
			<option value="">Seleccione</option>
			@foreach($via_types as $via)
			<option value="{{ $via['id'] }}">{{ $via['name'] }}</option>
			@endforeach
		</select>
	</div>
	
	<div class="col-sm-2">
		<label class="form-label">Orientación</label>
		<select id="id_intersection_orientation" name="id_intersection_orientation" class="form-select">
			<option value="">Seleccione</option>
			@foreach($orientations as $orientation)
			<option value="{{ $orientation['id'] }}">{{ $orientation['name'] }}</option>
			@endforeach
		</select>
	</div>
	
	<div class="col-sm-1">
		<label class="form-label">Num<span
			class="text-danger">*</span></label>
		<input type="number"
			id="complement"
			name="complement"
			class="form-control"
			required
			maxlength="3"
			pattern="[0-9]+"
			oninput="this.value=this.value.replace(/[^0-9]/g,'');">
	</div>
	
	  
</div>

<div class="col-sm-12 mt-2">
	<label class="form-label">Información adicional</label>
	<input type="text" id="aditional_info" name="aditional_info" class="form-control">
</div>

<div class="row mt-3">
	<div class="col-sm-12">
		<label class="form-label">Dirección</label>
		<input type="text" id="address_notification" name="address_notification"
		class="form-control bg-light" readonly>
	</div>
</div>
<script>
	@vite(['resources/js/auth/register.js'])
</script>

```

### JavaScript : addressAutocomplete.js
```javascript
export function setupAddressAutocomplete() {
  const camposDireccion = [
    'id_via_type', 'via_number', 'id_via_suffix', 'id_via_orientation',
    'intersection_number', 'id_intersection_suffix', 'id_intersection_orientation', 
    'complement', 'aditional_info'
  ];

  function actualizarDireccion() {
    const getSelectedText = (id) => {
      const el = document.getElementById(id);
      return el?.selectedIndex > 0 ? el.options[el.selectedIndex].text : '';
    };

    const getValue = (id) => {
      const el = document.getElementById(id);
      return el?.value || '';
    };

    const direccionParts = [
      getSelectedText('id_via_type'),
      getValue('via_number'),
      getSelectedText('id_via_suffix'),
      getSelectedText('id_via_orientation'),
      getValue('intersection_number') && `#${getValue('intersection_number')}`,
      getSelectedText('id_intersection_suffix'),
      getSelectedText('id_intersection_orientation'),
      getValue('complement') && `-${getValue('complement')}`,
      getValue('aditional_info') && `(${getValue('aditional_info')})`
    ].filter(Boolean);

    const addressInput = document.getElementById('address_notification');
    if (addressInput) {
      addressInput.value = direccionParts.join(' ').trim();
    }
  }

  camposDireccion.forEach(id => {
    const element = document.getElementById(id);
    if (element) {
      element.addEventListener('change', actualizarDireccion);
    }
  });

  // Inicializar al cargar
  actualizarDireccion();
})
```

### 📚 Tablas Relacionadas
```sql
CREATE TABLE direcciones (
  id SERIAL PRIMARY KEY,
  calle VARCHAR(255)
);
```

---

## 🎨 Uso
1. Importar componente:
   ```javascript
   import FormularioDireccion from '@components/FormularioDireccion.vue';
   ```
2. **Props aceptadas**:
   - `paisDefault: String` (Valor: "México")

---

## 🔗 Relacionados
- [[Módulos/Checkout]]  // Donde se usa este componente
- [[Database/Modelos#direcciones]]
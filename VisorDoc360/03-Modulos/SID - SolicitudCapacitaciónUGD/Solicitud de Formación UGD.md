# Nombre del Módulo

**Descripción breve:**  
> _El modulo de capacitación se basa en un formulario que llena un solicitante que tenga un cargo directivo para agenda una capacitación por parte de la Unidad de Gestión Documental en temas de archivo, como Documento Físico o electrónico.
---

## Indice
- [[#Requerimientos funcionales]]
- [[#Base de datos]]
- [[#Tablas involucradas]]
- [[#Migraciones]]
- [[#Librerias]]
- [[#Clases y funciones clave]]

## Requerimientos funcionales
- Controlar las solicitudes requeridas por las diferentes secretarias para estandarizar y encapsular las fechas, participantes, memorias del encuentro y actas de reunión.
- Para llevarlo a cabo se tiene el solicitante con cargo directivo (SID-SOLICITANTE) y el lider de la unidad de gestión documental (SID-ADMIN-SOLICITUD).
- Un equipo, secretaria o subsecretaria que requiera formación podra usar el formulario para enviar la solicitud y recibir una confirmación por parte del lider de la UGD

---

## Base de datos
### Tablas involucradas
- Nomenclatura de tablas "*ugd_request_nombretabla*" en el schema de InnovacionDigital
![[Untitled Diagram_2025-07-08T18_55_43.144Z.png]]

### Migraciones
```bash
php artisan migrate --path=database/migrations/SecretariaInnovacionDigital/SolicitudFormacionUGD
class="Database\\Seeders\\SecretariaDeInnovacionDigital\\SolicitudFormacionUGD\\AreasSeeder"
php artisan db:seed --class="Database\\Seeders\\SecretariaDeInnovacionDigital\\SolicitudFormacionUGD\\CategoryUGDSeeder"
php artisan db:seed --class="Database\\Seeders\\SecretariaDeInnovacionDigital\\SolicitudFormacionUGD\\StatusUGDSeeder"
php artisan db:seed --class="Database\\Seeders\\SecretariaDeInnovacionDigital\\SolicitudFormacionUGD\\SubjectsUGDSeeder"
php artisan db:seed --class="Database\\Seeders\\SecretariaDeInnovacionDigital\\SolicitudFormacionUGD\\ModalitiesUGDSeeder"

```

### Librerias
```bash
npm import xlsx
```
---

## Clases y funciones clave
- **Controladores**
  -  `app/Http/Controllers/SecretariaDeInnovacionDigital/SolicitudFormacionUGD/FUGDSolicitudController.php`
  - `app/Http/Controllers/SecretariaDeInnovacionDigital/SolicitudFormacionUGD/FUGDSolicitudAdminController.php`
 
  - En estas rutas esta definido los controladores que hacen la conexión de las rutas y los handlers que viene a ser la logica de negocio de cada controlador
  
- **Modelos**
  - Nuestro modelo principal `RequestUGD` contiene varias relaciones con tablas pivote
```php
  class RequestUGD extends Model{
	protected $connection = 'pgsqlInnovacionDigital';
	protected $table = 'request_ugd';
	protected $primaryKey = 'id';
	protected $fillable = [
	'id',
	'modality_id',
	'request_department',
	'request_subsecretary',
	'status_id',
	'request_user_id',
	'request_date',
	];
	
	public $timestamps = false;
	
	public function participantes(){
		return $this->belongsToMany(FugdUser::class, 'request_participants', 'request_id', 'participant_id');
	}
	  
	public function fechas(){
		return $this->hasMany(FugdProposedDates::class, 'request_id');
	}
	
	public function subjects(){
		return $this->belongsToMany(FugdSubject::class, 'request_subjects', 'request_id', 'subject_id');
	}
	
	public function user(){
		return $this->belongsTo(User::class, 'request_user_id');
	} 
	public function modality(){
		return $this->belongsTo(FugdModality::class, 'modality_id');
	}
	
	public function contacto(){
	
		return $this->hasOne(FugdContact::class, 'request_id');
	}
	public function status(){
		return $this->belongsTo(FugdStatus::class, 'status_id');
	}
	public function areas(){
		return $this->belongsToMany(FugdAreas::class,'request_areas','request_id', 'area_id');
	}
	public function files(){
		return $this->hasMany(FugdRequestFile::class, 'request_id');
	}
}
```
- Servicios/helpers
  - `app/Services/SecretariaInnovacionDigital/SolicitudFormacionUGD/FUGDSolicitudHandler.php`
  - `app/Services/SecretariaInnovacionDigital/SolicitudFormacionUGD/FUGDSolicitudAdminHandler.php`

---

## Cambios importantes / Historial
- 8 de Julio 2025, Mauricio Correa Celis - Requerimiento de formulario y vista administrador completa
- Librería nueva `npm import xlsx` 

---

## Dependencias o módulos relacionados
- Se usa LdapService para la pre-carga de datos del usuario
```php
      public function getFormData(){
        $dataArea = $this->LdapService->getAreaByDocument(auth()->user()->identification_nit);
        $dataUser = $this->LdapService->getDataRegister(auth()->user()->identification_nit);
        return [
            'categories' => FugdCategory::all(),
            'subjectsByCategory' => FugdSubject::where('official', true)->get()->groupBy('category_id'),
            'modalities' => FugdModality::all(),
            'dependencies' => $dataArea['department'] ?? null,
            'subsecretary' => $dataArea['subsecretary'] ?? null,
            'name_user' => auth()->user()->name ?? null,
            'position' => $dataArea['title'] ?? null,
            'email' => $dataUser['email'] ?? null, 
            'areas' => FugdAreas::where('is_active', true)->get(),
        ];
    }
```

---

## Consideraciones para desarrollo futuro
%% - Problemas conocidos
- Ideas de mejora
- Riesgos o advertencias %%

---

## Referencias
%% - Pull Requests
- Tickets / Issues
- Documentos externos](<#  Módulo: Inventario %%

## Estructura
%% - Modelos: `Producto`, `Movimiento`
- Controladores: `InventarioController`, `ReporteController`
- Vistas: `inventario/index.blade.php`, etc.
 %%
%% ## Casos de uso
- Registrar producto nuevo
- Entrada manual de inventario
- Salida por venta %%

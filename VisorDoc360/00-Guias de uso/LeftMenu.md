## Descripcion
El leftmenu es un componente donde podremos visualizar y seleccionar los modulos disponibles según el usuario por los roles o tipo de acceso que tenga.
## Uso

### Roles y permisos funcionarios y ciudadanos
En la vista leftmenu podemos controlar que puede o no hacer un usuario, es muy importante tener en claro si el modulo es abierto al publico o únicamente para usuarios internos de la alcaldía.

```html
@authmenu('SGHSC-SUPERADMIN EPP|SGHSC-ADMIN EPP', 'ldap')
<li>
	<a href="javascript: void(0);" class="has-arrow">
	<i class="fas fa-hard-hat icon nav-icon"></i>
	<span class="menu-item" data-key="t-email">Inventario EPP</span>
</a>
	<ul class="sub-menu" aria-expanded="false">
		<li>
			<a href="{{ route('gestionhumana.epp.list-entrega-funcionario') }}" data-key="t-inbox">Entrega EPP</a>
			<a href="{{ route('gestionhumana.epp.list-inventario') }}" data-key="t-inbox">Ver Inventario</a>
			
			@endhasrole
		</li>
	</ul>
</li>
@endauthmenu

```

Con el authmenu debemos definirle los roles con el permiso para visualizar la vista y AuthType según el tipo de autenticación


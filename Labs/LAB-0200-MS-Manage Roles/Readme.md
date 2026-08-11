# LAB-0210-Manage-Roles-RoleGroups

## Asignar rol directo a un usuario
* [WINDOWS] LON-CL1 -> Browser (admin center, ya logueado como Holly)
* [MENU] Users -> Active users
  * [LINK] Diego Siciliani (nombre, no checkbox)
    * [TAB] Account -> sección Roles -> Manage roles
      * Seleccionar **Admin center access**
      * Show all by category -> categoría **Other** -> **Billing Administrator**
      * Save changes
> [!NOTE]
> Best practice: asignar el rol menos permisivo posible

## Asignar rol vía Role Group
* [MENU] Teams & groups -> Active teams & groups
  * [TAB] Security groups
    * [LINK] + Add a security group
      * Name : User management role group
      * Description : This role group contains user management roles
      * [TAB] Edit settings -> tildar **Azure AD roles can be assigned to the group**
      * Create group
* [MENU] Security groups -> **User management role group**
  * [TAB] General -> sección Roles -> Manage roles
    * Admin center access -> tildar **User Administrator** y **User Experience Success Manager**
    * Show all by category -> categoría **Identity** -> tildar también **Helpdesk Administrator**
    * Save changes
  * Verificar que aparecen los 3 roles asignados
* [MENU] Users -> Active users -> **Lynne Robbins**
  * [TAB] Account -> sección Groups -> Manage groups
    * Assign memberships -> tildar **User management role group** -> Add(1)
  * Verificar: reabrir Lynne -> Manage roles -> los 3 roles aparecen grisados (heredados del grupo, no se pueden sacar individualmente)

## Asignar rol con Powershell
* [WINDOWS] Powershell (elevado, full screen)
```powershell
Connect-MgGraph -Scopes 'User.ReadWrite.All', 'RoleManagement.ReadWrite.Directory'
```
* Login Holly -> Consent on behalf of organization -> Accept
* Buscar el object ID del rol (Service Support Administrator)
```powershell
Get-MgDirectoryRoleTemplate | Where-Object DisplayName -eq "Service Support Administrator" | Format-Table Id, DisplayName
```
* Buscar el object ID del usuario (Patti Fernandez)
```powershell
Get-MgUser -Filter "DisplayName eq 'Patti Fernandez'" | Format-Table ID, DisplayName
```
* Asignar el rol
```powershell
New-MgRoleManagementDirectoryRoleAssignment -RoleDefinitionId 'role ID' -PrincipalId 'Patti ID' -DirectoryScopeId '/'
```
* Verificar asignación
```powershell
$assignedRole = Get-MgDirectoryRole -Filter "DisplayName eq 'Service Support Administrator'"
Get-MgDirectoryRoleMember -DirectoryRoleId $assignedRole.Id
```
* Auditoría: listar todos los Global Administrators
```powershell
$assignedRole = Get-MgDirectoryRole -Filter "DisplayName eq 'Global Administrator'"
Get-MgDirectoryRoleMember -DirectoryRoleId $assignedRole.Id
```
> [!NOTE]
> Best practice: mantener entre 2 y 4 Global Administrators

## Validar asignaciones (con LON-CL2)
* [WINDOWS] LON-CL1 -> Browser -> verificar rápido en admin center
  * Joni Sherman : **No administrator access**
  * Lynne Robbins : rol **User Administrator**
* [WINDOWS] LON-CL2 -> login local `LON-CL2\Admin` / Pa55w.rd
* [WINDOWS] Browser -> https://www.microsoft365.com
  * Login **Joni Sherman** (cambiar password en el primer login)
  * Verificar: **NO** aparece el ícono **Admin** en el panel de apps (no tiene rol asignado)
  * Sign out
* [WINDOWS] Browser -> Switch a different account -> login **Lynne Robbins** (cambiar password)
  * Verificar: **SÍ** aparece el ícono **Admin** -> entrar

### Como Lynne: resetear passwords
* [MENU] Users -> Active users
  * [LINK] Diego Siciliani -> ícono key (Reset a password)
    * Probar password manual débil ("diego") -> botón deshabilitado
    * Probar "Pa55w.rd" sin forzar cambio -> error (password fácil de adivinar)
    * Tildar **Automatically create a password** + **Require change at first sign-in** -> Reset password
    * ⚠️ Error esperado: Diego tiene rol admin (Billing Admin), Lynne no es Global Admin -> no puede resetearle el password
  * [LINK] Pradeep Gupta -> ícono key
    * Automatically create a password + Require change at first sign-in -> Reset password -> OK (Pradeep no es admin)

### Como Lynne: bloquear cuentas
* [MENU] Active users -> tildar checkbox **Alex Wilber** (solo el de él)
  * [MENU] ... (ellipsis) -> Edit sign-in status
    * Tildar **Block this user from signing in** -> Save changes -> OK
* Repetir con **Nestor Wilke**
  * ⚠️ Error esperado: Nestor es Global Admin, Lynne no puede bloquearlo
* Sign out Lynne

### Verificar bloqueo de Alex
* [WINDOWS] Browser -> https://www.microsoft365.com -> Use another account -> login **AlexW@...**
  * Verificar error: **"Your account has been locked..."**
  * (puede tardar unos minutos en propagar el bloqueo)

## Desbloquear Alex (como Holly)
* [WINDOWS] LON-CL1 -> Browser (ya logueado como Holly)
* [MENU] Active users -> checkbox **Alex Wilber**
  * [MENU] ... -> Edit sign-in status
    * Destildar **Block this user from signing in** -> Save changes
> [!NOTE]
> Puede tardar hasta 15 min en propagar, no hace falta verificar el login de nuevo

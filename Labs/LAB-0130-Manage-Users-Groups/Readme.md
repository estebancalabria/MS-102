# LAB-0130-Manage-Users-Groups


## Verificar asignacion Licencias a Usuarios

* Verificar las licenias disponibles para asingar

* [MENU] BILLING -> Licenceses
  * [TAB] Subscriptions
    * Si no hay licencias disponibles hay que sacarsela a alguien

* [MENU] Users -> Active users
  * Sacarle la licencia a un usuario por ejemplo elegir "Lidia Holloway"
  * Seleccionar el usuario
    * [TAB] "Licenses and aps"
      * Deseleccionar la licencia Microsoft 365 E% (no Teams)
      * Salvar Cambios

* [MENU] BILLING -> Licenceses
  * [TAB] Subscriptions
    * Verificar que hay una licencia mas disponible

## Agregar Usuario

* [MENU] Users - > Active USers
 * [LINK] Add a User
   * [TAB] Basics
     * Fist Name : Holly
     * Last Name : Dickson
     * Username : holly
   * [TAB] Licencses
     * Microsoft 365 E5 (no teams)
     * Microsoct Teams Enterprise
   * [TAB] Roles
     * Global Administrator

> [!NOTE]
> Copiar los datos del usuario generado y el password

* [BROWSER] Abrir una nueva ventana de incognito en otro browser
   * http://admin.microsoft.com/
   * Loguearse con lo nuevos usuarios
   * Cambiar el password
 
# Administrar Grupos

* [MENU] Teams & groups -> Active teams & groups
  * [TAB] Temas & Microsoft 365 groups
   * [LINK] + Add a Microsoft 365 group
     * Basics
       * Name : M365 pilot project.
       * Owner : Holly
      * Members
        * ...
      * Settings
       * Privacy : Public
       * Group email address : pilot@...

* [MENU] Teams & groups -> Active teams & groups
  * [TAB] Teams & Microsoft 365 groups
    * Seleccionar el grupo (ej: M365 pilot project) -> ⋮ More actions -> Delete team
    * Confirmar Delete team
      
* [MENU] Teams & groups -> Deleted groups
  * Verificar que aparece el grupo eliminado

# Administrar Grupos y Usuarios dede Powershell

* [TASKBAR] Abrir Powershell

* Conectarnos a MSGraph

```powershell
Connect-MgGraph -Scopes 'Group.ReadWrite.All', 'Directory.ReadWrite.All'
```

* Listar Grupos

```powershell
Get-MgGroup -Sort 'DisplayName'
```

* Ver los grupos eliminads

```powershell
Get-MgDirectoryDeletedItemAsGroup
```

* Restaurar grupo eliminado

```powershell
Restore-MgDirectoryDeletedItem -DirectoryObjectId 'paste in the object ID for the Inside Sales group here'
```

* Verificar que el grupo se ha establecido

```powershell
Get-MgGroup -Sort 'DisplayName'
```

* Verificar tambien en el portal

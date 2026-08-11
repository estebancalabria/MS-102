# Microsoft 365 – Administración de usuarios, identidades y colaboración externa

## 1. Modelos de identidad

Microsoft Entra ID puede trabajar con tres modelos principales:

### Cloud-only

Las identidades se crean y administran directamente en Microsoft Entra ID. La autenticación se realiza en la nube de Microsoft.

### Synchronized / Hybrid

Las identidades se mantienen en **Active Directory Domain Services (AD DS)** local y se sincronizan con Microsoft Entra ID mediante herramientas como Microsoft Entra Connect.

### Federated

La autenticación se delega a un **proveedor de identidad (IdP)** externo mediante una relación de confianza. El usuario se autentica ante el proveedor federado y este proporciona la información/token de autenticación que Microsoft Entra ID acepta.

**Resumen:**

| Modelo                | Identidad                  | Autenticación                  |
| --------------------- | -------------------------- | ------------------------------ |
| Cloud-only            | Microsoft Entra ID         | Microsoft Entra ID             |
| Synchronized / Hybrid | AD DS + Microsoft Entra ID | Según configuración híbrida    |
| Federated             | Puede estar en otro IdP    | Proveedor de identidad externo |

---

# 2. Manage user licenses in Microsoft 365

Los servicios cloud de Microsoft, como **Microsoft 365, Enterprise Mobility + Security y Dynamics 365**, requieren licencias asignadas a los usuarios.

**Microsoft Entra ID** es la infraestructura subyacente para la administración de identidades de los servicios Microsoft Cloud y almacena información sobre los estados de asignación de licencias.

### Administración de licencias

Los roles que pueden asignar o quitar licencias son:

* **Global Administrator**
* **User Management Administrator**

Pueden administrar licencias de usuarios individuales o múltiples usuarios.

Cuando se asigna una licencia, el sistema habilita automáticamente los servicios correspondientes para el usuario.

### Importante al quitar una licencia

Al quitar una licencia de un usuario:

* Los datos asociados a los servicios se eliminan mediante un proceso de **soft-delete**.
* Existe un período de recuperación de **30 días**.
* Después de los 30 días, los datos **no son recuperables**.

### Consultar licencias

En el Microsoft 365 admin center:

**Billing → Licenses → Subscriptions**

Permite consultar:

* Licencias disponibles.
* Licencias asignadas.
* Uso de las suscripciones.

Para encontrar usuarios sin licencia:

**Users → Active users → Filter → Unlicensed users**

### Asignación masiva

Seleccionando varios usuarios:

**Users → Active users → Manage product licenses**

Opciones:

* **Replace:** reemplaza las licencias existentes por las nuevas.
* **Assign more:** conserva las existentes y agrega otras.
* **Unassign all:** elimina todas las licencias.

---

## Microsoft Graph PowerShell para licencias

Conexión:

```powershell
Connect-MgGraph -Scopes User.ReadWrite.All, Organization.Read.All
```

Consultar los planes disponibles:

```powershell
Get-MgSubscribedSku
```

Las licencias disponibles se calculan como:

```text
ActiveUnits - WarningUnits - ConsumedUnits
```

### Buscar usuarios sin licencia

```powershell
Get-MgUser -Filter 'assignedLicenses/$count eq 0' `
  -ConsistencyLevel eventual `
  -CountVariable unlicensedUserCount `
  -All
```

Usuarios sincronizados sin licencia:

```powershell
Get-MgUser -Filter 'assignedLicenses/$count eq 0 and OnPremisesSyncEnabled eq true' `
  -ConsistencyLevel eventual `
  -CountVariable unlicensedUserCount `
  -All `
  -Select UserPrincipalName
```

### UsageLocation

Para asignar licencias, el usuario debe tener configurada la propiedad **UsageLocation** con un código válido ISO 3166-1 alpha-2, por ejemplo:

* `US`
* `FR`

Buscar usuarios sin UsageLocation:

```powershell
Get-MgUser -Select Id,DisplayName,Mail,UserPrincipalName,UsageLocation,UserType |
where { $_.UsageLocation -eq $null -and $_.UserType -eq 'Member' }
```

Asignar UsageLocation:

```powershell
$userUPN="<user sign-in name (UPN)>"
$userLoc="<ISO 3166-1 alpha-2 country code>"

Update-MgUser -UserId $userUPN -UsageLocation $userLoc
```

### Asignar una licencia

```powershell
Set-MgUserLicense `
  -UserId $userUPN `
  -AddLicenses @{SkuId = $e5Sku.SkuId} `
  -RemoveLicenses @()
```

También se pueden:

* Asignar varias licencias.
* Quitar licencias.
* Asignar una licencia deshabilitando determinados **service plans**.

Permiso necesario para administrar licencias:

**User.ReadWrite.All** o permisos equivalentes definidos para la operación de asignación de licencias.

Para consultar las licencias disponibles se requiere:

**Organization.Read.All**

---

# 3. Recover deleted user accounts in Microsoft 365

Cuando se elimina un usuario:

* El usuario deja de poder iniciar sesión.
* La licencia asignada queda disponible para asignarla a otro usuario.
* La cuenta permanece como **soft-deleted** durante **30 días**.

Durante ese período puede restaurarse.

## Eliminar usuarios

Desde Microsoft 365 admin center:

**Users → Active users → seleccionar usuario → Delete user**

También puede utilizarse:

```powershell
Remove-MgUser -UserId '5c442efb-5e66-484a-936a-91b6810bed14'
```

## Restaurar usuarios

Desde Microsoft 365 admin center:

**Users → Deleted users → seleccionar usuario → Restore user**

También mediante Microsoft Graph PowerShell:

```powershell
Restore-MgDirectoryDeletedItem `
  -DirectoryObjectId '5c442efb-5e66-484a-936a-91b6810bed14'
```

Los objetos eliminados permanecen disponibles para recuperación durante **30 días**. Después se eliminan permanentemente.

---

# 4. Perform bulk user maintenance in Microsoft Entra ID

Microsoft Entra ID permite realizar operaciones masivas sobre usuarios mediante archivos **CSV**:

* Crear usuarios.
* Eliminar usuarios.
* Restaurar usuarios.

Para las operaciones masivas desde el portal se requiere:

* **Global Administrator**, o
* **User Administrator**.

## Crear usuarios en bulk

Ruta:

**Microsoft Entra admin center → Users → All users → Bulk operations → Bulk create**

Se descarga la plantilla CSV correspondiente.

La plantilla contiene:

1. Version number.
2. Column headings.
3. Examples row.

Los primeros dos elementos de la plantilla no deben modificarse ni eliminarse.

Los valores mínimos para crear usuarios son:

* **Name**
* **User principal name**
* **Initial password**
* **Block sign in (Yes/No)**

La contraseña debe cumplir la política de contraseñas vigente.

Después de cargar el CSV:

1. Se valida el archivo.
2. Se corrigen errores si existen.
3. Se selecciona **Submit**.
4. Se puede consultar el resultado en **Bulk operation results**.

Una operación de creación masiva puede ejecutarse durante hasta **una hora** y permite crear al menos **50.000 usuarios**.

### Verificar usuarios

En el portal:

**Users → All users**

Con Microsoft Graph PowerShell:

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
Import-Module Microsoft.Graph.Identity.DirectoryManagement
Connect-MgGraph -Scopes 'User.Read.All'
```

```powershell
Get-MgUser -Filter "UserType eq 'Member'"
```

---

## Eliminar usuarios en bulk

Ruta:

**Microsoft Entra admin center → Users → All users → Bulk operations → Bulk delete**

La plantilla requiere principalmente:

```text
User name [userPrincipalName] Required
```

Se carga el CSV y se ejecuta **Submit**.

El resultado puede consultarse en:

**Bulk operation results**

---

## Restaurar usuarios en bulk

Ruta:

**Microsoft Entra admin center → Users → Deleted users → Bulk restore**

A diferencia del bulk delete, la plantilla de restauración utiliza:

```text
Object ID [objectId] Required
```

El procedimiento es:

1. Descargar la plantilla.
2. Agregar los Object IDs.
3. Guardar el CSV.
4. Cargarlo.
5. Validarlo.
6. Seleccionar **Submit**.
7. Consultar el resultado.

---

## Crear usuarios en bulk con PowerShell

Conectar Microsoft Graph:

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
Import-Module Microsoft.Graph.Identity.DirectoryManagement
Connect-MgGraph -Scopes 'User.ReadWrite.All'
```

Ejemplo de CSV:

```csv
UserPrincipalName,FirstName,LastName,DisplayName,UsageLocation,AccountSkuId,Password
ClaudeL@contoso.onmicrosoft.com,Claude,Loiselle,Claude Loiselle,US,contoso:ENTERPRISEPACK,User.pw1
LynneB@contoso.onmicrosoft.com,Lynne,Baxter,Lynne Baxter,US,contoso:ENTERPRISEPACK,User.pw2
ShawnM@contoso.onmicrosoft.com,Shawn,Melendez,Shawn Melendez,US,contoso:ENTERPRISEPACK,User.pw3
```

Importar el CSV y crear los usuarios:

```powershell
Import-Csv -Path "<Input CSV File Path and Name>" |
foreach {
    New-MgUser `
      -DisplayName $_.DisplayName `
      -GivenName $_.FirstName `
      -Surname $_.LastName `
      -UserPrincipalName $_.UserPrincipalName `
      -UsageLocation $_.UsageLocation `
      -LicenseAssignmentStates $_.AccountSkuId `
      -PasswordProfile $_.Password
} |
Export-Csv -Path "<Output CSV File Path and Name>"
```

El archivo de salida permite revisar los resultados de la operación.

---

# 5. Create and manage guest users using B2B collaboration

**Microsoft Entra B2B collaboration** permite que personas externas colaboren con usuarios de una organización utilizando sus propias credenciales.

El usuario externo:

1. Recibe una invitación.
2. Se autentica con su propio proveedor de identidad.
3. Accede únicamente a las aplicaciones y recursos compartidos.
4. Es representado como un objeto de usuario dentro del tenant de la organización.

Normalmente el usuario B2B tiene:

```text
UserType = Guest
```

y su UPN contiene:

```text
#EXT#
```

Ejemplo:

```text
john_contoso.com#EXT#@fabrikam.onmicrosoft.com
```

## Tipos de usuarios

### External guest

Usuario externo con cuenta en otra organización de Microsoft Entra o en otro proveedor de identidad y permisos de invitado.

```text
UserType = Guest
```

### External member

Usuario externo que recibe acceso de nivel **Member** en la organización de recursos.

```text
UserType = Member
```

Es habitual en organizaciones con múltiples tenants.

### Internal guest

Usuario con credenciales internas que históricamente fue configurado como invitado.

Puede migrarse a B2B para que utilice sus propias credenciales externas.

### Internal member

Usuario interno de la organización.

```text
UserType = Member
```

---

# 6. Guest access en Microsoft 365

Los invitados pueden utilizarse en:

* Microsoft Teams
* SharePoint
* OneDrive
* Microsoft 365 Groups
* Planner
* Lists
* Power Apps
* Yammer

Las aplicaciones de Office, como Word y Excel, controlan el acceso de invitados según dónde se almacena el archivo: SharePoint, Teams, OneDrive, etc.

## Configuración de colaboración externa

Para invitar invitados se necesita un rol apropiado, por ejemplo:

* Global Administrator
* User Administrator
* Guest Inviter

La organización puede configurar:

* Quién puede invitar invitados.
* Qué dominios pueden recibir invitaciones.
* Qué pueden visualizar los invitados.
* Self-service sign-up.
* Restricciones de colaboración.
* Cross-tenant access settings.

---

# 7. UserType, Identities y UPN en B2B

### UserType

Indica la relación del usuario con la organización anfitriona:

* **Member**
* **Guest**

No indica cómo se autentica el usuario.

### Identities

Indica el proveedor de identidad utilizado para autenticarse.

Algunos valores posibles:

| Identities          | Autenticación                            |
| ------------------- | ---------------------------------------- |
| `ExternalAzureAD`   | Otra organización Microsoft Entra        |
| `Microsoft account` | Cuenta Microsoft                         |
| `google.com`        | Google                                   |
| `facebook.com`      | Facebook                                 |
| `mail`              | Email OTP de Microsoft Entra External ID |
| `{issuer URI}`      | Proveedor SAML/WS-Fed                    |
| `{host domain}`     | Credenciales del tenant anfitrión        |

**Importante:** `UserType` e `Identities` son propiedades independientes.

---

# 8. Guest access permissions

Microsoft Entra ID permite limitar lo que pueden consultar los invitados.

Hay tres niveles:

| Nivel                        | Acceso                                                                    |
| ---------------------------- | ------------------------------------------------------------------------- |
| **Same as member users**     | Los invitados tienen el mismo acceso a recursos de Entra que los miembros |
| **Limited access (default)** | Pueden ver la membresía de grupos no ocultos                              |
| **Restricted access**        | No pueden ver la membresía de ningún grupo                                |

Con **Restricted access**, el invitado puede consultar únicamente su propio perfil y no puede consultar otros usuarios ni siquiera mediante UPN u Object ID.

No se requieren licencias para restringir el acceso de invitados.

---

# 9. External collaboration settings

Las configuraciones permiten controlar:

### Determine guest user access

Define qué información del directorio pueden consultar los invitados.

### Specify who can invite guests

Por defecto, los usuarios de la organización pueden invitar invitados, aunque esto puede restringirse a determinados roles.

### Guest self-service sign-up

Permite crear flujos de registro para que usuarios externos se registren directamente en aplicaciones.

### Allow or block domains

Permite establecer dominios permitidos o bloqueados.

### Cross-tenant access

Para colaboración B2B entre organizaciones Microsoft Entra se deben revisar las configuraciones de **cross-tenant access**, que permiten controlar:

* Acceso entrante.
* Acceso saliente.
* Usuarios.
* Grupos.
* Aplicaciones.

---

# 10. Invitation redemption

Cuando se envía una invitación B2B:

* Se crea inmediatamente un objeto de usuario en el tenant.
* Inicialmente no tiene credenciales propias.
* La autenticación se realiza mediante el proveedor de identidad del invitado.
* El estado aparece como:

```text
External user state = PendingAcceptance
```

El usuario que envía la invitación se establece como valor predeterminado del atributo **Sponsor (preview)**.

Las invitaciones B2B **no expiran**.

Después de aceptar la invitación, la propiedad **Identities** se actualiza según el proveedor utilizado.

---

# 11. Agregar invitados a Microsoft Entra ID

Ruta:

**Microsoft Entra admin center → Users → All users → +New user → Invite external user**

Se proporciona:

* Email.
* Display name.
* Opcionalmente mensaje de invitación.
* Información de perfil.
* Grupos.
* Roles.

Después de seleccionar **Review + Invite → Invite**, Microsoft Entra crea el usuario como invitado.

El UPN utiliza el formato:

```text
emailaddress#EXT#@domain
```

No se admiten direcciones de grupos como dirección de invitación y Microsoft Entra ID actualmente no admite el uso del signo `+` en las direcciones de email para estas invitaciones.

---

# 12. Agregar invitados a grupos

Los invitados pueden agregarse a grupos existentes o nuevos.

Ruta:

**Microsoft Entra admin center → Groups → All groups → grupo → Members → +Add members**

También pueden utilizarse **dynamic groups** con Microsoft Entra B2B collaboration.

---

# 13. Agregar invitados a aplicaciones

Ruta:

**Microsoft Entra admin center → Applications → Enterprise applications → aplicación → Users and groups → Add user/group**

Se selecciona el invitado y se asigna:

* La aplicación.
* El rol correspondiente, si la aplicación dispone de varios roles.

Por defecto, la asignación aparece con:

```text
Default Access
```

---

# 14. Collaborate with guests in a SharePoint site

Para permitir colaboración con invitados en SharePoint deben configurarse correctamente **cuatro niveles principales de control**:

1. Microsoft Entra external collaboration.
2. Microsoft 365 Groups.
3. SharePoint organization-level sharing.
4. SharePoint site-level sharing.

## Paso 1 – Microsoft Entra external collaboration

Ruta:

**Microsoft Entra admin center → External identities → External collaboration settings**

Debe permitirse la invitación de invitados.

También deben revisarse:

* Collaboration restrictions.
* Dominios bloqueados.
* Guest user access restrictions.

---

## Paso 2 – Microsoft 365 Groups

Ruta:

**Microsoft 365 admin center → Settings → Org settings → Microsoft 365 Groups**

Deben estar habilitadas ambas opciones:

* **Let group owners add people outside your organization to Microsoft 365 Groups as guests**
* **Let guest group members access group content**

---

## Paso 3 – SharePoint organization-level sharing

Ruta:

**SharePoint admin center → Policies → Sharing**

Para SharePoint se puede seleccionar:

* **Anyone**
* **New and existing guests**

### Anyone

Permite compartir archivos y carpetas incluso con personas que no se autentican.

### New and existing guests

Exige que las personas externas se autentiquen.

El nivel de organización establece el límite máximo que pueden utilizar los sitios individuales.

---

## Paso 4 – Crear el sitio

Ruta:

**SharePoint admin center → Sites → Active sites → Create → Team site**

Se configura:

* Nombre del sitio.
* Group owner / Site owner.
* Public o Private.
* Finalizar con **Finish**.

---

## Paso 5 – Site-level sharing

Ruta:

**SharePoint admin center → Sites → Active sites → seleccionar sitio → Settings → More sharing settings**

El sitio puede configurarse como:

* **Anyone**
* **New and existing guests**

El nivel del sitio **no puede ser más permisivo que el nivel de organización**.

Un sitio no puede compartirse directamente con personas no autenticadas mediante **Anyone**, aunque archivos y carpetas individuales sí pueden compartirse de esa manera.

También pueden utilizarse **sensitivity labels** para controlar la configuración de colaboración externa.

---

## Paso 6 – Invitar usuarios

El acceso al sitio está controlado mediante el **Microsoft 365 Group asociado**.

Para agregar usuarios internos:

**Site → Members → Add members**

Los invitados no se agregan directamente al grupo desde el sitio; deben gestionarse mediante el grupo asociado.

---

# 15. Create and manage contacts

Los **mail contacts** son personas externas a la organización que deben ser visibles para los usuarios internos y a quienes se puede enviar correo.

Son objetos habilitados para correo en **Exchange Online** que:

* Tienen una dirección de email externa.
* Aparecen en la **Global Address List (GAL)**.
* No necesitan una cuenta de usuario en el directorio.

## Mail contacts vs. mail users

| Tipo             | Dirección                             |
| ---------------- | ------------------------------------- |
| **Mail user**    | Dentro del dominio de la organización |
| **Mail contact** | Fuera del dominio de la organización  |

Un mail contact puede utilizarse para representar a:

* Proveedores.
* Clientes.
* Socios.
* Otros contactos externos.

---

## Permisos para crear contactos

Se puede utilizar:

* **Global Administrator**
* **Exchange Administrator**
* **Directory Writers**

---

## Crear un contacto

Ruta:

**Microsoft 365 admin center → Users → Contacts → Add a contact**

Datos principales:

* First name.
* Last name.
* **Display name** — obligatorio.
* **Email** — obligatorio y debe ser externo.
* Hide from Global Address List.
* Información de perfil.
* Mail tip.

Los cambios pueden tardar aproximadamente **30 minutos** en aplicarse.

---

## Eliminar un contacto

Ruta:

**Users → Contacts → seleccionar contacto → Delete contact**

El Microsoft 365 admin center no permite actualmente la edición o eliminación masiva de mail contacts.

Para operaciones masivas se utiliza:

* Exchange admin center clásico.
* Exchange Online PowerShell.

---

# 16. Exchange Online PowerShell para contactos

### Crear

```powershell
New-MailContact `
  -Name "Debra Garcia" `
  -ExternalEmailAddress dgarcia@tailspintoys.com `
  -Alias dgarcia
```

### Consultar y modificar

Para propiedades generales:

```powershell
Get-Contact
Set-Contact
```

Para propiedades relacionadas con correo:

```powershell
Get-MailContact
Set-MailContact
```

Ejemplo:

```powershell
Set-Contact "Allan Deyoung" `
  -Title Consultant `
  -Department "Public Relations" `
  -Company Fabrikam `
  -Manager "Alex Wilber"
```

Ocultar todos los contactos de las listas de direcciones:

```powershell
$Contacts = Get-MailContact -ResultSize unlimited

$Contacts | foreach {
    Set-MailContact `
      -Identity $_ `
      -CustomAttribute1 PartTime `
      -HiddenFromAddressListsEnabled $true
}
```

Modificar contactos de un departamento:

```powershell
$PR = Get-Contact `
  -ResultSize unlimited `
  -Filter "Department -eq 'Public Relations'"

$PR | foreach {
    Set-MailContact `
      -Identity $_ `
      -CustomAttribute15 TemporaryEmployee
}
```

### Eliminar

```powershell
Remove-MailContact -Identity "Nestor Wilke"
```

---

# Puntos clave para recordar

* **Microsoft Entra ID** es la base de identidad de los servicios Microsoft Cloud.
* Los tres modelos de identidad son **Cloud-only, Synchronized/Hybrid y Federated**.
* Las licencias pueden administrarse desde el Microsoft 365 admin center o Microsoft Graph PowerShell.
* Al quitar una licencia, los datos de servicio tienen un período de recuperación de **30 días**.
* Un usuario eliminado permanece **soft-deleted durante 30 días** y puede restaurarse.
* Las operaciones masivas de usuarios utilizan **CSV**.
* Para bulk create, delete y restore existen plantillas CSV diferentes.
* **B2B collaboration** permite que usuarios externos accedan a recursos utilizando sus propias credenciales.
* Un invitado B2B normalmente tiene `UserType = Guest` y un UPN con `#EXT#`.
* **UserType** e **Identities** son propiedades independientes.
* Los invitados pueden tener acceso **Same as member, Limited o Restricted**.
* Las invitaciones B2B tienen estado inicial **PendingAcceptance** y no expiran.
* Para SharePoint, la configuración de colaboración debe estar permitida en **Microsoft Entra, Microsoft 365 Groups, SharePoint a nivel organización y SharePoint a nivel sitio**.
* El nivel de sharing de un sitio no puede ser más permisivo que el nivel de la organización.
* Un **mail contact** representa a una persona externa sin crearle una cuenta de usuario.
* Los mail contacts tienen una dirección externa y aparecen en la **GAL**.
* Para administrar contactos mediante PowerShell se utilizan principalmente `Get-Contact`, `Set-Contact`, `Get-MailContact`, `Set-MailContact`, `New-MailContact` y `Remove-MailContact`.

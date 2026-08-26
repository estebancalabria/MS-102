# Sincronización de directorios e identidades

## Identidad y sincronización de directorios

* La sincronización de directorios permite sincronizar identidades u objetos entre distintos directorios.
* En Microsoft 365, normalmente sincroniza objetos de Active Directory local con Microsoft Entra ID.
* Puede utilizarse con otros directorios, como bases de datos de RR. HH. o directorios LDAP.
* En escenarios de identidad híbrida, la sincronización permite que usuarios y permisos del entorno local estén disponibles en Microsoft Entra ID para Microsoft 365 y aplicaciones alojadas en la nube.
* Existen escenarios de identidad solo en la nube e híbrida.
* La autenticación híbrida puede utilizar Password Hash Synchronization (PHS), Pass-through Authentication (PTA) o federación con AD FS/WAP.
* PHS sincroniza un hash de la contraseña, no la contraseña real, desde Active Directory local hacia Microsoft Entra ID.
* Se recomienda habilitar PHS.

## Administración de usuarios sincronizados

* Después de sincronizar objetos de Active Directory local con Microsoft 365, la autoridad de administración vuelve a Active Directory local.
* Los usuarios sincronizados no se pueden administrar desde el Microsoft 365 admin center ni desde Exchange Online admin center (EAC).
* Los usuarios pueden crearse, modificarse y eliminarse mediante:

  * Active Directory Users and Computers.
  * Windows PowerShell en Active Directory local.
* Los cambios realizados en atributos administrados desde Microsoft 365 no se sincronizan nuevamente al entorno local.
* Algunos atributos no existen en Active Directory local y deben administrarse en Microsoft 365, como:

  * Licencias de productos de Microsoft 365.
  * Configuraciones avanzadas de Exchange Online, como In-Place Archiving.

### Recuperación de usuarios eliminados

* Microsoft Entra ID admite soft delete, incluso cuando un usuario se elimina en Active Directory local y la eliminación se sincroniza con Microsoft 365.
* El usuario eliminado deja de aparecer en la lista de usuarios activos.
* La licencia queda disponible para ser reasignada.
* El objeto puede recuperarse durante 30 días.
* Puede recuperarse desde Microsoft 365 admin center o mediante PowerShell con `Restore-MgDirectoryDeletedItem`.
* Si se recupera el objeto eliminado desde la papelera de reciclaje de Active Directory, se restablece el vínculo entre las cuentas.
* Si Active Directory no tiene habilitada la papelera de reciclaje, se debe crear una nueva cuenta con un nuevo GUID.
* Una vez realizado un hard delete de la papelera de reciclaje en la nube, las cuentas eliminadas no pueden restaurarse.

### Eliminaciones no sincronizadas

* Una eliminación realizada en Active Directory local puede no eliminar el objeto correspondiente de Microsoft Entra ID si la sincronización no se completa o falla.
* El objeto que permanece en Microsoft Entra ID se denomina **orphaned Microsoft Entra object**.
* Para resolverlo:

  1. Ejecutar manualmente una sincronización, por ejemplo `Start-ADSyncSyncCycle -PolicyType Delta`.
  2. Verificar en Synchronization Service Manager que las sincronizaciones finalicen con estado **Success**.
  3. Verificar en Microsoft 365 admin center que los objetos se hayan eliminado correctamente.
* Si el objeto huérfano permanece, puede eliminarse manualmente con:

  * `Remove-MgUser`
  * `Remove-MgContact`
  * `Remove-MgGroup`

### Movimiento de un usuario fuera de sincronización

* Un usuario puede quedar fuera de sincronización cuando sus datos se actualizan en un controlador de dominio y todavía no se replican en los demás.
* Mover el usuario a otra OU o contenedor fuerza la replicación de su estado actualizado a los demás controladores.
* Si Microsoft Entra Connect Sync detecta posteriormente que el usuario ya no está en su OU esperada, puede asumir que fue eliminado o movido y realizar un soft delete del usuario correspondiente en Microsoft Entra ID.
* Si el usuario vuelve a su OU original dentro de 30 días, Microsoft Entra Connect Sync reactiva el usuario en Microsoft Entra ID durante la siguiente sincronización.
* Si no vuelve dentro de 30 días, el usuario soft-deleted se elimina permanentemente.

## Administración de grupos

* Después de implementar la sincronización entre Active Directory local y Microsoft Entra ID, la pertenencia a grupos debe administrarse en Active Directory local.
* Microsoft Entra Connect Sync y Microsoft Entra Cloud Sync pueden implementar la sincronización de directorios.
* La sincronización de grupos funciona de forma similar a la de usuarios: los grupos y sus miembros se sincronizan desde Active Directory local hacia Microsoft Entra ID.
* Group writeback permite escribir grupos de Microsoft 365 desde Microsoft Entra ID hacia Active Directory local.

### Group writeback con Microsoft Entra Connect Sync

* Group writeback es una característica opcional de Microsoft Entra Connect Sync.
* Requiere Exchange 2013 CU8 o posterior, o Exchange 2016.
* Se debe crear la OU y configurar los permisos necesarios en Active Directory local.
* `Initialize-ADSyncGroupWriteBack` prepara automáticamente Active Directory.
* Los grupos de Microsoft 365 aparecen en el contenedor local seleccionado y también como grupos de distribución en Active Directory local.
* Group writeback no involucra security groups ni distribution groups.
* Para que los grupos sincronizados aparezcan rápidamente en la Global Address List local se pueden utilizar:

  * `Update-Recipient`
  * `Update-AddressList`
  * `Update-GlobalAddressList`
* La sincronización de la pertenencia de grupos solo incluye usuarios creados en Active Directory local; los usuarios creados en Microsoft Entra ID no se incluyen en la pertenencia sincronizada.
* Al sincronizar un grupo, su atributo `name` se completa con `ObjectGUID` en lugar de un nombre legible.

### Group writeback con Microsoft Entra Cloud Sync

* Microsoft Entra Cloud Sync inicialmente no admitía group writeback.
* Con el provisioning agent **1.1.1370.0**, Microsoft Entra Cloud Sync incorpora group writeback en Preview.
* Permite aprovisionar grupos directamente en Active Directory local.

## Microsoft Entra Connect Sync Security Groups

Durante la configuración, Microsoft Entra Connect Sync crea automáticamente grupos de seguridad para:

* Delegar el control de Microsoft Entra Connect Sync a otros usuarios.
* Asignar temporalmente a un usuario permisos para ejecutar una sincronización manual.
* Solucionar problemas de sincronización.

### Grupos creados

| Grupo               | Función                                                                                                                                                                     |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ADSyncAdmins`      | Acceso completo al Microsoft Entra Connect Sync Service Manager.                                                                                                            |
| `ADSyncOperators`   | Permite ejecutar Management Agents, consultar estadísticas de sincronización y guardar el historial de ejecuciones. Sus miembros también deben pertenecer a `ADSyncBrowse`. |
| `ADSyncBrowse`      | Permite obtener información sobre el lineage de un usuario al restablecer contraseñas.                                                                                      |
| `ADSyncPasswordSet` | Permite realizar operaciones mediante la interfaz de administración de contraseñas. Sus miembros también deben pertenecer a `ADSyncBrowse`.                                 |

* Los grupos pueden crearse como grupos locales en servidores unidos al dominio o como grupos de dominio de Active Directory local cuando Microsoft Entra Connect Sync se instala en un controlador de dominio.
* Para crear grupos de dominio en servidores miembro se debe seleccionar **Specify Custom Sync Groups** y especificar los grupos mediante `Domain\Group Name`.

## Filtrado de objetos

* Object filtering controla qué objetos de Active Directory local se sincronizan con Microsoft Entra ID.
* La configuración predeterminada sincroniza todos los objetos de todos los dominios de los bosques configurados.
* La configuración predeterminada proporciona una Global Address List completa.
* El filtrado puede utilizarse, por ejemplo, para:

  * Sincronizar solo un subconjunto de usuarios durante un piloto.
  * Excluir cuentas de servicio y otras cuentas no personales.
  * Sincronizar únicamente cuentas activas cuando las cuentas deshabilitadas se conservan en Active Directory local.

### Tipos de filtrado

* **Group-based:** basado en un único grupo. Se configura durante la instalación inicial. Proporciona control granular, facilita la administración y reduce tráfico, pero tiene opciones limitadas, puede generar errores de configuración y puede ralentizar las sincronizaciones con muchos objetos.

* **Domain-based:** permite seleccionar qué dominios se sincronizan y modificar posteriormente los dominios incluidos.

* **OU-based:** permite seleccionar qué OUs se sincronizan, incluyendo todos los tipos de objetos de las OUs seleccionadas.

* **Object attribute-based:** permite filtrar según los valores de atributos y utilizar filtros diferentes para distintos tipos de objetos.

* Se pueden combinar varios tipos de filtrado.

* Cuando se combinan filtros, se aplica una lógica **AND**.

* Group, domain y OU filtering están disponibles en Microsoft Entra Connect Sync y Microsoft Entra Cloud Sync.

* Object attribute filtering está disponible únicamente en Microsoft Entra Connect Sync.

### Cambios y eliminación de objetos por filtrado

* En Microsoft Entra Connect Sync, el filtrado puede habilitarse en cualquier momento.
* Si inicialmente se sincronizaban todos los objetos y posteriormente se configura un filtro, los objetos filtrados dejan de sincronizarse y los objetos previamente sincronizados pueden eliminarse de Microsoft Entra ID.
* Al instalar o actualizar Microsoft Entra Connect Sync, la configuración de filtrado se conserva.
* Antes de la primera sincronización después de una actualización se debe verificar que la configuración no haya cambiado.
* Si existen varios bosques, el filtrado debe configurarse en cada bosque cuando se desea la misma configuración.
* **Prevent accidental deletes** está habilitado de forma predeterminada para evitar eliminaciones masivas accidentales.
* Cuando el filtrado provoca la eliminación de muchos objetos, 500 por defecto, se deben realizar pasos de verificación antes de permitir las eliminaciones.
* Los usuarios eliminados accidentalmente por un filtro pueden recuperarse quitando la configuración de filtrado y sincronizando nuevamente, lo que permite restaurarlos desde la papelera de reciclaje de Microsoft Entra ID.
* Otros tipos de objetos, como grupos de seguridad, no pueden recuperarse de esta manera.

### Scheduler durante cambios de filtrado

* Antes de modificar los filtros se debe deshabilitar el scheduler que ejecuta una sincronización cada 30 minutos:

```powershell
Set-ADSyncScheduler -SyncCycleEnabled $False
```

* Después de realizar y verificar los cambios se vuelve a habilitar:

```powershell
Set-ADSyncScheduler -SyncCycleEnabled $True
```

### Aplicación y verificación de filtros

* Después de modificar la configuración se deben aplicar los cambios a los objetos existentes.
* Con domain-based u OU-based filtering se requiere un **Full import** seguido de una **Delta synchronization**.
* Con attribute-based filtering se requiere una **Full synchronization**.
* Los cambios quedan preparados para exportación antes de enviarse a Microsoft Entra ID.
* Se pueden descargar los cambios preparados en un archivo CSV y revisarlos en Microsoft Excel.
* El proceso de revisión puede repetirse hasta obtener los cambios esperados.
* Una vez verificados, los cambios se exportan a Microsoft Entra ID y se vuelve a habilitar el scheduler.

## Enhanced user management

Microsoft Entra Connect Sync y Microsoft Entra Cloud Sync proporcionan características como:

* Password writeback.
* Device writeback.

### Password writeback

* Permite que los usuarios cambien o restablezcan sus contraseñas desde la nube y que la contraseña actualizada se escriba nuevamente en Active Directory local.
* Requisitos:

  * Controladores de dominio Windows Server 2008 o superior.
  * Licencia Microsoft Entra Premium.
  * Configuración de Self-Service Password Reset (SSPR).
* Primero se debe habilitar password writeback en la herramienta de sincronización y luego configurarlo para SSPR.

### Password writeback con Microsoft Entra Connect Sync

* Durante la instalación se debe seleccionar **Custom Setup** y habilitar **Password writeback**.
* También puede habilitarse posteriormente mediante:

  1. Abrir el asistente de Microsoft Entra Connect Sync.
  2. Seleccionar **Configure**.
  3. Seleccionar **Customize synchronization options**.
  4. Autenticarse con credenciales de administrador global.
  5. Avanzar hasta **Optional features**.
  6. Seleccionar **Password writeback**.
  7. Completar la configuración.

### Password writeback con Microsoft Entra Cloud Sync

* Microsoft Entra Cloud Sync utiliza el Microsoft Entra cloud provisioning agent.
* Password writeback se habilita mediante:

```powershell
Import-Module 'C:\Program Files\Microsoft Azure AD Connect Provisioning Agent\Microsoft.CloudSync.Powershell.dll'

Set-AADCloudSyncPasswordWritebackConfiguration -Enable $true -Credential $(Get-Credential)
```

* Se requieren credenciales de administrador global.

### Password writeback para SSPR

* Después de habilitar password writeback en Microsoft Entra Connect Sync o Microsoft Entra Cloud Sync, se configura SSPR.
* En Microsoft Entra admin center:

  1. **Identity** → **Protection** → **Password reset**.
  2. En **Password reset | Properties**, seleccionar **On-premises integration**.
  3. Verificar el estado del agente correspondiente.
  4. En **Manage settings**, habilitar:

     * **Write back passwords with Microsoft Entra Cloud Sync**.
     * **Allow users to unlock accounts without resetting their password**.
  5. Seleccionar **Save**.

### Device writeback

* Device writeback permite aplicar Conditional Access basado en dispositivos a aplicaciones protegidas por AD FS o relying party trusts.
* Los dispositivos y usuarios deben estar en el mismo forest.
* No admite despliegues con múltiples user forests.
* Requisitos:

  * Suscripción Microsoft Entra Premium.
  * Active Directory con Windows Server 2012 R2 o posterior.
  * AD FS en Windows Server 2012 R2 (AD FS v3.0) o posterior.
  * Licencia Microsoft Entra Premium.
* Microsoft Entra Connect Sync y Microsoft Entra Cloud Sync admiten password writeback, pero **solo Microsoft Entra Connect Sync admite device writeback**.
* Para habilitar device writeback con Microsoft Entra Connect Sync se ejecuta el asistente dos veces:

  1. Primera ejecución para sincronizar usuarios y grupos.
  2. Segunda ejecución, en **Custom Setup**, para habilitar device writeback.
* Microsoft recomienda sincronizar correctamente todos los usuarios y grupos antes de habilitar device writeback.
* En la segunda ejecución:

  1. Seleccionar **Configure device options**.
  2. Seleccionar **Configure device writeback**.
  3. Verificar el **Device writeback forest**.
  4. Preparar Active Directory mediante credenciales de enterprise administrator o mediante el script `CreateDeviceContainer.ps1`.
* El asistente crea o configura:

  * `CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn]`
  * `CN=RegisteredDevices,[domain-dn]`
  * Permisos necesarios para la cuenta del Microsoft Entra Connector.
* El asistente solo necesita ejecutarse en un forest, aunque Microsoft Entra Connect Sync esté instalado en varios.
* Los dispositivos pueden tardar hasta tres horas en escribirse nuevamente en Active Directory local.
* Los dispositivos registrados pueden verificarse desde **Active Directory Administrative Center → RegisteredDevices**.

## Microsoft Identity Manager (MIM)

* Microsoft Identity Manager (MIM) es una solución de administración de identidades para gestionar y sincronizar identidades entre distintos sistemas y directorios.
* Proporciona capacidades de:

  * Provisioning y deprovisioning de usuarios.
  * Sincronización de identidades.
  * Self-service password reset.
  * Administración del ciclo de vida de identidades.
  * RBAC.
  * Workflows y procesos de aprobación.
  * Administración de certificados y smart cards.
  * Reporting y auditing.
* MIM ayuda a administrar usuarios, credenciales, políticas y acceso en organizaciones y entornos híbridos.
* Incluye workflows automatizados, reglas de negocio e integración con plataformas heterogéneas del datacenter.
* Es principalmente una solución **on-premises** y debe instalarse dentro de la infraestructura de la organización.
* Puede integrarse con Active Directory, LDAP, bases de datos SQL y otras aplicaciones mediante reglas de sincronización, conectores y APIs.
* MIM permite sincronizar identidades y atributos entre múltiples sistemas y directorios.
* Puede automatizar el provisioning y deprovisioning según eventos, reglas, workflows y fuentes de identidad.
* Permite definir roles y asignar derechos de acceso según las responsabilidades de los usuarios.
* Sus workflows permiten automatizar aprobaciones para tareas relacionadas con identidades.
* También proporciona capacidades para certificados, PKI y smart cards.
* Sus funciones de reporting y auditing permiten registrar y revisar actividades relacionadas con identidades y acceso.

### MIM frente a Microsoft 365

* **On-premises vs. Cloud:** MIM es principalmente on-premises, mientras Microsoft 365 es una suite de servicios cloud.
* **Integración local:** MIM está orientado a integrar sistemas, directorios y aplicaciones locales; Microsoft 365 se centra más en integraciones cloud y el ecosistema de Microsoft.
* **Flexibilidad:** MIM ofrece mayor capacidad de personalización, scripting y automatización mediante workflows.
* **Escenarios avanzados:** MIM puede utilizarse en escenarios complejos híbridos con sistemas locales y cloud.
* Microsoft 365 y Microsoft Entra ID ofrecen funcionalidades similares de administración de identidades y acceso en escenarios cloud.
* Una organización puede utilizar Microsoft 365, MIM o un enfoque híbrido según sus requisitos.
* MIM permite que Active Directory tenga los usuarios y permisos necesarios para aplicaciones locales.
* Microsoft Entra Connect y Microsoft Entra Connect Cloud Sync pueden hacer disponibles esos usuarios y permisos en Microsoft Entra ID para Microsoft 365 y aplicaciones cloud.

### Uso habitual de MIM

* Provisioning automático de identidades y grupos según políticas de negocio y workflows.
* Integración de directorios con sistemas de RR. HH. y otras fuentes de autoridad.
* Sincronización de identidades entre directorios, bases de datos y aplicaciones locales mediante APIs, protocolos y conectores.
* Protección de cuentas privilegiadas locales.
* La identidad digital está formada por:

**Credenciales + privilegios = identidad digital**

### Implementación de MIM

* La versión indicada es **Microsoft Identity Manager 2016 2.0**.
* La implementación requiere:

  1. Preparar el dominio de Active Directory local.
  2. Preparar los servidores de administración de identidades, incluyendo Windows Server, SQL Server y SharePoint Server.
  3. Instalar los componentes de MIM 2016 SP2:

     * MIM Synchronization Service.
     * MIM Service and Portal.
     * Sincronización de Active Directory y las bases de datos del servicio MIM.

## Troubleshooting de sincronización

* Los administradores de Microsoft 365 deben analizar logs y corregir errores de sincronización utilizando Microsoft Entra Connect Sync o Microsoft Entra Cloud Sync.
* Problemas habituales:

  * Errores de autenticación por credenciales incorrectas.
  * Desactivación accidental de la sincronización.
  * Cambios inesperados en Active Directory que afectan el alcance de OUs o el filtrado de atributos.
  * Active Directory local corrupto.
  * Atributos duplicados que deben ser únicos, como `UserPrincipalName` y `ProxyAddress`.

### Desactivar y reactivar la sincronización

* Al desactivar la sincronización de directorios, la autoridad pasa de Active Directory local a Microsoft 365.
* Esto puede realizarse cuando ya no se utiliza Active Directory local para crear y administrar usuarios, grupos, contactos y buzones.
* Al reactivar la sincronización, la autoridad vuelve a Active Directory local.
* **Al reactivar la sincronización, el proceso sobrescribe los cambios realizados en los objetos de Microsoft 365.**

### Duplicate attribute resiliency

* Microsoft Entra ID exige que `UserPrincipalName` y `ProxyAddress` sean únicos entre objetos User, Group y Contact del tenant.
* Si se intenta crear o actualizar un objeto con un valor duplicado, normalmente la operación falla.
* Duplicate attribute resiliency permite sincronizar el objeto aunque exista un conflicto.
* El atributo duplicado se pone en **quarantine**.
* Si el atributo es necesario para el provisioning, como `UserPrincipalName`, Microsoft Entra ID asigna temporalmente un valor con el formato:

```text
<OriginalPrefix>+<4DigitNumber>@<InitialTenantDomain>.onmicrosoft.com
```

* Si el atributo no es obligatorio, como `ProxyAddress`, el conflicto se pone en quarantine y el objeto puede crearse o actualizarse.
* El conflicto aparece en el informe de errores cuando se produce la quarantine, pero no continúa apareciendo en los informes posteriores.
* Como la exportación del objeto tiene éxito, el cliente de sincronización no registra un error ni vuelve a intentar la operación en los siguientes ciclos.
* El atributo `DirSyncProvisioningErrors` almacena los atributos en conflicto en los objetos User, Group y Contact.
* Una tarea ejecutada cada hora busca conflictos resueltos y elimina automáticamente los atributos correspondientes de quarantine.
* El proceso de resiliency se aplica a valores UPN y SMTP ProxyAddress.

### Ver errores de sincronización

* Microsoft 365 admin center proporciona una vista general de los errores.
* Para consultarlos:

  1. Iniciar sesión en Microsoft 365 admin center.
  2. En **Home**, abrir **User management**.
  3. Seleccionar **Sync errors** bajo **Microsoft Entra Connect**.
  4. Seleccionar un error para consultar sus detalles y recomendaciones.

### Notificación de sincronización no saludable

* Microsoft Entra Connect Sync informa por defecto mediante correo electrónico sobre errores de sincronización.
* El asunto del informe es **Directory Synchronization Error Report: Date + Time**.
* El correo se envía a la dirección de contacto técnico configurada en el tenant de Microsoft 365.

### Directory synchronization troubleshooter

* Microsoft Entra Connect Sync incluye una tarea de troubleshooting que identifica posibles problemas y proporciona orientación para corregirlos.
* Ofrece:

  * **Quick Scan:** analiza event logs y configuraciones de Microsoft 365.
  * **Full Scan:** ejecuta Quick Scan y además analiza objetos de Active Directory.
* Para ejecutar las comprobaciones se utiliza Microsoft 365 Support Assistant.
* El usuario debe tener al menos permisos de lectura en Active Directory local y en el tenant de Microsoft 365.

### Synchronization Service Manager

* Synchronization Service Manager permite revisar las operaciones de sincronización.
* En **Operations** se pueden comprobar:

  * Import en el AD Connector.
  * Import en el Microsoft Entra Connector.
  * Export en el AD Connector.
  * Export en el Microsoft Entra Connector.
  * Full Sync en el AD Connector.
  * Full Sync en el Microsoft Entra Connector.
* La sincronización se ejecuta por defecto cada 30 minutos.
* Se puede ejecutar manualmente desde **Connectors → Actions → Run** y seleccionar:

  * Full.
  * Delta.
  * Export.

También puede utilizarse PowerShell:

```powershell
Start-ADSyncSyncCycle -PolicyType Initial
```

Inicia una sincronización completa.

```powershell
Start-ADSyncSyncCycle -PolicyType Delta
```

Inicia una sincronización delta.

## Troubleshooting de Password Hash Synchronization

* Password Hash Synchronization es uno de los métodos de inicio de sesión para identidad híbrida.
* Microsoft Entra Connect Sync sincroniza un hash de la contraseña desde Active Directory local hacia Microsoft Entra ID, no la contraseña real.
* Permite a los usuarios utilizar la misma contraseña para iniciar sesión en Microsoft Entra ID y en Active Directory local.
* Las contraseñas se sincronizan casi en tiempo real, cada dos minutos.
* El scheduler de sincronización no realiza una sincronización completa de todas las contraseñas.
* Para realizar una sincronización completa de contraseñas se debe solicitar manualmente mediante PowerShell.
* Para problemas con un usuario concreto, no se debe seleccionar **User must change password at next logon** en Active Directory Users and Computers, ya que las contraseñas temporales no se sincronizan con Microsoft Entra ID.
* Si existe una regla inbound u outbound con `PasswordSync=True`, se deben revisar:

  * **In from AD – User AccountEnabled**
  * **Out to Microsoft Entra ID – User Join sync**

## Herramientas y tareas de troubleshooting

Las principales tareas y herramientas para solucionar problemas de sincronización incluyen:

* Desactivar y reactivar directory synchronization.
* Consultar errores desde Microsoft 365 admin center.
* Duplicate attribute resiliency.
* Notificaciones de identidad no saludable.
* Directory Synchronization Troubleshooter.
* Synchronization Service Manager.
* Troubleshooting de Password Hash Synchronization.

Otros problemas pueden estar relacionados con:

* Hashes de contraseña que no se sincronizan.
* Objetos sincronizados que no aparecen o no se actualizan en la nube.
* Falta de eventos recientes de sincronización.
* Problemas de conectividad.
* Cuentas y permisos de Microsoft Entra Connect.
* Exceso de cuota de objetos.
* Atributos sincronizados.
* Objetos que no pueden administrarse o eliminarse en la nube.
* Exceso del número de objetos que pueden sincronizarse.

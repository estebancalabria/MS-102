# Resumen — Roles administrativos en Microsoft 365

## Introducción

Microsoft 365 incluye roles administrativos que pueden asignarse a usuarios según funciones empresariales comunes. Estos roles otorgan permisos para realizar tareas específicas en los centros de administración.

El modelo de permisos de Microsoft 365 permite controlar **quién puede hacer qué y sobre qué recursos**, mediante:

* Roles.
* Grupos de roles.
* Ámbitos.
* Asignaciones.
* Unidades administrativas.
* Privileged Identity Management (PIM).

El módulo aborda la administración de roles en servicios como **Exchange Online, SharePoint Online, Teams y Microsoft Entra ID**, además de la delegación de roles a partners, la administración de permisos de SharePoint para evitar la exposición excesiva de datos y el uso de PIM para elevar privilegios de forma controlada.

También se estudian los roles administrativos integrados, como:

* Global Administrator.
* Service Administrator.
* Billing Administrator.
* User Management Administrator.

Los **grupos de roles** permiten asignar uno o más roles a un grupo en lugar de asignarlos directamente a usuarios. Los miembros del grupo heredan los roles asignados.

Las **unidades administrativas** y **Privileged Identity Management** permiten limitar el alcance de las asignaciones y proporcionar acceso **just-in-time** y **just-enough-access** a recursos sensibles.

---

## Modelo de permisos de Microsoft 365

Microsoft 365 utiliza un modelo basado en **Azure Role-Based Access Control (RBAC)**, donde los permisos se gestionan mediante **roles, ámbitos y asignaciones**.

### Roles

Los roles son conjuntos de permisos que permiten realizar tareas específicas.

Existen dos tipos:

* **Roles integrados (built-in roles):** vienen predefinidos y cubren los escenarios más comunes. Hay más de 30 roles integrados en Microsoft 365, como Exchange Administrator, SharePoint Administrator, Teams Administrator y Security Reader.
* **Roles personalizados (custom roles):** pueden crearse para necesidades específicas, basándose en roles existentes o desde cero, con permisos granulares para recursos o acciones concretas.

### Ámbitos (Scopes)

Los ámbitos limitan el alcance de un rol.

Existen:

* **Directory scopes:** se basan en la estructura organizativa y pueden limitar un rol a grupos, sitios, equipos, ubicaciones, departamentos o cargos específicos.
* **Management scopes:** se basan en el servicio o aplicación y pueden limitar un rol a servicios como Exchange Online, SharePoint Online o Teams, o a condiciones específicas como tipos de buzón, colecciones de sitios o tipos de equipos.

### Asignaciones (Assignments)

Las asignaciones conectan roles y ámbitos con usuarios y grupos y determinan quién puede hacer qué y dónde.

* **Direct assignments:** asignan directamente el rol a un usuario o grupo.
* **Indirect assignments:** asignan permisos mediante membresías o reglas, permitiendo conceder o revocar permisos dinámicamente según cambios en la membresía o regla. Se pueden realizar con roles personalizados y ámbitos de administración.

---

## Tipos y categorías de roles

### Tipos de roles

* **Global roles:** proporcionan permisos de alto nivel en todos los servicios y características de Microsoft 365. Ejemplos: Global Administrator, Global Reader y Power Platform Administrator.
* **Service-specific roles:** permiten administrar un servicio concreto, como Exchange Online, SharePoint Online, Teams o OneDrive.
* **Feature-specific roles:** permiten administrar una característica o función concreta, como seguridad, cumplimiento o administración de dispositivos.

### Categorías de roles

* **Administrator roles:** permiten realizar tareas administrativas como gestionar usuarios, dispositivos, licencias, políticas, configuraciones y reportes.
* **Reader roles:** permiten consultar información y reportes sin realizar modificaciones.
* **Application roles:** proporcionan acceso y uso de determinadas aplicaciones, como Power BI, Power Apps o Power Automate, sin otorgar capacidades administrativas.

---

# Administración de roles en el ecosistema Microsoft 365

El **Microsoft 365 admin center** es el principal lugar para administrar roles integrados y personalizados aplicables a gran parte de la plataforma.

Algunos servicios tienen sus propios roles, administrados desde sus respectivos portales:

* Microsoft Entra ID.
* Microsoft Defender.
* Microsoft Purview.

Estos roles se basan también en permisos y asignaciones, pero su alcance y administración están vinculados al servicio correspondiente.

> **Nota:** Azure Active Directory (Azure AD) ahora se denomina **Microsoft Entra ID**.

El Microsoft 365 admin center permite administrar roles de Microsoft Entra, Exchange e Intune, además de crear **role groups (role-assignable groups)** que contienen uno o más roles. Los usuarios miembros de estos grupos heredan los roles asignados.

### Alcance de los roles

* Los roles de **Microsoft Entra** tienen alcance sobre todo el tenant.
* Los roles de **Exchange, Intune y Purview** son roles de workload.

Las asignaciones se realizan a diferentes identidades:

* Microsoft Entra → usuarios y grupos asignables a roles.
* Exchange → usuarios y grupos habilitados para correo.
* Intune → grupos de seguridad.

Los grupos de roles de Exchange pueden crearse y administrarse desde Exchange Online, pero no pueden asignarse desde el Microsoft 365 admin center. Desde Microsoft 365 se pueden asignar roles de Exchange, pero no grupos de roles de Exchange.

### Diferencia entre roles generales y roles específicos del servicio

Un rol asignado desde el Microsoft 365 admin center puede proporcionar permisos amplios, pero no necesariamente todos los permisos disponibles dentro del portal específico del servicio.

Por ejemplo:

* **Exchange Administrator** permite administrar elementos de Exchange Online, como buzones, grupos y políticas, pero no necesariamente tareas avanzadas como conectores, reglas de transporte y flujo de correo. Para estas tareas se requieren roles más granulares dentro de Exchange admin center.
* **Security Administrator** proporciona permisos amplios sobre servicios de seguridad, pero no concede automáticamente todos los permisos del portal Microsoft Defender. Las tareas avanzadas, como administrar incidentes, investigaciones o roles RBAC personalizados, pueden requerir roles específicos de Defender.

Los roles específicos de servicios también pueden personalizarse para agregar o eliminar permisos y adaptar el acceso al modelo operativo de la organización.

---

# Portales de administración y sus roles

| Servicio o aplicación  | Roles                             | Ubicación                  |
| ---------------------- | --------------------------------- | -------------------------- |
| Microsoft 365          | Roles integrados y personalizados | Microsoft 365 admin center |
| Microsoft Entra ID     | Roles de gobernanza de datos      | Microsoft Entra ID portal  |
| Microsoft Defender XDR | Roles de seguridad                | Microsoft Defender portal  |
| Microsoft Purview      | Roles de catálogo de datos        | Microsoft Purview portal   |

## Microsoft 365 admin center

Permite administrar permisos mediante:

* **Usuarios y grupos:** creación y administración de cuentas y grupos y asignación de roles y permisos.
* **Azure RBAC:** asignación de roles predefinidos como Global Administrator, User Management Administrator, Exchange Administrator y SharePoint Administrator.
* **Permisos específicos de servicios:** administración de permisos de Exchange Online, SharePoint Online, OneDrive y Teams.
* **Permisos de aplicaciones:** administración de permisos e integraciones de aplicaciones y consentimiento para aplicaciones externas que acceden a datos de Microsoft 365.

## Microsoft Entra ID portal

Microsoft Entra ID es una solución de Identity as a Service (IaaS) para administrar identidad y acceso.

Sus roles específicos permiten administrar:

* Identidades.
* Políticas de acceso.
* Gobernanza.

Algunos roles derivan de roles de Microsoft 365, como **Identity Administrator** e **Identity Reader**. Otros son específicos, como **Identity Governance Administrator** y **Entitlement Management Administrator**.

Funciones destacadas:

* **Conditional Access:** políticas de acceso basadas en ubicación, dispositivo y riesgo.
* **Risk-based authentication:** evaluación del riesgo según comportamiento y contexto.
* **Identity insights and monitoring:** visibilidad sobre identidades, inicios de sesión y uso de licencias.
* **Passwordless authentication:** autenticación sin contraseña.
* **Data residency and security:** administración segura de los datos de identidad y acceso en la nube.

## Microsoft Defender portal

Es una consola centralizada para protección, detección, investigación y respuesta frente a amenazas.

Sus roles específicos permiten administrar:

* Incidentes.
* Investigaciones.
* Acciones de seguridad.

Algunos roles derivan de Microsoft 365, como **Security Administrator** y **Security Reader**. Otros son propios del servicio, como **Incident Responder** y **Threat Hunter**.

Funciones destacadas:

* **Threat investigation:** investigación y respuesta ante amenazas.
* **Incident management:** seguimiento, asignación y resolución de incidentes.
* **Advanced hunting:** consultas mediante Kusto Query Language para investigar amenazas e indicadores de compromiso.
* **Threat analytics:** análisis, reportes e información sobre la postura de seguridad.
* **Integración con Microsoft 365:** integración con Defender for Endpoint, Defender for Office 365 y Microsoft Cloud App Security.

## Microsoft Purview portal

Es un centro para administrar requisitos regulatorios y de cumplimiento, riesgos y protección de datos sensibles.

Sus roles son un subconjunto de los roles de Microsoft Entra. Algunos derivan de Microsoft 365, como **Compliance Administrator** y **Compliance Reader**, mientras que otros son específicos, como **Data Source Administrator** y **Data Asset Curator**.

Funciones destacadas:

* **Compliance management:** políticas de cumplimiento.
* **Data protection:** DLP, information barriers, sensitivity labels y gobernanza de datos.
* **Risk assessment and insights:** Compliance Score, análisis y recomendaciones.
* **E-discovery y legal hold:** búsqueda y preservación de información electrónica.
* **Compliance reporting and auditing:** informes y auditorías.
* **Collaboration and training:** colaboración y recursos de capacitación sobre cumplimiento.

---

# Roles administrativos en Microsoft 365

Una suscripción de Microsoft 365 incluye roles administrativos integrados que pueden asignarse desde el Microsoft 365 admin center. Cada rol corresponde a funciones empresariales comunes y proporciona permisos para determinadas tareas.

Microsoft 365 permite administrar roles de Microsoft Entra e Intune, aunque estos representan solo un subconjunto de los roles disponibles directamente en sus respectivos centros de administración.

Los roles administrativos deben asignarse cuidadosamente porque proporcionan acceso a datos y configuraciones sensibles.

Para administrar permisos se requiere ser **Global Administrator** o miembro del grupo de roles **Organization Management**. El rol **Role Management** permite ver, crear y modificar grupos de roles en Microsoft Defender y, de forma predeterminada, está asignado a Organization Management.

Otros servicios tienen modelos de permisos propios:

* **Exchange Online:** utiliza un modelo similar a Azure RBAC y además un modelo basado en permisos individuales para buzones.
* **SharePoint Online:** utiliza grupos de seguridad, permisos y niveles de permisos para recursos como colecciones de sitios, sitios y documentos.

---

# Recomendaciones de seguridad para asignar roles

| Recomendación                              | Motivo                                                                                                                                     |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Mantener entre 2 y 4 Global Administrators | Se necesitan al menos dos para situaciones como bloqueo de cuentas, pero demasiados Global Administrators aumentan el riesgo de seguridad. |
| Asignar el rol menos permisivo             | Cada administrador debe recibir únicamente los permisos necesarios para realizar su trabajo.                                               |
| Requerir MFA para administradores          | Protege las cuentas incluso si la contraseña queda comprometida.                                                                           |

Un usuario puede recibir un mensaje en el admin center indicando que no tiene permisos para modificar una configuración porque sus roles no incluyen ese permiso.

---

# Roles administrativos más utilizados

Los roles pueden consultarse desde **Role assignments** en el Microsoft 365 admin center. La pestaña **Permissions** muestra las tareas permitidas y las pestañas **Assigned** o **Assigned admins** permiten agregar usuarios.

### Billing Administrator

Gestiona:

* Compras.
* Suscripciones.
* Solicitudes de servicio.
* Estado de los servicios.
* Facturación.
* Tickets de soporte en Microsoft Entra admin center.

### Compliance Administrator

Gestiona:

* Cumplimiento normativo.
* Casos de eDiscovery.
* Políticas de gobernanza de datos.
* Políticas de cumplimiento.
* Alertas de cumplimiento.
* Investigaciones legales y de datos.
* Data Subject Requests.
* Datos de auditoría de Intune.

### Exchange Administrator

Administra:

* Buzones.
* Microsoft 365 Groups.
* Exchange Online.
* Flujo de mensajes.
* Elementos eliminados.
* Retención de correo.
* Políticas de uso compartido de buzones.
* Delegados Send As y Send on Behalf.
* Buzones compartidos.
* Filtros antispam y antimalware.
* Microsoft 365 Groups.

Microsoft recomienda asignar también **Service Administrator** a usuarios con Exchange Administrator para que puedan consultar información importante del servicio.

### Global Administrator

Proporciona acceso a prácticamente todas las funciones administrativas de Microsoft Entra ID y servicios que utilizan identidades de Microsoft Entra, incluidos Microsoft 365 Defender, Microsoft Purview, Exchange Online, SharePoint Online y Skype for Business Online.

Puede:

* Restablecer contraseñas de usuarios y administradores.
* Administrar dominios.
* Desbloquear otros Global Administrators.
* Ver logs de actividad de directorio.
* Elevar su acceso para administrar suscripciones y grupos de administración de Azure.

El usuario que registra los servicios online de Microsoft 365 recibe automáticamente este rol.

Un Global Administrator no puede eliminar su propia asignación de Global Administrator, evitando que la organización quede sin administradores globales.

### Global Reader

Permite leer configuraciones e información administrativa sin realizar acciones de administración.

Es la alternativa de solo lectura a Global Administrator y puede utilizarse para:

* Planificación.
* Auditorías.
* Investigaciones.

Puede combinarse con roles administrativos limitados, como Exchange Administrator.

Funciona con Microsoft 365 admin center, Exchange, SharePoint, Teams, Defender, Purview, Azure y Device Management admin centers.

### Groups Administrator

Administra grupos y sus configuraciones:

* Crear, editar, eliminar y restaurar Microsoft 365 Groups.
* Administrar políticas de creación, expiración y nomenclatura.
* Crear, editar y eliminar grupos de seguridad de Microsoft Entra.

El rol permite administrar grupos de toda la organización en workloads como Teams, SharePoint, Yammer y Outlook.

### Helpdesk Administrator

Puede:

* Restablecer contraseñas.
* Forzar el cierre de sesión.
* Invalidar refresh tokens.
* Administrar solicitudes de soporte.
* Supervisar el estado de los servicios.

Puede ayudar a usuarios no administradores y a usuarios con determinados roles limitados.

### License Administrator

Permite:

* Consultar, agregar, eliminar y actualizar asignaciones de licencias.
* Administrar licencias basadas en grupos.
* Administrar la ubicación de uso.
* Reprocesar asignaciones de licencias.
* Asignar licencias de productos a grupos.

No permite comprar o administrar suscripciones ni administrar usuarios o grupos más allá de la ubicación de uso.

### Message Center Reader

Permite:

* Supervisar notificaciones y actualizaciones del Message Center.
* Recibir resúmenes semanales.
* Compartir publicaciones del Message Center.
* Acceder de forma de solo lectura a determinados servicios de Microsoft Entra.

No permite administrar tickets de soporte.

### Office Apps Administrator

Administra:

* Configuración cloud de aplicaciones de Microsoft 365.
* Políticas cloud.
* Descargas de autoservicio.
* Políticas mediante Office Cloud Policy Service.
* Solicitudes de servicio.
* Contenido "What's New".
* Estado de los servicios.

### Password Administrator

Permite restablecer contraseñas de usuarios que no son administradores y de Password Administrators, con capacidades limitadas.

No permite administrar solicitudes de servicio ni supervisar el estado de los servicios.

### Power Platform Administrator

Administra:

* Funciones administrativas de Power Apps.
* Flows.
* Políticas de prevención de pérdida de datos.
* Solicitudes de servicio.
* Estado de los servicios.

### Reports Reader

Permite consultar:

* Datos de uso.
* Dashboards de reportes.
* Reportes de actividad.
* Sign-in logs.
* Audit logs.
* Datos del Microsoft Graph reporting API.
* Power BI adoption content pack.

No proporciona permisos administrativos para configurar servicios ni acceder a centros administrativos específicos de productos.

### Security Administrator

Administra la seguridad general de la organización:

* Políticas de seguridad.
* Analítica y reportes.
* Amenazas y alertas.
* Actividad sospechosa.
* Roles.
* Machine groups.
* Detección y remediación automatizada de amenazas.
* Inventario de dispositivos.
* Información de usuarios, dispositivos, aplicaciones e Intune.
* Configuración de bloqueo por intentos fallidos.
* Listas de contraseñas prohibidas y protección de contraseñas locales.

Tiene permisos relacionados con Microsoft Defender, Microsoft Entra ID Protection, Microsoft Entra Authentication, Azure Information Protection y Microsoft Purview.

### Service Support Administrator

Permite:

* Crear y administrar solicitudes de soporte.
* Consultar el dashboard de servicios.
* Consultar y compartir publicaciones del Message Center.
* Supervisar el estado de los servicios.

Se recomienda como rol adicional para administradores que necesiten estas funciones además de sus responsabilidades principales.

### SharePoint Administrator

Administra SharePoint Online:

* Sitios.
* Colecciones de sitios.
* Configuración global.
* Microsoft 365 Groups.
* Políticas y configuraciones de perfiles de usuario.
* Conexiones BCS.
* Registros.
* Experiencia de búsqueda.
* Configuraciones híbridas.
* InfoPath Forms Services.
* Tickets de soporte.
* Estado de los servicios.

Tiene permisos globales dentro de SharePoint Online cuando el servicio está disponible.

### Teams Administrator

Administra todos los aspectos de Microsoft Teams, incluidos:

* Telefonía.
* Mensajería.
* Reuniones.
* Teams.
* Microsoft 365 Groups.
* Conference bridges.
* Configuración organizativa.
* Federation.
* Actualizaciones de Teams.
* Configuración del cliente.
* Solución de problemas de comunicación.

### User Administrator

Puede:

* Agregar usuarios y grupos.
* Asignar licencias.
* Administrar propiedades de usuarios.
* Crear y administrar vistas.
* Actualizar políticas de expiración de contraseñas.
* Administrar solicitudes de servicio.
* Supervisar el estado de los servicios.
* Administrar nombres de usuario.
* Eliminar y restaurar usuarios.
* Restablecer contraseñas.
* Forzar el cierre de sesión.
* Actualizar claves de dispositivos FIDO.

Puede realizar estas tareas sobre usuarios que no son administradores y sobre determinados roles limitados.

---

# Mejores prácticas al configurar roles administrativos

## 1. Administrar según el principio de mínimo privilegio

El principio de **least privilege** consiste en otorgar exactamente los permisos necesarios para realizar el trabajo.

Al asignar un rol deben considerarse tres aspectos:

* Un conjunto específico de permisos.
* Un ámbito específico.
* Un período de tiempo específico.

Se deben evitar roles demasiado amplios en ámbitos demasiado amplios, ya que limitar roles y scopes reduce los recursos expuestos ante una posible vulneración.

Microsoft Entra RBAC admite más de 65 roles integrados para administrar objetos de directorio y servicios como Exchange, SharePoint e Intune. Si ningún rol integrado satisface las necesidades, se pueden crear roles personalizados.

## 2. Usar Privileged Identity Management para acceso just-in-time

**Microsoft Entra Privileged Identity Management (PIM)** permite otorgar acceso administrativo **just-in-time**.

Un usuario puede ser miembro elegible de un rol y activarlo durante un período limitado cuando lo necesite.

* PIM elimina automáticamente el acceso cuando finaliza el período.
* Puede requerir aprobación.
* Puede enviar notificaciones cuando se activa un rol.
* Puede alertar cuando se agregan usuarios a roles altamente privilegiados.

Aunque Global Administrator y Privileged Role Administrator pueden asignar roles, Microsoft recomienda que **Privileged Role Administrator** gestione las asignaciones mediante PIM para aplicar el principio de mínimo privilegio.

## 3. Activar MFA para todas las cuentas administrativas

Microsoft recomienda utilizar **MFA** para todas las cuentas administrativas.

MFA puede configurarse mediante:

* Configuración de roles en PIM.
* Conditional Access.

Según los estudios mencionados, el uso de MFA reduce en un 99,9 % la probabilidad de que los usuarios sean comprometidos.

## 4. Configurar revisiones periódicas de acceso

Las **Access Reviews** permiten revisar periódicamente el acceso administrativo para garantizar que solo las personas adecuadas mantengan permisos.

Las revisiones son importantes porque:

* Una cuenta puede ser comprometida.
* Los usuarios pueden cambiar de equipo y acumular permisos innecesarios.

## 5. Limitar los Global Administrators a menos de cinco

Microsoft recomienda asignar **Global Administrator a menos de cinco personas** para reducir la superficie de ataque.

Los Global Administrators tienen acceso prácticamente total a las configuraciones administrativas y pueden elevar su acceso para consultar datos.

Todas las cuentas Global Administrator deben estar protegidas mediante MFA.

Microsoft recomienda mantener **dos cuentas "break glass"** asignadas permanentemente a Global Administrator y configurarlas de manera que no dependan del mismo mecanismo de MFA utilizado por las cuentas administrativas normales.

## 6. Usar grupos para asignaciones de roles y delegar la administración

Cuando una organización utiliza sistemas externos de gobernanza basados en grupos, se recomienda asignar roles a **grupos de Microsoft Entra** en lugar de usuarios individuales.

Los grupos asignables a roles pueden administrarse mediante PIM para evitar propietarios o miembros permanentes en grupos privilegiados.

El propietario de un grupo asignable a roles determina quién entra o sale del grupo y, por lo tanto, puede decidir indirectamente quién recibe el rol.

Esto permite que Global Administrator o Privileged Role Administrator deleguen la administración de roles mediante grupos.

## 7. Usar cuentas cloud-native para roles de Microsoft Entra

Se recomienda evitar cuentas sincronizadas desde entornos on-premises para asignaciones de roles de Microsoft Entra.

Si una cuenta on-premises sincronizada se compromete, también podría comprometer los recursos de Microsoft Entra de la organización.

---

# Asignación de roles administrativos en Microsoft 365

Los roles administrativos pueden gestionarse desde:

* **Microsoft 365 admin center**.
* **Windows PowerShell** mediante Microsoft Graph PowerShell.

Los roles administrativos no son mutuamente excluyentes. Un usuario puede recibir varios roles, por ejemplo:

* Exchange Administrator.
* SharePoint Administrator.
* User Management Administrator.

Los roles administrativos se basan en grupos de Microsoft Entra. Aunque estos grupos no aparecen en Microsoft Entra admin center, pueden asignarse desde Microsoft 365 admin center o Windows PowerShell.

## Asignar roles desde Microsoft 365 admin center

Se requiere una cuenta **Global Administrator**.

1. Ir a **Users > Active Users**.
2. Seleccionar el usuario.
3. En **Roles**, seleccionar **Edit**.
4. Elegir:

   * **User:** sin acceso administrativo.
   * **Global administrator**.
   * **Customized administrator:** permite seleccionar roles administrativos.
5. Utilizar **Alternative email address** para notificaciones importantes, incluido el restablecimiento de la contraseña administrativa.
6. Seleccionar **Save**.

---

# Asignar roles mediante Windows PowerShell

Los administradores pueden utilizar el módulo **Microsoft Graph PowerShell**.

Para asignar un rol se necesita:

* Object ID del usuario.
* Object ID del rol de directorio.

Para obtener los usuarios:

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
Import-Module Microsoft.Graph.Identity.DirectoryManagement
Connect-MgGraph -Scopes 'User.Read.All', 'RoleManagement.ReadWrite.Directory'
Get-MgUser -All | Format-List ID, DisplayName, Mail, UserPrincipalName
```

Para consultar los roles activados:

```powershell
Get-MgDirectoryRole | Format-List
```

Microsoft Graph PowerShell solo muestra los roles administrativos **activados**.

Un rol se activa cuando:

* Se activa manualmente, incluso sin usuarios asignados.
* Se asigna uno o más usuarios activos al rol.

Si un rol no aparece en `Get-MgDirectoryRole`, primero debe activarse.

## Asignar un rol activado a un usuario

Una vez obtenidos los Object ID del usuario y del rol:

```powershell
$UserObjectId = @{ "@odata.id" = "https://graph.microsoft.com/v1.0/directoryObjects/e4e2b110-8d4f-434f-a990-7cd63e23aed6" }

New-MgDirectoryRoleMemberByRef -DirectoryRoleId 'a2d10e79-df32-47fc-86ef-64d199860810' -BodyParameter $UserObjectId
```

## Activar un rol mediante su template

Si el rol no está activado, primero se obtiene su template mediante:

```powershell
Get-MgDirectoryRoleTemplate -All | Format-List ID, DisplayName
```

Por ejemplo, el template de **Helpdesk Administrator**:

```text
Id          : 95e79109-95c0-4d8e-aee3-d01accf2d47b
DisplayName : Helpdesk Administrator
```

Se activa con:

```powershell
New-MgDirectoryRole -roleTemplateId '95e79109-95c0-4d8e-aee3-d01accf2d47b'
```

Después se verifica:

```powershell
Get-MgDirectoryRole | Format-List
```

Una vez activado, se puede asignar a un usuario:

```powershell
$UserObjectId = @{ "@odata.id" = "https://graph.microsoft.com/v1.0/directoryObjects/dba12422-ac75-486a-a960-cd7cb3f6963f" }

New-MgDirectoryRoleMemberByRef -DirectoryRoleId '227ec638-37b9-4eb7-a661-2773dcce2b36' -BodyParameter $UserObjectId
```

En este ejemplo:

* El Object ID de Adele Vance identifica al usuario.
* El Object ID `227ec638-37b9-4eb7-a661-2773dcce2b36` identifica el rol Helpdesk Administrator.
* El rol debe estar activado antes de poder asignarlo.

---

# Conceptos fundamentales

* **Roles:** definen qué acciones puede realizar un usuario o grupo.
* **Scopes:** limitan dónde puede aplicarse un rol.
* **Assignments:** vinculan roles y scopes con usuarios o grupos.
* **Role groups:** permiten asignar roles mediante grupos y hacer que sus miembros hereden los permisos.
* **Microsoft 365 admin center:** administra los roles generales y algunos roles de servicios.
* **Portales específicos:** Microsoft Entra, Defender y Purview mantienen roles propios y más granulares.
* **Least privilege:** asignar únicamente los permisos necesarios, sobre el alcance necesario y durante el tiempo necesario.
* **PIM:** proporciona acceso administrativo just-in-time.
* **MFA:** debe utilizarse para proteger las cuentas administrativas.
* **Access Reviews:** permiten retirar permisos que ya no son necesarios.
* **Global Administrator:** debe limitarse a menos de cinco personas.
* **Grupos asignables a roles:** permiten delegar y centralizar la administración de asignaciones.
* **Cuentas cloud-native:** se recomiendan para roles de Microsoft Entra en lugar de cuentas sincronizadas desde entornos on-premises.

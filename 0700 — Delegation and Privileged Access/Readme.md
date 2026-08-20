# Resumen — Microsoft 365

## Delegar roles de administración a partners

Una organización que no cuenta con administradores internos puede externalizar la administración de Microsoft 365 a un partner de Microsoft. Esta modalidad se denomina **administración delegada**.

### Administración delegada

El partner inicia el proceso enviando un correo a la organización para solicitar permiso para actuar como administrador en su nombre.

Para aceptar la oferta:

1. Abrir el correo del partner y revisar los términos.
2. Seleccionar el enlace para autorizar el acuerdo.
3. En **Delegated administration**, seleccionar **Yes** para autorizar al partner como administrador delegado.
4. Si la oferta incluye una suscripción de prueba o de compra, crear la cuenta del tenant correspondiente.

Para consultar los administradores delegados:

1. En el **Centro de administración de Microsoft 365**, acceder a **Active users**.
2. Seleccionar **Filter**.
3. En la lista desplegable, seleccionar cualquiera de los roles asignados.

Si no existe ningún administrador delegado, se muestra el mensaje: **“There are no delegated administrators associated with your account.”**

### Roles de administración establecidos por partners

Al delegar la administración, el partner puede asignar roles a usuarios que cree en nombre de la organización, tanto a agentes de soporte de su propia organización como a usuarios del cliente.

Los dos roles disponibles son:

#### Full Administration

Proporciona amplios privilegios administrativos sobre la organización delegada:

* Administrar usuarios, cuentas, licencias, dominios y servicios.
* Crear y administrar usuarios, incluyendo la asignación de roles y permisos.
* Administrar configuraciones de seguridad, como políticas de contraseñas.
* Administrar suscripciones de Microsoft 365, incluyendo compra y asignación de licencias.
* Administrar configuraciones de Exchange Online, correo y buzones.
* Acceder a los datos de la organización.
* Administrar sitios y archivos de SharePoint Online.

#### Limited Administration

Proporciona privilegios administrativos restringidos:

* Crear y modificar cuentas de usuario.
* Restablecer contraseñas.
* Administrar membresías de grupos.
* Consultar información de estado del servicio y soporte.
* Ver y administrar tickets de soporte relacionados con Microsoft 365.
* No permite administrar configuraciones sensibles como dominios, suscripciones o seguridad.

### Buenas prácticas para la administración delegada

Las organizaciones deben evaluar cuidadosamente el nivel de confianza y acceso concedido al partner, definir claramente los roles y responsabilidades y verificar que se ajusten a sus requisitos de seguridad y cumplimiento.

Microsoft recomienda:

* Planificar los roles administrativos mediante una matriz que los distribuya según el modelo operativo de la organización.
* Documentar y auditar los roles administrativos y sus privilegios.
* Mantener los roles actualizados, modificándolos o eliminándolos cuando sea necesario.
* Obtener aprobación de la dirección para el diseño final de los roles administrativos.

Las capacidades y permisos de estos roles pueden cambiar con el tiempo, por lo que se recomienda consultar la documentación oficial de Microsoft o al partner de Microsoft 365 para obtener información actualizada.

---

## Implementar grupos de roles en Microsoft 365

Los **grupos de roles** permiten asignar roles a un grupo en lugar de asignarlos directamente a usuarios individuales. Simplifican la administración de roles, mantienen permisos consistentes y facilitan la auditoría.

Un grupo de roles puede incluir roles integrados de Microsoft 365 y roles personalizados de la organización.

### Ventajas de los grupos de roles

* **Simplifican la asignación de roles:** se administra un único grupo en lugar de múltiples asignaciones individuales y se mantiene un conjunto consistente de permisos.
* **Mejoran la seguridad y el cumplimiento:** facilitan el principio de mínimo privilegio y la separación de funciones.
* **Aumentan la productividad y colaboración:** permiten agrupar usuarios según sus roles y responsabilidades y proporcionarles los permisos necesarios.
* **Facilitan la administración:** agregar o quitar usuarios del grupo permite asignar o retirar indirectamente los roles correspondientes.

También permiten crear grupos de roles personalizados adaptados a las necesidades específicas de la organización.

### Buenas prácticas

* **Usar grupos de roles integrados:** Microsoft proporciona grupos predefinidos para escenarios habituales, como **Helpdesk Administrator**, **Service Support Administrator** y **Reports Reader**.
* **Crear grupos personalizados:** utilizarlos cuando los grupos integrados no cubran las necesidades de la organización, aplicando mínimo privilegio y separación de funciones.
* **Revisar y actualizar los grupos:** ajustar roles y miembros cuando cambien los requisitos, servicios, responsabilidades o integrantes de la organización.

### Crear grupos de roles personalizados

Para asignar un rol a un grupo, se debe crear un grupo de seguridad o Microsoft 365 que sea **role-assignable**. Su propiedad `isAssignableToRole` debe estar establecida en `true`.

#### Microsoft 365 admin center

1. Al crear un grupo de seguridad, seleccionar **Azure AD roles can be assigned to the group**.
2. Al crear un grupo de Microsoft 365, establecer **Privacy** en **Private** y seleccionar **Allow admin roles to be assigned to this group**.
3. Después de crear el grupo, abrirlo nuevamente y asignarle los roles.
4. Agregar los usuarios como miembros del grupo.

#### Microsoft Entra admin center

1. Al crear un grupo de seguridad o Microsoft 365, establecer **Microsoft Entra roles can be assigned to the group** en **Yes**.
2. Durante la creación se pueden asignar uno o más roles de Microsoft Entra directamente al grupo.
3. Agregar los usuarios como miembros del grupo.

#### Windows PowerShell / Microsoft Graph PowerShell

1. Crear el grupo con `New-MgGroup` y establecer `-IsAssignableToRole:$true`.
2. Obtener la definición del rol con `Get-MgRoleManagementDirectoryRoleDefinition`.
3. Asignar el rol al grupo mediante `New-MgRoleManagementDirectoryRoleAssignment`.

Ejemplo:

```powershell
Connect-MgGraph -Scopes "Group.ReadWrite.All"

$group = New-MgGroup -DisplayName "Contoso_Helpdesk_Administrators" -Description "Helpdesk Administrator role assigned to group" -MailEnabled:$false -SecurityEnabled -MailNickName "contosohelpdeskadministrators" -IsAssignableToRole:$true

$roleDefinition = Get-MgRoleManagementDirectoryRoleDefinition -Filter "displayName eq 'Helpdesk Administrator'"

$roleAssignment = New-MgRoleManagementDirectoryRoleAssignment -DirectoryScopeId '/' -RoleDefinitionId $roleDefinition.Id -PrincipalId $group.Id
```

### Protección de los grupos de roles

Un administrador que pueda modificar la membresía de un grupo con roles podría agregarse a sí mismo y obtener privilegios adicionales. Por ello, los grupos de roles tienen mecanismos y restricciones específicas.

La membresía de un grupo de roles es de tipo **Assigned**, por lo que solo administradores autorizados, como los **Global Administrators**, pueden administrarla. Esto evita que administradores no autorizados eleven sus privilegios agregándose al grupo.

#### Restricciones

* `isAssignableToRole` es inmutable: no puede modificarse después de crear el grupo.
* Un grupo existente no puede convertirse posteriormente en grupo de roles.
* Se pueden crear como máximo **500 grupos de roles** por organización de Microsoft Entra.
* Solo **Global Administrators** y **Privileged Role Administrators** pueden crear grupos de roles, aunque la administración puede delegarse mediante propietarios del grupo.
* La membresía debe ser **Assigned**; no se admiten grupos dinámicos de Microsoft Entra.
* Para administrar la membresía mediante Microsoft Graph se requiere el permiso `RoleManagement.ReadWrite.Directory`; `Group.ReadWrite.All` no es suficiente.
* Solo un **Privileged Authentication Administrator** o **Global Administrator** puede cambiar credenciales, restablecer MFA o modificar atributos sensibles de miembros y propietarios de un grupo de roles.
* No se admite el anidamiento de grupos.

### Usar PIM para hacer elegible un grupo para una asignación de roles

Si se quiere evitar que los miembros tengan acceso permanente a un rol, se puede utilizar **Microsoft Entra Privileged Identity Management (PIM)** para hacer que el grupo sea elegible para una asignación.

Cada miembro puede activar la asignación del rol durante un período de tiempo determinado.

Para grupos utilizados para elevar privilegios en roles de Microsoft Entra, Microsoft recomienda exigir un proceso de aprobación para las asignaciones de miembros elegibles. Las asignaciones activables sin aprobación pueden representar un riesgo de seguridad para administradores con menos privilegios.

### Requisitos de licencia

* Para utilizar grupos de roles se requiere **Microsoft Entra ID P1**.
* Para utilizar **Privileged Identity Management (PIM)** para activación de roles just-in-time se requiere **Microsoft Entra ID P2**.

---

## Administrar permisos mediante unidades administrativas en Microsoft Entra ID

Una **unidad administrativa (Administrative Unit)** es un recurso de Microsoft Entra que funciona como contenedor para **usuarios, grupos o dispositivos**.

Permite limitar el alcance de los permisos de un rol a una parte específica de la organización. Por ejemplo, se puede delegar el rol **Helpdesk Administrator** a especialistas regionales para que administren únicamente los usuarios de su región.

Un usuario puede pertenecer a varias unidades administrativas, por ejemplo, una basada en **geografía** y otra en **división**.

### Escenario de implementación

Las unidades administrativas son útiles para organizaciones con divisiones independientes. Por ejemplo, una universidad puede:

1. Crear una unidad administrativa para la **School of Business**.
2. Agregar únicamente sus estudiantes y personal.
3. Crear un rol con permisos administrativos limitados a los usuarios de esa unidad.
4. Asignar el equipo de TI de la escuela al rol con ese alcance.

### Requisitos de licencia

* Cada administrador de una unidad administrativa requiere **Microsoft Entra Premium P1**.
* Cada miembro de una unidad administrativa requiere **Microsoft Entra Free**.
* Si se utilizan reglas de membresía dinámica, cada miembro requiere **Microsoft Entra Premium P1**.

### Administración de unidades administrativas

Se pueden administrar mediante:

* **Microsoft Entra admin center**.
* **PowerShell**.
* **Microsoft Graph API**.

Pueden utilizarse para representar estructuras como:

* Límites geográficos de una organización.
* Suborganizaciones semiautónomas.
* Divisiones organizativas.

La estructura debe definirse según las necesidades de la organización y considerando cómo se utilizarán las unidades administrativas en los distintos servicios de Microsoft 365.

### Ciclo de adopción

1. **Adopción inicial:** se crean unidades según los criterios iniciales y su número puede aumentar mientras se refinan esos criterios.
2. **Poda (Pruning):** se eliminan las unidades que ya no son necesarias.
3. **Estabilización:** una vez definida la estructura organizativa, el número de unidades no cambia significativamente a corto plazo.

### Escenarios actualmente compatibles

Como **Global Administrator** o **Privileged Role Administrator**, se puede:

* Crear unidades administrativas.
* Agregar usuarios, grupos o dispositivos.
* Administrar usuarios o dispositivos mediante reglas de membresía dinámica.
* Asignar personal de TI a roles con alcance sobre unidades administrativas.

Los administradores con alcance de unidad administrativa pueden utilizar el **Centro de administración de Microsoft 365** para la administración básica de usuarios dentro de sus unidades. Los administradores de grupos con este alcance pueden administrar grupos mediante PowerShell, Microsoft Graph y los centros de administración de Microsoft 365.

Las unidades administrativas limitan únicamente los **permisos de administración**. No impiden que usuarios o administradores utilicen sus permisos predeterminados para consultar otros usuarios, grupos o recursos fuera de la unidad. El Centro de administración de Microsoft 365 puede filtrar los usuarios que aparecen para un administrador con alcance, pero este puede consultar otros usuarios desde Microsoft Entra admin center, PowerShell y otros servicios de Microsoft.

No están disponibles funciones a nivel de organización para un rol de Microsoft Entra con alcance de unidad administrativa; solo se admiten las funcionalidades indicadas.

### Administración de unidades administrativas

| Operación                                                                        | Microsoft Graph / PowerShell | Microsoft Entra admin center | Microsoft 365 admin center |
| -------------------------------------------------------------------------------- | :--------------------------: | :--------------------------: | :------------------------: |
| Crear o eliminar unidades administrativas                                        |               ✓              |               ✓              |                            |
| Agregar o quitar miembros individualmente                                        |               ✓              |               ✓              |                            |
| Agregar o quitar miembros mediante archivos CSV                                  |                              |               ✓              |         No previsto        |
| Asignar administradores con alcance de unidad administrativa                     |               ✓              |               ✓              |                            |
| Agregar o quitar usuarios o dispositivos dinámicamente mediante reglas (Preview) |               ✓              |               ✓              |                            |
| Agregar o quitar grupos dinámicamente mediante reglas                            |                              |                              |                            |

### Administración de usuarios

| Operación                                                                               | Microsoft Graph / PowerShell | Microsoft Entra admin center | Microsoft 365 admin center |
| --------------------------------------------------------------------------------------- | :--------------------------: | :--------------------------: | :------------------------: |
| Administrar propiedades y contraseñas de usuarios con alcance de unidad                 |               ✓              |               ✓              |              ✓             |
| Administrar licencias de usuarios con alcance de unidad                                 |               ✓              |                              |              ✓             |
| Bloquear o desbloquear inicios de sesión de usuarios con alcance de unidad              |               ✓              |               ✓              |              ✓             |
| Administrar credenciales de autenticación multifactor de usuarios con alcance de unidad |               ✓              |               ✓              |                            |

### Administración de grupos

| Operación                                                           | Microsoft Graph / PowerShell | Microsoft Entra admin center | Microsoft 365 admin center |
| ------------------------------------------------------------------- | :--------------------------: | :--------------------------: | :------------------------: |
| Administrar propiedades y membresía de grupos con alcance de unidad |               ✓              |               ✓              |                            |
| Administrar licencias de grupos con alcance de unidad               |               ✓              |               ✓              |                            |

Agregar un grupo a una unidad administrativa incluye **el grupo**, pero no a sus miembros individuales dentro del alcance. Un administrador puede administrar propiedades y membresía del grupo, pero no las propiedades de los usuarios o dispositivos que pertenecen al grupo.

Para administrar, por ejemplo, los métodos de autenticación de esos usuarios, es necesario agregar directamente los usuarios a la unidad administrativa y asignar un rol que permita administrar sus métodos de autenticación.

### Administración de dispositivos

| Operación                                       | Microsoft Graph / PowerShell | Microsoft Entra admin center | Microsoft 365 admin center |
| ----------------------------------------------- | :--------------------------: | :--------------------------: | :------------------------: |
| Habilitar, deshabilitar o eliminar dispositivos |               ✓              |               ✓              |                            |
| Leer claves de recuperación de BitLocker        |               ✓              |               ✓              |                            |

### Administración de permisos

Se pueden crear **roles personalizados** y limitar su alcance a una unidad administrativa específica para otorgar permisos determinados a usuarios o grupos dentro de esa unidad.

No se puede crear un rol con alcance global para **todas las unidades administrativas** de la organización. Cada unidad tiene su propio conjunto de roles y permisos.

Como alternativa, se puede crear un rol personalizado con permisos aplicables a varias unidades administrativas y asignarlo individualmente a usuarios o grupos dentro de cada una de ellas.

Agregar un grupo a una unidad administrativa afecta al **grupo en sí**, no a sus miembros. Esto se debe al modelo **RBAC (Role-Based Access Control)** de Microsoft Entra ID, que concede acceso a recursos según el rol y los permisos asociados.

### Restricciones

* Las unidades administrativas **no pueden anidarse**.
* Los administradores de cuentas de usuario con alcance de unidad administrativa no pueden crear ni eliminar usuarios.
* Una asignación de rol con alcance no se aplica a los miembros de un grupo agregado a una unidad administrativa, salvo que esos miembros se agreguen directamente a la unidad.
* Actualmente, las unidades administrativas no están incluidas en **Microsoft Entra Identity Governance**.

---

## Administrar permisos de SharePoint para evitar el uso compartido excesivo de datos

El **oversharing** ocurre cuando contenido de SharePoint queda accesible para una audiencia más amplia de la prevista. Puede producirse porque:

* Los usuarios guardan archivos críticos en ubicaciones accesibles para demasiadas personas, incluidos usuarios externos.
* Comparten con grupos grandes en lugar de personas específicas.
* No revisan cuidadosamente los permisos al cargar archivos.

Microsoft SharePoint y Microsoft Copilot para Microsoft 365 utilizan los datos a los que cada usuario tiene **al menos permisos de View**. Por ello, contenido compartido ampliamente puede aparecer para usuarios que desconocen que tienen acceso. El oversharing puede provocar la exposición de información sensible a destinatarios no previstos.

Los administradores deben utilizar el modelo de permisos de SharePoint para garantizar que los usuarios y grupos tengan acceso únicamente al contenido correspondiente.

> Algunas de las funcionalidades descritas requieren una licencia de **SharePoint Advanced Management**.

### Paso 1: Revisar los controles de uso compartido y eliminar "Everyone Except External Users"

Los administradores deben promover el uso cuidadoso de permisos a nivel de **sitio, biblioteca y carpeta**, y educar a los usuarios sobre los riesgos del oversharing.

El **People Picker** permite buscar y seleccionar usuarios, grupos y claims al asignar permisos. Una de sus opciones es **Everyone Except External Users**, que permite compartir contenido ampliamente dentro de la organización.

Esta opción incluye usuarios internos y excluye colaboradores externos. Sin embargo, puede provocar oversharing al compartir accidentalmente información sensible con una audiencia interna demasiado amplia.

Se recomienda revisar los controles de uso compartido a nivel de sitio y deshabilitar esta opción. Los usuarios pueden seguir compartiendo con personas o grupos específicos.

Además:

* Educar a los administradores de sitios sobre los controles disponibles para restringir el uso compartido.
* Configurar que los **Site Owners** sean los destinatarios de las solicitudes de acceso.
* Considerar ocultar los permisos de alcance amplio del People Picker para evitar su uso accidental.
* Considerar cambiar los valores predeterminados de los vínculos de uso compartido de toda la organización a vínculos para **personas específicas**.

### Paso 2: Identificar sitios inactivos y restringirlos o eliminarlos

Se deben identificar sitios de SharePoint que hayan permanecido inactivos durante mucho tiempo para reducir la superficie de contenido potencialmente compartido de forma excesiva.

Se pueden utilizar las **Inactive Site Policies** de SharePoint Advanced Management y posteriormente:

* Restringir los permisos mediante **Restricted Access Control**.
* Eliminar los sitios cuando corresponda.

### Paso 3: Identificar contenido potencialmente compartido en exceso

Los administradores de SharePoint pueden utilizar informes del Centro de administración de SharePoint para detectar actividades de uso compartido amplio.

Los informes de **Data Access Governance** de SharePoint Advanced Management permiten analizar, durante los últimos 28 días:

* Uso de **Everyone Except External Users**.
* Uso de vínculos **People in your organization**.
* Uso de vínculos **Anyone**.

Los informes pueden descargarse como archivos CSV. También se pueden crear informes personalizados mediante **Microsoft Graph Data Connect for SharePoint**.

### Paso 4: Aplicar acciones de corrección

Las acciones deben considerar la sensibilidad de los datos, la gravedad del oversharing y la necesidad de mantener las operaciones del negocio.

#### Contenido que requiere acción inmediata

* Configurar una **Restricted Access Control Policy** para el sitio. El acceso existente queda restringido al grupo de usuarios configurado por el administrador y el contenido solo será visible para ese grupo.
* La política funciona tanto para **OneDrive** como para **SharePoint**.
* Para casos importantes, utilizar **Change History** para determinar quién, cómo y cuándo realizó los cambios que provocaron el oversharing.

#### Casos que requieren intervención de los propietarios del sitio

* Contactar a los propietarios de los sitios identificados mediante los informes de Data Access Governance.
* Informarles sobre los archivos o carpetas compartidos excesivamente.
* Solicitar que eliminen manualmente los accesos innecesarios.
* Utilizar **Site Access Review** para que los propietarios revisen el contenido ampliamente compartido, eliminen permisos excesivos o proporcionen una justificación empresarial al administrador de SharePoint.

### Paso 5: Proteger sitios críticos para el negocio

Los administradores de SharePoint deben utilizar **Restricted Access Control** de forma preventiva en sitios críticos.

También pueden:

* Aplicar una **block download policy** para impedir descargas desde sitios seleccionados.
* Bloquear específicamente la descarga de **grabaciones de reuniones de Teams**.
* Aplicar cifrado con **extract rights** para documentos de Office críticos para el negocio.

---

## Elevar privilegios mediante Microsoft Entra Privileged Identity Management

**Microsoft Entra Privileged Identity Management (PIM)** permite administrar, controlar y supervisar el acceso de los usuarios a recursos de Microsoft Entra ID, Azure y otros servicios de Microsoft, como Microsoft 365 e Intune.

### Beneficios de PIM

* Identifica usuarios con roles privilegiados o administrativos.
* Permite acceso administrativo **Just-in-Time (JIT)** bajo demanda a:

  * Microsoft 365 e Intune.
  * Recursos de Azure.
  * Grupos de recursos.
  * Recursos individuales, como máquinas virtuales.
* Mantiene un historial de activaciones administrativas y cambios realizados en recursos de Azure.
* Genera alertas ante cambios en asignaciones administrativas.
* Puede requerir aprobación para activar roles administrativos privilegiados.
* Permite revisar la pertenencia a roles administrativos y exigir una justificación para mantenerla.

### Acceso administrativo Just-in-Time

Tradicionalmente, un administrador asigna permanentemente un usuario a un rol administrativo mediante el Centro de administración de Microsoft Entra, otros portales de Microsoft o PowerShell.

PIM introduce el concepto de **administrador elegible (eligible administrator)**:

* El usuario es elegible para un rol, pero no tiene el rol activo permanentemente.
* Cuando necesita realizar una tarea administrativa, debe activar el rol.
* La activación es temporal y dura un período predeterminado.
* Este modelo reduce o elimina el **standing admin access**, es decir, el acceso administrativo permanente.

### Privileged Role Administrator (PRA)

El **Privileged Role Administrator** administra PIM y las asignaciones de roles privilegiados.

Sus principales responsabilidades son:

* **Administrar roles privilegiados:** definir qué roles requieren privilegios elevados y asignarlos según las necesidades del negocio y el principio de mínimo privilegio.
* **Gestionar acceso JIT:** configurar políticas para el acceso temporal y revisar, aprobar o rechazar solicitudes.
* **Supervisar y auditar:** revisar registros e informes para detectar actividades no autorizadas o sospechosas y tomar medidas cuando sea necesario.
* **Seguridad y cumplimiento:** alinear el acceso privilegiado con las políticas de seguridad y cumplimiento.
* **Documentación y capacitación:** establecer pautas y materiales sobre la administración y el uso seguro de cuentas privilegiadas.

El PRA determina qué usuarios necesitan privilegios elevados y les asigna los roles correspondientes mediante PIM.

PIM proporciona roles integrados para tareas habituales, como **Global Administrator**, **Exchange Administrator** y **SharePoint Administrator**, además de permitir roles personalizados.

Desde PIM, el PRA puede:

* Revisar solicitudes de acceso.
* Aprobar o rechazar solicitudes según las políticas.
* Definir la duración de los privilegios elevados.

El objetivo es aplicar el **principio de mínimo privilegio**, concediendo acceso elevado solo cuando sea necesario y durante el tiempo requerido.

### Solicitar activación de un rol

Si un usuario es **elegible** para un rol administrativo, debe activarlo cuando necesite realizar acciones privilegiadas.

Por ejemplo, en lugar de asignar permanentemente **Global Administrator**, se puede hacer elegible al usuario para un rol como **Exchange Online Administrator**, que podrá activar cuando sea necesario.

Durante la activación, PIM agrega temporalmente una asignación activa al rol. Al desactivarse manualmente o finalizar el período de activación, PIM elimina esa asignación activa.

La propagación del cambio puede depender de la arquitectura y caché de cada aplicación.

### Proceso de activación

1. Iniciar sesión en **Microsoft Entra admin center**.
2. Acceder a **Privileged Identity Management** desde **Identity governance**.
3. En **Tasks**, seleccionar **My roles**.
4. En **Eligible assignments**, localizar el rol que se desea activar.
5. Seleccionar **Activate**.
6. Realizar la verificación de seguridad adicional.
7. Completar la autenticación multifactor y seleccionar **Activate**.
8. Opcionalmente, especificar un **Scope** reducido para limitar los recursos a los estrictamente necesarios.
9. Opcionalmente, establecer una hora de inicio personalizada.
10. Indicar el motivo de la activación en **Reason**.
11. Seleccionar **Activate**.
12. Si el rol requiere aprobación, la solicitud queda pendiente hasta su aprobación.

La recomendación es solicitar el **menor alcance de recursos necesario** y utilizar la activación temporal para reducir la exposición de privilegios elevados.

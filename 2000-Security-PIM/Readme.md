# Microsoft Entra Privileged Identity Management (PIM)

## Introducción

Microsoft Entra Privileged Identity Management (PIM) es una solución en la nube para controlar y monitorear el acceso y los permisos de empleados y administradores. Permite aplicar el principio de mínimo privilegio y reducir la cantidad de personas con acceso a información o recursos seguros en Microsoft 365, Microsoft Entra ID, Azure y Microsoft Intune.

PIM ayuda a:

* Asignar roles y permisos de forma temporal y just-in-time (JIT).
* Revisar y auditar actividades y solicitudes de usuarios privilegiados.
* Aplicar políticas y buenas prácticas para administrar el acceso privilegiado.
* Integrarse con otros servicios y aplicaciones de Microsoft Entra.
* Reducir riesgos de seguridad, cumplir requisitos regulatorios y mejorar la eficiencia operativa.

El proceso de asignación de roles de PIM incluye:

1. Configurar los ajustes de los roles.
2. Asignar roles a usuarios.
3. Activar las asignaciones.
4. Aprobar o rechazar solicitudes.
5. Extender y renovar asignaciones.

PIM mantiene un registro de auditoría de actividades y solicitudes privilegiadas, como activaciones, aprobaciones y cambios de configuración. Este registro permite revisar acciones, detectar actividades sospechosas o no autorizadas y generar información para cumplimiento. Puede consultarse desde el centro de administración de Microsoft Entra o exportarse para análisis.

## Explorar Privileged Identity Management

PIM permite administrar, controlar y monitorear el acceso a recursos importantes de Microsoft Entra ID, Azure, Microsoft 365 y Microsoft Intune.

### ¿Por qué utilizar PIM?

PIM permite reducir el riesgo de:

* Acceso por parte de actores maliciosos.
* Impactos accidentales de usuarios autorizados sobre recursos sensibles.
* Permisos excesivos, innecesarios o mal utilizados.

Sus principales capacidades incluyen:

* Acceso privilegiado just-in-time a Microsoft Entra ID y Azure.
* Acceso limitado mediante fechas de inicio y finalización.
* Aprobación para activar roles privilegiados.
* MFA para activar roles.
* Justificación para conocer el motivo de una activación.
* Notificaciones cuando se activan roles privilegiados.
* Access reviews para verificar que los usuarios continúan necesitando los roles.
* Descarga del historial de auditoría.
* Prevención de la eliminación de las últimas asignaciones activas de Global Administrator y Privileged Role Administrator.

Históricamente, la asignación de un rol administrativo convertía al usuario en administrador permanente y siempre activo. PIM introduce el concepto de **administrador elegible (eligible admin)**: el usuario tiene el rol disponible, pero este permanece inactivo hasta que necesita utilizarlo. Entonces debe realizar un proceso de activación y obtiene el rol activo durante un período determinado.

Este enfoque **just-in-time** permite reducir o eliminar el acceso administrativo permanente (*standing admin access*).

## Implementación de PIM

El flujo general es:

1. La organización decide qué roles proteger con PIM.
2. Asigna usuarios elegibles a esos roles.
3. Cuando un usuario elegible necesita el rol, lo activa.
4. Según la configuración, puede necesitar:

   * MFA.
   * Aprobación.
   * Justificación empresarial.
5. Al activarse, obtiene el rol durante un período preconfigurado.
6. Los administradores pueden revisar las actividades en el registro de auditoría y utilizar funciones como access reviews y alertas.

Para utilizar PIM se necesita una licencia **Microsoft Entra Premium P2** o **Enterprise Mobility + Security (EMS) E5**.

### Escenarios y permisos

**Privileged Role Administrator:**

* Habilitar aprobación para roles específicos.
* Definir usuarios o grupos aprobadores.
* Consultar el historial de solicitudes y aprobaciones.

**Aprobadores:**

* Consultar solicitudes pendientes.
* Aprobar o rechazar solicitudes de elevación.
* Proporcionar justificación para la aprobación o rechazo.

**Usuarios con roles elegibles:**

* Solicitar la activación de un rol que requiere aprobación.
* Consultar el estado de la solicitud.
* Utilizar el rol una vez aprobada la activación.

## Roles administrados por PIM

PIM puede administrar:

* **Roles de Microsoft Entra:** roles integrados y personalizados para administrar Microsoft Entra ID y otros servicios online de Microsoft 365.
* **Roles de Azure:** roles RBAC que proporcionan acceso a grupos de administración, suscripciones, grupos de recursos y recursos.
* **PIM for Groups:** acceso just-in-time a los roles de miembro y propietario de grupos de seguridad de Microsoft Entra.

Los roles o grupos pueden asignarse a:

* **Usuarios:** acceso JIT a roles de Microsoft Entra, roles de Azure y PIM for Groups.
* **Grupos:** sus integrantes pueden obtener acceso JIT a roles de Microsoft Entra y Azure.

  * Para roles de Microsoft Entra, el grupo debe ser un nuevo grupo cloud marcado como asignable a un rol.
  * Para roles de Azure, puede utilizarse cualquier grupo de seguridad de Microsoft Entra.

Microsoft no recomienda asignar o anidar un grupo a un **PIM for Groups**.

### Administración de asignaciones

Para roles de Microsoft Entra, únicamente usuarios con **Privileged Role Administrator** o **Global Administrator** pueden administrar asignaciones de otros administradores. Global Administrators, Security Administrators, Global Readers y Security Readers también pueden visualizar las asignaciones.

Para roles de recursos de Azure, las asignaciones pueden ser administradas por un administrador de la suscripción, un **Owner** del recurso o un **User Access Administrator**. Privileged Role Administrators, Security Administrators y Security Readers no tienen acceso predeterminado para visualizar las asignaciones de roles de recursos de Azure en PIM.

## Terminología

| Concepto                           | Descripción                                                                                                                              |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Eligible**                       | Asignación que requiere que el usuario realice acciones para utilizar el rol.                                                            |
| **Active**                         | Asignación que permite utilizar el rol sin realizar acciones adicionales.                                                                |
| **Activate**                       | Proceso mediante el cual un usuario elegible realiza las acciones necesarias para utilizar el rol, como MFA, justificación o aprobación. |
| **Assigned**                       | Usuario que tiene una asignación activa.                                                                                                 |
| **Activated**                      | Usuario con una asignación elegible que realizó la activación y ahora tiene el rol activo durante un período preconfigurado.             |
| **Permanent eligible**             | Usuario que siempre puede activar el rol.                                                                                                |
| **Permanent active**               | Usuario que puede utilizar permanentemente el rol sin realizar acciones.                                                                 |
| **Time-bound eligible**            | Usuario elegible únicamente dentro de fechas de inicio y finalización determinadas.                                                      |
| **Time-bound active**              | Usuario que puede utilizar el rol únicamente dentro de fechas determinadas.                                                              |
| **Just-in-time (JIT) access**      | Modelo en el que los usuarios reciben permisos temporales únicamente cuando necesitan realizar tareas privilegiadas.                     |
| **Principio de mínimo privilegio** | Práctica que proporciona a cada usuario únicamente los privilegios mínimos necesarios para sus tareas autorizadas.                       |

### Tipos de asignaciones

Existen dos tipos principales:

* **Eligible:** requiere una acción del usuario para utilizar el rol.
* **Active:** permite utilizar directamente los privilegios asignados.

Cada tipo puede ser:

* Permanent eligible.
* Permanent active.
* Time-bound eligible.
* Time-bound active.

Las asignaciones pueden extenderse o renovarse cuando expiran.

Microsoft recomienda mantener **cero asignaciones permanentemente activas**, excepto las dos cuentas de acceso de emergencia (*break-glass*) recomendadas, que deben tener el rol permanente de Global Administrator.

---

# Configurar Privileged Identity Management

Microsoft Entra ID asigna automáticamente los roles **Microsoft 365 Security Administrator** y **Privileged Role Administrator** a la primera persona que utiliza PIM en una instancia de Microsoft Entra ID. Esta persona debe ser un usuario elegible de Microsoft Entra. Solo los Privileged Role Administrators pueden administrar las asignaciones de roles de directorio de Microsoft Entra de otros usuarios.

El proceso de asignación de roles de PIM comprende:

* Configurar los ajustes de PIM.
* Asignar roles a usuarios.
* Activar asignaciones.
* Aprobar o rechazar solicitudes.
* Extender y renovar asignaciones.

PIM envía notificaciones por correo electrónico cuando ocurren eventos importantes relacionados con roles, como asignaciones o activaciones, incluyendo enlaces a tareas relevantes.

## Configurar ajustes de roles

Los ajustes de los roles definen propiedades como:

* Requisitos de MFA y aprobación para la activación.
* Duración máxima de las asignaciones.
* Configuración de notificaciones.

Se requiere **Global Administrator** o **Privileged Role Administrator** para administrar los ajustes de PIM de un rol de Microsoft Entra. Los ajustes se definen individualmente para cada rol y todas sus asignaciones siguen la misma configuración.

### Descubrir y mitigar roles privilegiados

La organización debe:

* Revisar los usuarios asignados.
* Identificar administradores que ya no necesitan el rol.
* Eliminarlos de sus asignaciones.

Las revisiones de acceso de roles de Microsoft Entra pueden automatizar el descubrimiento, revisión y aprobación o eliminación de asignaciones.

### Determinar los roles que PIM debe administrar

Después de identificar los roles privilegiados, se deben priorizar los roles con más permisos y aquellos relacionados con datos o permisos sensibles.

PIM debe administrar primero todos los roles **Global Administrator** y **Security Administrator**, ya que los usuarios con estos roles pueden causar mayor impacto si sus cuentas son comprometidas. También deben protegerse otros roles vulnerables utilizados por la organización.

### Configurar ajustes de PIM

Se deben definir los ajustes para cada rol privilegiado de Microsoft Entra utilizado por la organización.

Los ajustes disponibles incluyen:

* **Activation maximum duration:** duración máxima de una activación, entre 1 y 24 horas.
* **Require multifactor authentication on activation:** requiere MFA antes de activar un rol elegible.
* **Require justification on activation:** exige una justificación empresarial.
* **Require ticket information on activation:** permite exigir un número de ticket de soporte; es únicamente informativo y PIM no valida su correlación con un sistema de tickets.
* **Require approval to activate:** requiere aprobación para activar una asignación elegible. Debe existir al menos un aprobador y Microsoft recomienda al menos dos.
* **Assignment duration:** define la duración máxima predeterminada de las asignaciones elegibles y activas.
* **Require multifactor authentication on active assignment:** exige MFA al crear una asignación activa.
* **Require justification on active assignment:** exige justificación al crear una asignación activa.
* **Notification settings:** permiten controlar destinatarios y tipos de notificaciones.

Las asignaciones elegibles pueden configurarse como permanentes o con fecha de inicio y finalización. Las asignaciones activas también pueden ser permanentes o tener fechas determinadas. Global Administrators y Privileged Role Administrators pueden renovar asignaciones con fecha de finalización y los usuarios pueden solicitar extensiones o renovaciones.

Las notificaciones pueden:

* Desactivarse.
* Enviarse únicamente a direcciones especificadas.
* Enviarse a destinatarios predeterminados y adicionales.
* Limitarse a correos críticos que requieran acción inmediata.

## Asignar roles a usuarios

Un Global Administrator puede realizar asignaciones permanentes de roles administrativos de Microsoft Entra. Los Privileged Role Administrators pueden realizar asignaciones permanentes y también hacer que usuarios sean elegibles para roles administrativos.

Un administrador elegible puede activar el rol cuando necesita utilizarlo, permaneciendo activo durante la duración configurada. PIM admite roles de Microsoft Entra integrados y personalizados.

Una asignación incluye:

* **Miembros o propietarios** a los que se asigna el rol.
* **Scope:** limita el rol a un conjunto específico de recursos.
* **Tipo de asignación:** eligible o active.
* **Duración:** permanent o time-bound.

Las asignaciones **eligible** pueden requerir:

* MFA.
* Justificación empresarial.
* Aprobación.

Las asignaciones **active** no requieren acciones adicionales para utilizar los privilegios.

Las asignaciones permanentes no tienen fecha de expiración, mientras que las asignaciones time-bound expiran al finalizar el período especificado.

Para determinados roles, PIM permite limitar el scope a una unidad administrativa, service principal o aplicación.

## Activar asignaciones

Un usuario elegible debe activar su rol cuando necesita realizar acciones privilegiadas. En lugar de asignar permanentemente un rol amplio como Global Administrator, los Privileged Role Administrators pueden hacer elegible al usuario para un rol específico, como Exchange Online Administrator.

La activación proporciona el control administrativo durante un período predeterminado. Si el rol requiere aprobación, PIM envía una notificación al aprobador; si no la requiere, el usuario puede comenzar a utilizar el rol inmediatamente.

## Aprobar o rechazar solicitudes

Los aprobadores delegados reciben notificaciones cuando existe una solicitud pendiente. Pueden visualizarla, aprobarla o rechazarla desde PIM.

Una vez aprobada, el usuario o grupo puede comenzar a utilizar el rol asignado.

## Extender y renovar asignaciones

Las asignaciones pueden configurarse con fechas de inicio y finalización. Cuando se aproxima la expiración, PIM envía notificaciones a los usuarios o grupos afectados y a los administradores del recurso.

El sistema puede mantener las asignaciones visibles durante hasta **30 días** en estado expirado, independientemente de que un administrador haya extendido el acceso.

Existen dos acciones:

* **Extend:** solicitar una extensión cuando la asignación se aproxima a su expiración.
* **Renew:** solicitar una renovación cuando la asignación ya expiró.

Ambas solicitudes iniciadas por usuarios requieren aprobación de un Global Administrator o Privileged Role Administrator.

Solo los administradores del recurso pueden extender o renovar directamente las asignaciones. El usuario o grupo afectado puede solicitar una extensión para una asignación próxima a expirar o una renovación para una asignación ya expirada.

PIM envía notificaciones sobre roles próximos a expirar dentro de los **14 días** y nuevamente un día antes de la expiración. También envía una notificación cuando la asignación expira.

Al aprobar una extensión, los administradores del recurso pueden definir:

* Nueva fecha de inicio.
* Nueva fecha de finalización.
* Tipo de asignación.

También pueden cambiar una asignación de **Eligible** a **Active** para proporcionar acceso limitado a una tarea específica sin requerir que el usuario realice la activación.

Un administrador puede extender una asignación en nombre del usuario sin requerir aprobación. El sistema notifica a los demás administradores.

---

# Auditoría de Privileged Identity Management

PIM permite visualizar actividades, activaciones e historial de auditoría de recursos de Azure, incluyendo suscripciones, grupos de recursos y máquinas virtuales. Los recursos que utilizan RBAC de Azure pueden aprovechar las capacidades de seguridad y administración del ciclo de vida de PIM.

PIM no muestra las asignaciones de roles autorizadas por un proveedor de servicios mediante **Azure delegated resource management**.

## Visualizar actividad y activaciones

Los administradores pueden consultar las acciones realizadas por un usuario sobre distintos recursos y revisar la actividad asociada a un período de activación.

Ruta:

1. **Microsoft Entra admin center**.
2. **Identity governance**.
3. **Privileged Identity Management**.
4. **Azure resources**.
5. Seleccionar el recurso.
6. Seleccionar **Roles** o **Members**.
7. Seleccionar un usuario para consultar sus acciones y activaciones.
8. Seleccionar una activación específica para ver sus detalles y la actividad correspondiente del recurso.

## Historial de auditoría

Desde el panel de PIM se puede acceder mediante:

**Manage privileged roles > Audit history**

Para consultar la auditoría de un recurso:

1. **Microsoft Entra admin center**.
2. **Identity governance**.
3. **Privileged Identity Management**.
4. **Azure resources**.
5. Seleccionar el recurso.
6. Seleccionar **Resource audit**.
7. Filtrar por una fecha predefinida o un rango personalizado.
8. En **Audit type**, seleccionar **Activate (Assigned + Activated)**.
9. En **Action**, seleccionar la actividad de un usuario para consultar sus detalles.

El historial de auditoría permite visualizar:

* Total de activaciones.
* Máximo de activaciones por día.
* Promedio de activaciones por día.
* Información filtrada por rol.

## Exportar asignaciones de roles con recursos secundarios

PIM permite consultar las asignaciones de roles de un recurso incluyendo sus recursos secundarios. Esto permite obtener una lista completa de asignaciones activas y elegibles de una suscripción, incluyendo grupos de recursos y recursos.

Para exportarlas:

1. **Microsoft Entra admin center**.
2. **Identity governance**.
3. **Privileged Identity Management**.
4. **Azure resources**.
5. Seleccionar el recurso, por ejemplo una suscripción.
6. Seleccionar **Members**.
7. Seleccionar **Export**.
8. Seleccionar **Export all members** para generar un archivo CSV con todas las asignaciones.

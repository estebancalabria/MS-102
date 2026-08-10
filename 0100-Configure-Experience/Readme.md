# Resumen — Configuración de Microsoft 365

## Introduction

La implementación de Microsoft 365 requiere primero planificar la experiencia del tenant y luego configurar esa experiencia de acuerdo con lo planificado.

El proceso de configuración de Microsoft 365 incluye:

* Configurar el **perfil de la organización**.
* Administrar las **suscripciones del tenant**.
* Administrar los **servicios y complementos (add-ins)**.
* Completar la **configuración del tenant**.

Al completar este módulo, se debe poder:

* Configurar el **perfil organizacional** de la empresa, necesario para establecer correctamente el tenant.
* Mantener los **requisitos mínimos de suscripción** de la organización.
* Administrar servicios y complementos.
* Asignar **licencias adicionales** cuando sea necesario.
* Comprar **almacenamiento adicional** cuando sea necesario.
* Configurar diferentes **opciones a nivel de organización** del tenant.

### Configuración de SharePoint Online y OneDrive

Se pueden configurar opciones de **SharePoint Online** y **OneDrive** relacionadas con el **uso compartido externo**.

El uso compartido externo permite que los usuarios compartan contenido con personas fuera de la organización, como:

* Socios.
* Proveedores.
* Clientes.
* Otros usuarios externos.

Estas configuraciones permiten establecer el nivel de control sobre el uso compartido externo que requiere la organización.

### Configuración de Microsoft Teams

También se pueden configurar **opciones a nivel de tenant** para controlar cómo los usuarios pueden realizar reuniones en **Microsoft Teams**.

### Unified Audit Logging

Se puede habilitar **Unified Audit Logging** para:

* Supervisar incidentes de seguridad.
* Investigar incidentes de seguridad.
* Detectar o investigar incumplimientos de compliance.
* Analizar problemas operativos.
* Generar informes de auditoría.
* Generar alertas basadas en eventos o criterios específicos.

### Checklist de configuración

Finalmente, se puede crear una **checklist de configuración** para verificar que el tenant de Microsoft 365 cumpla con las necesidades del negocio.

La idea es aplicar el principio:

> **Plan your work and work your plan.**

Es decir, planificar previamente la configuración y utilizar una lista de comprobación para confirmar posteriormente que todos los requisitos fueron implementados.

---

# Manage your tenant subscriptions in Microsoft 365

Mantener los **requisitos mínimos de suscripción** es esencial para que una organización pueda seguir funcionando correctamente.

La cantidad de licencias debe estar equilibrada:

* **Comprar pocas licencias** puede provocar errores y retrasos en la implementación.
* **Comprar demasiadas licencias** puede generar gastos innecesarios.

Un tenant puede utilizar **group-based licensing**. Si todas las licencias disponibles ya fueron asignadas, no quedan licencias disponibles para nuevos usuarios o procesos de provisioning, lo que puede generar **provisioning errors** debido al agotamiento de las licencias.

## Administración de licencias y suscripciones

Todas las licencias:

* Activas.
* Deprovisioned.

pueden revisarse desde el **Microsoft 365 admin center**.

Ruta:

**Microsoft 365 admin center → Billing → Licenses → Subscriptions**

Desde esta página el administrador puede:

* Asignar licencias a cuentas de usuario.
* Quitar licencias de cuentas de usuario.
* Comprar licencias adicionales.

### Compra de licencias adicionales y billing date

Comprar licencias adicionales puede modificar la **fecha de facturación mensual** de esas licencias específicas.

Por ejemplo:

* Suscripción principal comprada el **14 de mayo**.
* Licencias adicionales compradas el **15 de mayo**.

Los siguientes ciclos de facturación pueden mostrar fechas de vencimiento diferentes:

* Suscripción principal → **14 de junio**.
* Licencias adicionales → **15 de junio**.

Es decir, las licencias compradas posteriormente pueden tener un **billing cycle independiente** respecto de la suscripción original.

---

## Billing group

Toda la información relacionada con las suscripciones existentes de la organización, incluyendo información de:

* Billing.
* Payments.

se encuentra dentro del grupo **Billing** del Microsoft 365 admin center.

El grupo Billing incluye las siguientes páginas:

### Purchase services

Permite:

* Comparar productos.
* Comparar hasta **tres productos simultáneamente**.
* Iniciar las compras que la organización decida realizar.

### Your products

Muestra todos los planes adquiridos por la organización.

Desde esta página también pueden mantenerse y administrarse esos planes.

### Licenses

Proporciona un resumen de:

* Las licencias contratadas para cada plan.
* Las licencias disponibles para cada plan.

Es una página fundamental para controlar si existen suficientes licencias para los usuarios y evitar problemas de provisioning.

### Bills and payments

Proporciona:

* Historial de todas las facturas cobradas a la organización.
* Métodos de pago.
* Billing profiles.

### Billing accounts

Permite administrar la relación de compra entre la organización y Microsoft.

Cada billing account contiene información que identifica a la organización, por ejemplo:

* Direcciones.
* Información de contacto.
* Información fiscal aplicable.

Las compras realizadas mediante el billing account están cubiertas por el acuerdo que la organización firmó con Microsoft.

### Payment methods

Permite definir los métodos de pago que la organización puede utilizar para pagar sus suscripciones.

### Billing notifications

Permite determinar:

* Quién recibe las notificaciones de billing dentro de la organización.
* Cómo se recibe cada billing statement.

---

# Configure tenant-level settings for Microsoft Teams

Como **Microsoft 365 administrator**, se pueden configurar diferentes **organization-level tenant settings** para Microsoft Teams.

Estos settings determinan cómo los usuarios y los invitados pueden acceder y utilizar las funcionalidades y capacidades de Teams.

Los principales grupos de configuración a nivel de organización son:

| Setting                         | Descripción                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Guest access**                | Permite habilitar o deshabilitar el acceso de invitados a Teams. Los invitados son usuarios externos que pueden participar en chats, llamadas, reuniones y canales de Teams, pero tienen acceso limitado a otros recursos. También se pueden controlar los dominios desde los que se permiten invitados y las funcionalidades disponibles para ellos.                       |
| **Teams upgrade**               | Permite controlar cómo los usuarios y las organizaciones realizan la transición de Skype for Business a Teams. Incluye modos de coexistencia y actualización como **Islands**, **Teams Only**, **Skype for Business Only**, entre otros. Cada modo determina qué aplicación se utiliza para chat, llamadas y reuniones y si los usuarios pueden cambiar entre aplicaciones. |
| **Teams settings**              | Permite personalizar diferentes aspectos de Teams, incluyendo **app setup policies, meeting policies, messaging policies, live events policies, voice settings y device settings**. Cada policy define la experiencia y permisos de usuario para un escenario determinado.                                                                                                  |
| **Teams apps**                  | Permite administrar las aplicaciones que los usuarios pueden utilizar en Teams. Se pueden ver, aprobar, cargar, bloquear o desinstalar aplicaciones. También se pueden crear **app permission policies** y **app setup policies**.                                                                                                                                          |
| **Teams analytics and reports** | Permite monitorizar y analizar el uso y rendimiento de Teams mediante reportes y dashboards, como **Teams user activity report, Teams device usage report, Teams live event usage report y call quality dashboard**.                                                                                                                                                        |

---

# Teams meeting settings

Las configuraciones de reuniones de Teams se dividen principalmente en:

1. **Meeting policy settings**.
2. **Meeting configuration settings**.

Estas configuraciones controlan cómo los usuarios pueden:

* Programar reuniones.
* Unirse a reuniones.
* Participar y operar durante reuniones.

Se pueden crear y asignar diferentes **meeting policies** a usuarios o grupos según sus necesidades.

---

# Meeting policy settings

Una **meeting policy** es un conjunto de configuraciones que define la experiencia del usuario y los permisos para las reuniones en Teams.

Se pueden utilizar:

* Meeting policies predefinidas.
* Custom meeting policies.

Las políticas pueden asignarse a:

* Usuarios individuales.
* Grupos de usuarios.
* Toda la organización.

## Principales configuraciones

### Allow scheduling private meetings

Determina si los usuarios pueden programar **private meetings**.

Las private meetings:

* No se publican en un canal.
* Tienen una lista específica de invitados.

Si está habilitado:

* Los usuarios pueden programar reuniones privadas con participantes específicos.

Si está deshabilitado:

* Los usuarios solo pueden programar channel meetings o utilizar **Meet now** en canales.

### Allow meet now in channels

Determina si los usuarios pueden iniciar una reunión instantánea dentro de un canal.

Si está habilitado:

* Los usuarios pueden iniciar un **instant meeting** en cualquier canal del que sean miembros.

Si está deshabilitado:

* Los usuarios solo pueden programar reuniones previamente.

### Allow channel meeting scheduling

Determina si los usuarios pueden programar **channel meetings**.

Los channel meetings:

* Se publican en un canal.
* Tienen como invitados a los miembros del canal.

Si está habilitado:

* Los usuarios pueden programar reuniones en cualquier canal del que sean miembros.

Si está deshabilitado:

* Solo pueden programar private meetings o utilizar Meet now en canales.

### Allow IP video

Determina si los usuarios pueden utilizar vídeo durante las reuniones.

Si está habilitado:

* Pueden activar su cámara.

Si está deshabilitado:

* Solo pueden compartir audio y contenido.

### Allow screen sharing

Determina si los usuarios pueden compartir:

* Su pantalla completa.
* Una aplicación.
* Una ventana.

Si está deshabilitado:

* Los usuarios solo pueden compartir archivos y utilizar whiteboard.

### Allow transcription

Determina si los usuarios pueden generar una **transcripción** del audio de la reunión.

Si está habilitado:

* Pueden activar transcription.
* Se genera una transcripción en tiempo real del audio.

Si está deshabilitado:

* No se genera transcript.

### Allow cloud recording

Determina si los usuarios pueden grabar y almacenar la reunión en la nube.

Si está habilitado:

* Los usuarios pueden iniciar y detener la grabación.
* El vídeo y audio se procesan y almacenan en la nube.
* La grabación puede ser accedida y compartida por el organizador y participantes.

Si está deshabilitado:

* No hay grabación disponible.

### Allow live captions

Determina si los usuarios pueden visualizar **live captions** durante una reunión.

Si está habilitado:

* Pueden activar captions en tiempo real.

Si está deshabilitado:

* No están disponibles las captions.

### Media bit rate (Kbps)

Determina el **máximo bitrate** para el tráfico multimedia de las reuniones.

Un bitrate mayor:

* Puede mejorar la calidad de audio y vídeo.
* También aumenta el consumo de ancho de banda.

El administrador puede establecer un valor máximo que equilibre:

* Calidad.
* Uso de bandwidth.

### Allow live events

Determina si los usuarios pueden crear y organizar **live events**.

Los live events son eventos online de gran escala que pueden tener hasta **10.000 asistentes**.

Si está habilitado:

* Los usuarios pueden crear y organizar live events.

Si está deshabilitado:

* Los live events no están disponibles.

---

# Meeting configuration settings

Una **meeting configuration** es un conjunto de configuraciones que se aplica a **todas las reuniones de la organización**.

Estas configuraciones se pueden administrar desde:

**Microsoft Teams admin center → Meetings → Meeting settings**

## Designated presenter role mode

Determina quién puede actuar como **presenter** durante las reuniones.

Un presenter puede:

* Compartir contenido.
* Silenciar participantes.
* Admitir personas desde el lobby.

Las opciones son:

1. **Everyone**.
2. **Everyone in the same organization**.
3. **Everyone in the same organization and federated users**.
4. **Organizer only**.

La opción seleccionada determina quién puede ser presenter en todas las reuniones de la organización.

## Who can bypass the lobby

Determina quién puede entrar directamente a la reunión sin esperar en el lobby.

Las opciones son:

1. **Everyone**.
2. **Everyone in my organization**.
3. **Everyone in my organization and federated organizations**.
4. **Everyone in my organization and trusted organizations**.
5. **People I invite**.
6. **Only me**.

## Announce when callers join or leave

Determina si se reproduce un sonido cuando alguien se une o abandona una reunión.

## Allow dial-in users to bypass the lobby

Determina si los usuarios que ingresan por teléfono pueden evitar el lobby.

## Automatically admit people

Determina quién puede ser admitido automáticamente a una reunión sin pasar por el lobby.

Opciones:

1. **Everyone**.
2. **Everyone in your organization**.
3. **Everyone in your organization and federated organizations**.
4. **Everyone in your organization and trusted organizations**.

## Allow anonymous users to join a meeting

Determina si usuarios que no están autenticados en Teams pueden unirse mediante el enlace de la reunión.

## Allow users to chat privately

Determina si los usuarios pueden enviar mensajes privados durante una reunión.

## Allow users to send reactions

Determina si los usuarios pueden utilizar reacciones emoji durante una reunión.

## Allow users to view shared notes

Determina si los usuarios pueden ver y editar las notas compartidas durante o después de la reunión.

---

# Diferencia clave: Meeting policy vs Meeting configuration

| Aspecto   | Meeting policy                                                                                  | Meeting configuration                                                              |
| --------- | ----------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Alcance   | Usuarios, grupos o toda la organización                                                         | Todas las reuniones de la organización                                             |
| Propósito | Define experiencia y permisos                                                                   | Define configuración general de reuniones                                          |
| Ejemplos  | Private meetings, Meet now, channel scheduling, video, screen sharing, transcription, recording | Presenter, lobby, anonymous access, dial-in, private chat, reactions, shared notes |

---

# Knowledge check — Microsoft Teams

**Pregunta:** ¿Qué tenant-level setting permite personalizar app setup policies, meeting policies, messaging policies, live events policies, voice settings y device settings?

**Respuesta: Teams settings**

---

# Enable Unified Audit Logging in Microsoft 365

**Unified Audit Logging** es una funcionalidad de Microsoft 365 que permite **registrar y rastrear actividades de usuarios y administradores** en diferentes servicios y aplicaciones.

Entre los servicios incluidos se encuentran:

* Exchange Online.
* SharePoint Online.
* OneDrive.
* Microsoft Teams.
* Power BI.
* Microsoft Entra ID.

El **Unified Audit Log** proporciona una colección centralizada de eventos de auditoría relacionados con Microsoft 365.

Puede registrar actividades como:

* Descargas de archivos desde SharePoint o OneDrive.
* Inicios de sesión de usuarios.
* Acciones administrativas.
* Actividades de aplicaciones.
* Otras acciones relevantes de servicios de Microsoft 365.

## Beneficios de Unified Audit Logging

### Mejorar seguridad y compliance

Ayuda a detectar y responder ante:

* Actividades sospechosas.
* Actividades no autorizadas.
* Data breaches.
* Malware attacks.
* Policy violations.

### Mejorar la eficiencia operativa

Permite identificar y resolver problemas como:

* Errores de configuración.
* Service outages.
* Problemas reportados por usuarios.

### Obtener visibilidad sobre el comportamiento de los usuarios

Permite analizar actividades como:

* Acceso a archivos.
* Compartición de archivos.
* Colaboración.
* Comunicación.
* Otras acciones realizadas por usuarios.

---

# Acceso al Unified Audit Log

El audit log puede consultarse desde el **Microsoft Purview portal**.

Las actividades están agrupadas por servicio, facilitando la búsqueda de eventos específicos.

Desde el audit log se pueden:

* Buscar eventos.
* Filtrar actividades.
* Analizar acciones de usuarios y administradores.
* Generar reportes.
* Crear alertas.
* Investigar incidentes.

---

# Actividades registradas

El audit log captura una amplia variedad de actividades.

## Application administration activities

Incluye actividades relacionadas con aplicaciones registradas en **Microsoft Entra ID**, como:

* Agregar aplicaciones.
* Modificar aplicaciones.
* Agregar delegation entries.
* Administrar service principals.
* Modificar authentication permissions.

## Microsoft Defender for Identity activities

Las actividades de **Microsoft Defender for Identity** se registran en el Unified Audit Log cuando están habilitadas en el **Microsoft Defender XDR portal**.

Para poder visualizar estas actividades:

* El Unified Audit Log debe estar habilitado.

## Custom Searches

La funcionalidad **Audit search** permite crear búsquedas personalizadas para recuperar información relevante del Unified Audit Log.

---

# Estado predeterminado del auditing

El **audit logging está activado por defecto** para las organizaciones de Microsoft 365.

Sin embargo, al configurar una organización nueva se recomienda **verificar el estado de auditing**.

Esto permite confirmar que el registro de actividades está funcionando correctamente.

---

# Retención de audit logs

Cuando auditing está habilitado en el Microsoft Purview portal:

* Las actividades de usuarios y administradores se registran en el audit log.
* Los datos se retienen automáticamente durante **180 días** como período predeterminado.

La duración de retención comienza cuando los datos se agregan al auditing log.

La retención depende de:

* **Audit log retention policies**.
* La **licencia asignada a los usuarios**.

Los cambios en:

* User licensing.
* Retention policies.

también pueden modificar la fecha de expiración de los audit data.

### Importante: cambio de 90 a 180 días

Los **Audit (Standard) logs**:

* Generados **antes del 17 de octubre de 2023** → se retienen durante **90 días**.
* Generados **el 17 de octubre de 2023 o posteriormente** → siguen el nuevo período de retención predeterminado de **180 días**.

---

# Deshabilitar auditing

Una organización puede tener motivos para no querer registrar y conservar datos de auditoría.

En ese caso, un **Global administrator** puede desactivar auditing para la organización.

### Consecuencia importante

Si se desactiva auditing en Microsoft 365:

* No se puede utilizar el **Office 365 Management Activity API** para acceder a los datos o logs de auditoría.
* No se puede utilizar **Microsoft Sentinel** para acceder a esos datos.
* Las búsquedas desde Microsoft Purview no devuelven resultados.
* `Search-UnifiedAuditLog` en Exchange Online PowerShell no devuelve resultados.

Por lo tanto, desactivar auditing elimina la capacidad de consultar los audit logs de la organización mediante estos mecanismos.

---

# Verify the auditing status for your organization

El estado del Unified Audit Log puede verificarse mediante **Exchange Online PowerShell**.

Comando:

```powershell
Get-AdminAuditLogConfig | Format-List UnifiedAuditLogIngestionEnabled
```

La propiedad:

**UnifiedAuditLogIngestionEnabled**

indica si auditing está habilitado.

### Resultados

* `True` → auditing está activado.
* `False` → auditing no está activado.

### Importante

El comando debe ejecutarse en **Exchange Online PowerShell**.

Aunque `Get-AdminAuditLogConfig` también está disponible en **Security & Compliance PowerShell**, la propiedad:

`UnifiedAuditLogIngestionEnabled`

aparece siempre como `False` allí, incluso cuando auditing está habilitado.

**Punto clave para examen:** para verificar correctamente `UnifiedAuditLogIngestionEnabled`, utilizar **Exchange Online PowerShell**.

---

# Turn on auditing

Para activar o desactivar auditing se necesita tener asignado el **Audit Logs role** en Exchange Online.

Por defecto, este rol está asignado a los siguientes role groups en el **Exchange admin center → Permissions**:

* **Compliance Management**.
* **Organization Management**.

Si auditing no está habilitado, puede activarse mediante:

* **Microsoft Purview portal**.
* **Exchange Online PowerShell**.

Después de activarlo puede tardar **hasta aproximadamente una hora** antes de que las búsquedas del audit log comiencen a devolver resultados.

---

# Enable auditing from Microsoft Purview

Pasos:

1. Iniciar sesión en **Microsoft Purview portal**.
2. Seleccionar la tarjeta **Audit**.
3. Si la tarjeta Audit no aparece:

   * Seleccionar **View all solutions**.
   * Seleccionar **Audit** dentro de la sección **Core**.
4. Si auditing no está habilitado, aparecerá un banner para comenzar a registrar las actividades.
5. Seleccionar **Start recording user and admin activity**.

Esto habilita el registro de las actividades de usuarios y administradores.

---

# Enable auditing using Exchange Online PowerShell

Primero se debe conectar a **Exchange Online PowerShell**.

Después ejecutar:

```powershell
Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true
```

Este comando establece:

`UnifiedAuditLogIngestionEnabled = True`

y activa la ingesta de eventos en el Unified Audit Log.

---

# Configure audit log retention policies

Además de habilitar auditing, una organización debe considerar configurar una **audit log retention policy**.

Ruta:

**Microsoft Purview portal → Audit → Policies → Create audit retention policy**

Una retention policy permite especificar:

* Cuánto tiempo se deben conservar los audit logs.
* Qué servicios se incluyen.
* Qué actividades se incluyen.

### Retención

El período predeterminado indicado en el módulo es:

**180 días (6 meses)**.

Puede extenderse hasta:

**10 años**.

La duración efectiva depende de las políticas de retención y de las licencias asignadas a los usuarios.

---

# Search and export audit logs

Los audit logs pueden buscarse desde:

**Microsoft Purview portal → Audit → Search**

Durante la búsqueda se puede especificar:

* **Date range**.
* **Service**.
* **Activity**.

También se pueden utilizar:

* Filters.
* Keywords.

para refinar los resultados.

Los resultados pueden exportarse a:

* **CSV**.
* **Azure Storage account**.

---

# Create audit alerts

Se pueden crear **audit alerts** para detectar determinadas actividades.

Ruta indicada en el módulo:

**Microsoft Purview portal → Solutions → Compliance Manager → Policies → +Add**

Al crear una alerta se pueden definir:

* Conditions.
* Actions.
* Recipients.

También se pueden crear custom alerts mediante PowerShell utilizando:

```powershell
New-ProtectionAlert
```

---

# View audit reports

Los informes de auditoría pueden consultarse desde:

**Microsoft Purview portal → Solutions → Compliance Manager → Reports**

Se pueden consultar reportes predefinidos, como:

* **History Report**.

Estos reportes proporcionan una visión general de las actividades registradas.

---

# Unified Audit Logging — conceptos clave para examen

* **Unified Audit Logging** registra actividades de usuarios y administradores de diferentes servicios de Microsoft 365.
* Servicios incluidos:

  * Exchange Online.
  * SharePoint Online.
  * OneDrive.
  * Teams.
  * Power BI.
  * Microsoft Entra ID.
* El **Unified Audit Log** proporciona una colección centralizada de eventos de auditoría.
* Permite investigar:

  * Security incidents.
  * Compliance violations.
  * Operational issues.
* También permite:

  * Generar audit reports.
  * Generar alerts.
  * Realizar custom searches.
* El auditing está **activado por defecto** en las organizaciones de Microsoft 365.
* La retención predeterminada indicada para los audit data es **180 días**.
* Audit (Standard) logs anteriores al **17/10/2023** tienen una retención de **90 días**.
* Audit (Standard) logs generados desde el **17/10/2023** tienen una retención predeterminada de **180 días**.
* La retención depende también de:

  * Audit log retention policies.
  * Licencias de los usuarios.
* La retención puede configurarse mediante políticas y puede extenderse hasta **10 años**, según lo indicado por el módulo.
* Un **Global administrator** puede desactivar auditing.
* Si auditing está desactivado:

  * Microsoft Purview Audit no devuelve resultados.
  * `Search-UnifiedAuditLog` no devuelve resultados.
  * Office 365 Management Activity API no puede utilizarse para acceder a los audit logs.
  * Microsoft Sentinel no puede utilizarse para acceder a esos datos.
* Para verificar el estado del auditing se utiliza:

```powershell
Get-AdminAuditLogConfig | Format-List UnifiedAuditLogIngestionEnabled
```

* `True` = auditing habilitado.
* `False` = auditing deshabilitado.
* El comando debe ejecutarse en **Exchange Online PowerShell**, no en Security & Compliance PowerShell.
* Para activar auditing mediante PowerShell:

```powershell
Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true
```

* Se necesita el **Audit Logs role** para activar o desactivar auditing.
* Por defecto, el Audit Logs role está asignado a:

  * Compliance Management.
  * Organization Management.
* Después de activar auditing puede tardar **hasta aproximadamente una hora** antes de que las búsquedas devuelvan resultados.
* Desde Microsoft Purview se activa mediante:
  **Audit → Start recording user and admin activity**.
* Se recomienda configurar **audit log retention policies**.
* Las políticas se administran desde:
  **Microsoft Purview → Audit → Policies**.
* Los audit logs pueden buscarse desde:
  **Microsoft Purview → Audit → Search**.
* Las búsquedas pueden utilizar:

  * Date range.
  * Service.
  * Activity.
  * Filters.
  * Keywords.
* Los resultados pueden exportarse a:

  * CSV.
  * Azure Storage account.
* Se pueden crear audit alerts definiendo:

  * Conditions.
  * Actions.
  * Recipients.
* También pueden crearse custom alerts mediante:

```powershell
New-ProtectionAlert
```

* Los audit reports pueden consultarse desde:
  **Microsoft Purview → Solutions → Compliance Manager → Reports**.
* Un ejemplo de reporte predefinido es **History Report**.

---

# Complete your tenant configuration in Microsoft 365

Finalizar la configuración del tenant de Microsoft 365 es un paso fundamental para garantizar una transición fluida para los usuarios y mantener la **seguridad y el compliance**.

Una **checklist estructurada** permite a los administradores verificar que todos los componentes necesarios estén correctamente configurados y funcionando.

Las configuraciones concretas pueden variar según las necesidades de cada organización, pero existen varias tareas habituales que deberían comprobarse antes de considerar terminado el proceso.

---

## Common tasks for tenant configuration

### 1. User and Mailbox Migration

Verificar que:

* Todos los usuarios hayan sido migrados.
* Los usuarios tengan mailboxes completamente funcionales.
* Se haya realizado la migración de datos correspondiente cuando sea necesaria.

### 2. System Resources and Permissions

Configurar y asignar los **permisos necesarios** para los recursos del sistema.

Se debe comprobar que los usuarios y servicios tengan únicamente los permisos requeridos para sus funciones.

### 3. Domain Configuration

Transferir y verificar los **custom domains**, también conocidos como **vanity domains**.

Se debe comprobar que los dominios utilizados por la organización estén correctamente configurados y verificados.

### 4. Device Management

Registrar los dispositivos **Windows 10 y Windows 11** en **Microsoft Intune**.

Si la organización utiliza **Microsoft Endpoint Configuration Manager**, también se debe configurar **co-management** cuando corresponda.

### 5. Mobile Device Governance

Implementar políticas de **governance para dispositivos móviles**.

Estas políticas permiten establecer cómo se administran y protegen los dispositivos móviles utilizados para acceder a los recursos corporativos.

### 6. DNS Records and Mail Flow

Actualizar y verificar los **DNS records** globalmente.

También se deben configurar las políticas necesarias para proteger las comunicaciones por correo electrónico.

### 7. Identity Synchronization

Si la organización utiliza sincronización de identidades, configurar y validar:

**Microsoft Entra Connect Sync**

Esto permite comprobar que la sincronización entre el entorno correspondiente y Microsoft Entra ID funciona correctamente.

### 8. Multifactor Authentication (MFA)

Habilitar **MFA** para agregar una capa adicional de seguridad a las identidades de los usuarios.

### 9. Security and Compliance Enhancements

Implementar las principales medidas de seguridad y compliance, incluyendo:

* **Conditional Access policies**.
* Deshabilitar **legacy authentication**.
* Configurar **audit logging**.

Estas configuraciones ayudan a proteger el entorno y mejorar la capacidad de detectar e investigar actividades.

### 10. Data Protection

Configurar políticas de **Data Loss Prevention (DLP)**.

También se debe habilitar **Azure Information Protection (AIP)** para:

* Clasificar información sensible.
* Proteger información sensible.

### 11. Monitoring and Reporting

Utilizar herramientas como **Microsoft Secure Score** para:

* Supervisar la configuración de seguridad.
* Identificar oportunidades de mejora.
* Mejorar progresivamente la postura de seguridad del tenant.

### 12. Regular Security Reviews

La configuración del tenant no debe considerarse un proceso único.

Se deben revisar y actualizar periódicamente:

* Security settings.
* Governance policies.

Esto permite mantener el entorno alineado con las necesidades de seguridad y compliance de la organización.

---

# Verifying tenant readiness

Una vez realizadas las configuraciones, se deben utilizar herramientas que permitan comprobar que el entorno está preparado.

## Microsoft Remote Connectivity Analyzer

El **Microsoft Remote Connectivity Analyzer** permite comprobar:

* DNS records.
* Mail flow settings.

Es útil para verificar que los servicios de comunicación y conectividad estén correctamente configurados.

## Microsoft Support and Recovery Assistant (SARA)

El **Microsoft Support and Recovery Assistant (SARA)** permite:

* Diagnosticar problemas comunes de conectividad.
* Ayudar a resolver problemas de configuración y conectividad.

Estas herramientas complementan la checklist de configuración y ayudan a detectar problemas antes de considerar el tenant listo para los usuarios.

---

# Tenant-to-tenant migration

Una **tenant-to-tenant migration** consiste en transferir datos y configuraciones desde un tenant de Microsoft 365 hacia otro tenant.

Este tipo de migración puede ser necesario, por ejemplo, en situaciones de:

* **Mergers**.
* **Acquisitions**.
* **Business restructurings**.

Las migraciones tenant-to-tenant son procesos complejos y especializados.

**Importante:** las tenant-to-tenant migrations están **fuera del alcance de este entrenamiento**.

---

# Checklist final de configuración del tenant

Una forma práctica de verificar la preparación del tenant es utilizar una checklist como la siguiente:

* [ ] Perfil de la organización configurado.
* [ ] Suscripciones revisadas.
* [ ] Cantidad de licencias suficiente.
* [ ] Licencias asignadas correctamente.
* [ ] Servicios y add-ins configurados.
* [ ] Almacenamiento revisado.
* [ ] SharePoint Online configurado.
* [ ] OneDrive configurado.
* [ ] External sharing revisado.
* [ ] Guest access de Teams revisado.
* [ ] Teams upgrade configurado.
* [ ] Teams settings configurados.
* [ ] Teams apps revisadas.
* [ ] Meeting policies configuradas.
* [ ] Meeting configuration revisada.
* [ ] Unified Audit Logging habilitado y verificado.
* [ ] Audit log retention policies revisadas.
* [ ] Audit searches y reports disponibles.
* [ ] Audit alerts configuradas cuando corresponda.
* [ ] Usuarios migrados.
* [ ] Mailboxes funcionando correctamente.
* [ ] System resources y permissions configurados.
* [ ] Custom domains transferidos y verificados.
* [ ] Dispositivos Windows 10/11 registrados en Intune.
* [ ] Co-management configurado cuando corresponda.
* [ ] Mobile device governance implementado.
* [ ] DNS records verificados.
* [ ] Mail flow verificado.
* [ ] Microsoft Entra Connect Sync validado cuando corresponda.
* [ ] MFA habilitado.
* [ ] Conditional Access configurado.
* [ ] Legacy authentication deshabilitada.
* [ ] Audit logging configurado.
* [ ] DLP configurado.
* [ ] Azure Information Protection habilitado cuando corresponda.
* [ ] Microsoft Secure Score revisado.
* [ ] Security settings revisados.
* [ ] Governance policies revisadas.
* [ ] Microsoft Remote Connectivity Analyzer utilizado para verificar DNS y mail flow.
* [ ] Microsoft Support and Recovery Assistant utilizado cuando sea necesario para diagnosticar problemas.

---

# Resumen final del módulo

La configuración de un tenant de Microsoft 365 debe abordarse como un proceso estructurado: **planificar, configurar, verificar y mantener**.

Los principales bloques de trabajo son:

1. **Configurar la organización**.
2. **Administrar suscripciones y licencias**.
3. **Configurar servicios y add-ins**.
4. **Configurar SharePoint Online y OneDrive**, especialmente el external sharing.
5. **Configurar Microsoft Teams a nivel de tenant**.
6. **Configurar las políticas y opciones de reuniones de Teams**.
7. **Habilitar y administrar Unified Audit Logging**.
8. **Completar la configuración de identidades, dispositivos, dominios, DNS y mail flow**.
9. **Implementar controles de seguridad y compliance**, como MFA, Conditional Access, DLP y audit logging.
10. **Verificar la preparación del tenant** mediante herramientas de diagnóstico y una checklist.
11. **Revisar periódicamente** la configuración de seguridad y governance.

La configuración no termina cuando los servicios están funcionando. Un tenant correctamente preparado debe mantenerse mediante **monitoring, reporting, auditoría y revisiones periódicas**.

El objetivo final es garantizar que el entorno de Microsoft 365 sea **funcional, seguro, gobernado y alineado con las necesidades del negocio**.


# Sincronización de directorios con Microsoft 365

## Introducción

La sincronización de directorios permite sincronizar identidades u objetos —usuarios, grupos, contactos y equipos— entre directorios diferentes. En Microsoft 365, normalmente se realiza entre **Active Directory local (on-premises)** y **Microsoft Entra ID**.

> Azure Active Directory (Azure AD) ahora se denomina Microsoft Entra ID.

Antes de implementar la sincronización, las organizaciones deben preparar los entornos local y cloud, principalmente mediante:

* Preparación de Active Directory local.
* Configuración de sufijos UPN.
* Uso de Microsoft 365 IdFix.

Las principales herramientas de sincronización son:

* **Microsoft Entra Connect Sync**: solución instalada localmente, con mayor infraestructura y footprint.
* **Microsoft Entra Cloud Sync**: utiliza agentes ligeros, tiene menor footprint y permite administrar la configuración de aprovisionamiento desde la nube.

Microsoft Entra Connect Sync es fácil de implementar, pero requiere una planificación detallada cuando existen implementaciones complejas de Active Directory o requisitos especiales.

---

# Planificación del despliegue de Microsoft Entra ID

Una infraestructura de identidad bien planificada permite proporcionar acceso seguro a aplicaciones y datos únicamente a usuarios y dispositivos conocidos.

La implementación puede organizarse en fases que pueden completarse durante 30, 60, 90 días o más. Muchas recomendaciones pueden implementarse con **Microsoft Entra Free** o sin licencia; cuando se requiere una licencia específica, se indica a continuación.

## Fase 1: Crear una base de seguridad

Objetivo: establecer las funcionalidades de seguridad fundamentales antes de importar o crear las cuentas normales de usuario.

Principales tareas:

| Tarea                                                                                                              | Licencia                   |
| ------------------------------------------------------------------------------------------------------------------ | -------------------------- |
| Crear entre 2 y 4 cuentas de Global Administrator cloud-only para emergencias, con contraseñas largas y complejas. | Microsoft Entra Free       |
| Utilizar roles administrativos distintos de Global Administrator cuando sea posible y aplicar mínimo privilegio.   | Microsoft Entra Free       |
| Habilitar Privileged Identity Management para realizar seguimiento del uso de roles administrativos.               | Microsoft Entra Premium P2 |
| Implementar Self-Service Password Reset.                                                                           | Microsoft Entra Premium P1 |
| Crear una lista personalizada de contraseñas prohibidas específica de la organización.                             | Microsoft Entra Premium P1 |
| Integrar la protección de contraseñas de Microsoft Entra con el entorno local.                                     | Microsoft Entra Premium P1 |
| Aplicar las recomendaciones de Microsoft sobre contraseñas.                                                        | Microsoft Entra Free       |
| Deshabilitar los cambios periódicos de contraseña para cuentas cloud-only.                                         | Microsoft Entra Free       |
| Personalizar Smart Lockout de Microsoft Entra.                                                                     | Microsoft Entra Premium P1 |
| Habilitar Extranet Smart Lockout para AD FS.                                                                       | —                          |
| Bloquear autenticación heredada mediante Conditional Access.                                                       | Microsoft Entra Premium P1 |
| Implementar MFA mediante políticas de Conditional Access.                                                          | Microsoft Entra Premium P1 |
| Habilitar Microsoft Entra ID Protection para detectar inicios de sesión riesgosos y credenciales comprometidas.    | Microsoft Entra Premium P2 |
| Utilizar detecciones de riesgo para activar MFA, cambios de contraseña o bloqueo de inicios de sesión.             | Microsoft Entra Premium P2 |
| Habilitar el registro combinado para SSPR y MFA.                                                                   | Microsoft Entra Premium P1 |

## Fase 2: Importar usuarios, habilitar sincronización y administrar dispositivos

Esta fase agrega a la base de seguridad:

* Importación de usuarios.
* Sincronización.
* Planificación del acceso de invitados.
* Preparación para funcionalidades adicionales.

Principales tareas:

| Tarea                                                                                                                 | Licencia                            |
| --------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| Instalar Microsoft Entra Connect Sync para sincronizar usuarios del directorio local.                                 | Microsoft Entra Free                |
| Implementar Password Hash Synchronization.                                                                            | Microsoft Entra Free                |
| Implementar Password Writeback.                                                                                       | Microsoft Entra Premium P1          |
| Implementar Microsoft Entra Connect Health para monitorizar servidores de Connect, AD FS y controladores de dominio.  | Microsoft Entra Premium P1          |
| Asignar licencias mediante pertenencia a grupos.                                                                      | Microsoft Entra Premium P1          |
| Crear un plan para acceso de usuarios invitados.                                                                      | Microsoft Entra External Identities |
| Definir la estrategia de administración de dispositivos, incluyendo registro, join, BYOD y dispositivos corporativos. | —                                   |
| Implementar Windows Hello for Business.                                                                               | —                                   |
| Implementar métodos de autenticación passwordless.                                                                    | Microsoft Entra Premium P1          |

## Fase 3: Administrar aplicaciones

Las organizaciones deben identificar las aplicaciones candidatas para migración e integración con Microsoft Entra ID.

Principales tareas:

* Identificar aplicaciones locales, SaaS y aplicaciones de negocio.
* Determinar qué aplicaciones pueden y deben administrarse mediante Microsoft Entra ID.
* Integrar aplicaciones SaaS disponibles en la galería de Microsoft Entra ID.
* Utilizar Application Proxy para proporcionar acceso a aplicaciones locales mediante cuentas de Microsoft Entra.

Licencias:

* Identificación de aplicaciones: sin licencia.
* Aplicaciones de la galería: Microsoft Entra Free.
* Application Proxy: Microsoft Entra Premium P1.

## Fase 4: Auditar identidades privilegiadas, revisar acceso y administrar el ciclo de vida

Objetivos:

* Aplicar mínimo privilegio.
* Realizar las primeras revisiones de acceso.
* Automatizar tareas habituales del ciclo de vida de usuarios.

Principales tareas:

| Tarea                                                                                                                                                      | Licencia                   |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| Aplicar PIM y eliminar roles administrativos de las cuentas utilizadas diariamente. El acceso privilegiado puede requerir MFA, justificación o aprobación. | Microsoft Entra Premium P2 |
| Realizar revisiones de acceso de roles de Microsoft Entra en PIM.                                                                                          | Microsoft Entra Premium P2 |
| Implementar grupos dinámicos basados en atributos como departamento, cargo o región.                                                                       | Microsoft Entra Premium P1 |
| Implementar aprovisionamiento de aplicaciones basado en grupos.                                                                                            | Microsoft Entra Premium P1 |
| Automatizar el aprovisionamiento y desaprovisionamiento de usuarios desde el sistema de origen, como RR. HH., hacia Microsoft Entra ID.                    | Microsoft Entra Premium P1 |

---

# Preparación para la sincronización de directorios

Las organizaciones suelen combinar aplicaciones locales y cloud. Los usuarios necesitan acceder a recursos de ambos entornos utilizando una identidad común.

## Provisioning

El aprovisionamiento consiste en:

1. Crear un objeto cuando se cumplen determinadas condiciones.
2. Mantenerlo actualizado.
3. Eliminarlo cuando las condiciones dejan de cumplirse.

Por ejemplo, cuando un empleado ingresa a una organización, RR. HH. registra al usuario y el aprovisionamiento puede crear la cuenta correspondiente en:

* Microsoft Entra ID.
* Active Directory local.
* Aplicaciones que el usuario necesita.

Esto permite que el usuario tenga acceso a sus sistemas y aplicaciones desde el primer día.

El aprovisionamiento de identidades puede involucrar:

* Aprovisionamiento desde RR. HH.
* Aprovisionamiento de directorios.
* Aprovisionamiento de aplicaciones.

El aprovisionamiento de identidades locales hacia Microsoft Entra ID se realiza mediante sincronización de directorios utilizando **Microsoft Entra Connect Sync** o **Microsoft Entra Cloud Sync**.

La activación de la sincronización debe considerarse un compromiso a largo plazo. Una vez activada, los objetos sincronizados solo pueden editarse mediante herramientas de administración de Active Directory local.

---

# Preparación de Active Directory local

Antes de implementar la sincronización, la organización debe:

* Identificar la fuente de autoridad.
* Limpiar Active Directory.
* Configurar auditoría.

## Source of authority

La fuente de autoridad es el lugar donde se administran originalmente los objetos de Active Directory, como usuarios y grupos, en un entorno híbrido.

Cuando un objeto se sincroniza, la fuente de autoridad pasa de Microsoft 365 al directorio local de la organización.

La fuente de autoridad puede cambiarse mediante:

* Activación de la sincronización.
* Desactivación.
* Reactivación de la sincronización desde Microsoft 365 o Windows PowerShell.

## Limpieza de Active Directory

Antes de comenzar la sincronización se deben revisar y corregir:

* Valores duplicados de `proxyAddresses`.
* Valores duplicados de `userPrincipalName`.
* Valores `userPrincipalName` vacíos o inválidos.
* Caracteres inválidos o cuestionables en:

  * `givenName`
  * `surname` (`sn`)
  * `sAMAccountName`
  * `displayName`
  * `mail`
  * `proxyAddresses`
  * `mailNickname`
  * `userPrincipalName`

---

# UPN suffixes

Antes de implementar la sincronización:

* Los objetos de usuario locales deben tener configurado un sufijo UPN.
* El sufijo UPN es la parte ubicada después de `@`, por ejemplo `@adatum.com` o `@contoso.com`.
* El sufijo debe ser correcto tanto para Active Directory como para Microsoft 365.

Cuando se utiliza un dominio enrutable en Internet como UPN, ese dominio debe ser el sufijo UPN.

Si el sufijo local no contiene un dominio DNS enrutable, como `adatum.local`, Microsoft 365 utiliza el dominio de enrutamiento predeterminado, por ejemplo `adatum.onmicrosoft.com`.

Como práctica recomendada, Microsoft recomienda utilizar la dirección SMTP principal de cada usuario como su UPN. Esto reduce confusión porque algunas aplicaciones solicitan la dirección de correo electrónico aunque técnicamente requieran el nombre de inicio de sesión UPN.

Si se modifica el sufijo UPN local, deben revisarse las aplicaciones que dependan de un UPN específico.

El UPN de Microsoft 365 puede no coincidir con el UPN local si, por ejemplo, se asignó una licencia de Microsoft 365 antes de verificar el dominio. En ese caso, Windows PowerShell puede utilizarse para actualizar los UPN de Microsoft 365 y hacerlos coincidir con el nombre y dominio corporativos.

---

# Microsoft 365 IdFix

**IdFix DirSync Error Remediation Tool** identifica y corrige la mayoría de los errores de sincronización de objetos en los bosques de Active Directory.

Debe ejecutarse antes de la sincronización para facilitar la sincronización correcta de:

* Usuarios.
* Contactos.
* Grupos.

IdFix consulta todos los dominios de Active Directory del bosque autenticado y muestra los valores de atributos que podrían producir errores durante la sincronización.

Funciones principales:

* **Confirmación de cambios:** el administrador revisa los errores y selecciona qué objetos modificar.
* **Transaction rollback:** permite deshacer actualizaciones confirmadas.
* **Exclusiones conocidas:** evita mostrar objetos críticos del sistema para edición.
* **Save to File:** exporta información en CSV o LDF para edición o investigación offline.
* **Import CSV:** permite importar cambios mediante CSV, utilizando `distinguishedName` para determinar el objeto.
* **Verbose logging:** el registro detallado está habilitado de forma predeterminada.
* **Multi-tenant y tenants dedicados:** permite validar múltiples tenants o tenants dedicados de Microsoft 365.

Debe utilizarse con precaución porque permite realizar actualizaciones masivas de objetos.

---

# Opciones de sincronización

La sincronización entre Active Directory local y Microsoft Entra ID forma parte de la identidad híbrida.

Sus beneficios incluyen:

* Una única identidad para acceder a aplicaciones locales y servicios cloud como Microsoft 365.
* Una herramienta común para facilitar la implementación de sincronización e inicio de sesión.
* Mayor productividad al utilizar una identidad común.
* Mejor gobierno de identidades, orientado a garantizar que las personas correctas tengan el acceso correcto a los recursos correctos en el momento correcto.

Las dos opciones son:

1. **Microsoft Entra Connect Sync**
2. **Microsoft Entra Cloud Sync**

---

# Microsoft Entra Connect Sync

Microsoft Entra Connect Sync es una aplicación de Microsoft instalada localmente para implementar identidad híbrida.

Normalmente se instala en un servidor local unido al dominio, aunque también puede instalarse en un controlador de dominio. Requiere una conexión HTTPS saliente hacia los servidores de Microsoft 365.

Características:

* Soporta la mayoría de los escenarios híbridos de Microsoft Entra.
* Puede utilizarse con directorios grandes.
* Tiene capacidades robustas de sincronización.
* Requiere mayor inversión de infraestructura.
* Puede ser más complejo de configurar.
* Puede generar mayores costes de mantenimiento.

## Funcionalidades

### Filtering

Permite limitar qué objetos se sincronizan.

Por defecto sincroniza:

* Usuarios.
* Contactos.
* Grupos.
* Equipos Windows 10.

El filtrado puede realizarse por:

* Dominios.
* OUs.
* Atributos.

### Password Hash Synchronization

Sincroniza el hash de la contraseña de Active Directory con Microsoft Entra ID.

Permite al usuario utilizar la misma contraseña local y cloud, administrándola desde una única ubicación.

### Password Writeback

Permite cambiar o restablecer contraseñas desde la nube y escribir los cambios nuevamente en Active Directory local.

### Device Writeback

Permite escribir dispositivos registrados en Microsoft Entra ID nuevamente en Active Directory local para utilizarlos con Conditional Access.

### Preventing accidental deletes

Protege el directorio cloud frente a múltiples eliminaciones simultáneas.

Por defecto permite hasta **500 eliminaciones por ejecución**, aunque el valor puede modificarse.

### Automatic upgrade

Mantiene Microsoft Entra Connect Sync actualizado con la versión más reciente. Está habilitado de forma predeterminada en instalaciones con Express Settings.

## Configuración

Las organizaciones pueden utilizar:

* **Express Settings** para escenarios sencillos.
* **Custom Settings** cuando existen múltiples bosques, funcionalidades opcionales o requisitos de topología que Express Settings no cubre.

Custom Settings debe utilizarse cuando Express Settings no satisface las necesidades de implementación.

## Componentes principales

### Synchronization services

Responsable de:

* Sincronizar usuarios, grupos y otros objetos.
* Mantener coincidente la información de identidad entre usuarios y grupos locales y cloud.

### Microsoft Entra Connect Health

Proporciona:

* Monitorización del estado.
* Visualización centralizada en el centro de administración de Microsoft Entra.

---

# Microsoft Entra Cloud Sync

Microsoft Entra Cloud Sync también sincroniza usuarios, grupos y contactos desde Active Directory local hacia Microsoft Entra ID.

A diferencia de Connect Sync, utiliza un modelo de **agente ligero**:

* Reduce el footprint local.
* Requiere menos infraestructura.
* La configuración de aprovisionamiento se administra desde la nube.
* Simplifica la implementación y el mantenimiento.

El agente actúa como puente entre Active Directory local y Microsoft Entra ID.

Microsoft Online Services almacena y administra la configuración de aprovisionamiento en Microsoft Entra ID.

## Ventajas

* Menor infraestructura local.
* Menores costes potenciales de infraestructura y licenciamiento.
* Menores costes de soporte y mantenimiento.
* Arquitectura simplificada.
* Implementación más rápida.
* Soporte de múltiples agentes.
* Mayor resiliencia.
* Soporte para múltiples bosques sin conectividad de red entre ellos.
* Puede utilizarse junto con Microsoft Entra Connect Sync.
* Puede actualizar Microsoft Entra ID con mayor frecuencia.

En implementaciones grandes, Connect Sync puede requerir SQL Server, mientras que Cloud Sync no necesita esa infraestructura.

### Alta disponibilidad

Se pueden instalar múltiples agentes activos para proporcionar alta disponibilidad y failover automático.

Microsoft recomienda **tres agentes activos** para alta disponibilidad.

Con múltiples agentes:

* El servicio puede continuar funcionando si falla un agente.
* Se reduce el riesgo de interrupciones.

El agente de aprovisionamiento cloud **no realiza load balancing** entre los agentes. Solo un agente está activo en cada momento.

### Múltiples bosques desconectados

Cloud Sync resulta adecuado cuando se deben aprovisionar usuarios desde múltiples bosques de Active Directory sin conectividad de red entre ellos.

Se pueden instalar agentes en cada red aislada para que cada bosque se comunique independientemente con Microsoft Entra ID.

Cloud Sync y Connect Sync pueden utilizarse simultáneamente.

---

# Comparación entre Microsoft Entra Connect Sync y Cloud Sync

Una diferencia fundamental es dónde se almacena la configuración y dónde ocurre el aprovisionamiento:

* **Connect Sync:** la configuración se almacena en el servidor local de sincronización y el aprovisionamiento se ejecuta allí.
* **Cloud Sync:** la configuración se almacena en la nube y el aprovisionamiento se ejecuta como parte del servicio de aprovisionamiento de Microsoft Entra.

| Funcionalidad                                                | Connect Sync | Cloud Sync |
| ------------------------------------------------------------ | -----------: | ---------: |
| Un único bosque AD local                                     |            ✓ |          ✓ |
| Múltiples bosques AD locales                                 |            ✓ |          ✓ |
| Múltiples bosques AD desconectados                           |              |          ✓ |
| Instalación mediante agente ligero                           |              |          ✓ |
| Múltiples agentes activos para alta disponibilidad           |              |          ✓ |
| Conexión con directorios LDAP                                |            ✓ |            |
| Objetos de usuario                                           |            ✓ |          ✓ |
| Objetos de grupo                                             |            ✓ |          ✓ |
| Objetos de contacto                                          |            ✓ |          ✓ |
| Objetos de dispositivo                                       |            ✓ |            |
| Personalización básica de attribute flows                    |            ✓ |          ✓ |
| Atributos de Exchange Online                                 |            ✓ |          ✓ |
| Extension attributes 1–15                                    |            ✓ |          ✓ |
| Atributos AD definidos por el cliente                        |            ✓ |            |
| Password Hash Synchronization                                |            ✓ |          ✓ |
| Pass-Through Authentication                                  |            ✓ |            |
| Federation                                                   |            ✓ |          ✓ |
| Seamless Single Sign-On                                      |            ✓ |          ✓ |
| Instalación en Domain Controller                             |            ✓ |          ✓ |
| Windows Server 2016                                          |            ✓ |          ✓ |
| Filtrado por dominios/OUs/grupos                             |            ✓ |          ✓ |
| Filtrado por valores de atributos                            |            ✓ |            |
| MinSync                                                      |            ✓ |          ✓ |
| Eliminación de atributos desde AD hacia Microsoft Entra ID   |            ✓ |          ✓ |
| Personalización avanzada de attribute flows                  |            ✓ |            |
| Password Writeback                                           |            ✓ |          ✓ |
| Device Writeback                                             |            ✓ |            |
| Group Writeback                                              |            ✓ |            |
| Combinación de atributos de usuario desde múltiples dominios |            ✓ |            |
| Microsoft Entra Domain Services                              |            ✓ |            |
| Exchange Hybrid Writeback                                    |            ✓ |            |
| Número ilimitado de objetos por dominio AD                   |            ✓ |            |
| Hasta 150.000 objetos por dominio AD                         |            ✓ |          ✓ |
| Grupos de hasta 50.000 miembros                              |            ✓ |          ✓ |
| Grupos grandes de hasta 250.000 miembros                     |            ✓ |            |
| Referencias entre dominios                                   |            ✓ |          ✓ |
| Aprovisionamiento bajo demanda                               |            ✓ |          ✓ |
| US Government                                                |            ✓ |          ✓ |

---

# Planificación de Microsoft Entra Connect Sync

Aunque Connect Sync es sencillo de implementar, requiere una planificación especialmente cuidadosa cuando existen:

* Active Directory complejo.
* Múltiples bosques.
* Requisitos especiales.
* Sincronización parcial de atributos.

Preguntas principales de planificación:

* ¿En qué servidor se instalará Connect Sync?
* ¿Se necesita un escenario de failover?
* ¿Se sincronizará uno o varios Active Directory o bosques?
* ¿Se sincronizará todo Active Directory o solo una parte?
* ¿Se sincronizarán todos los atributos o se utilizarán filtros?
* ¿Se utilizarán funcionalidades avanzadas como Password Hash Synchronization, Password Writeback o Device Writeback?

## Decisión sobre Password Hash Synchronization

### Implementar Password Hash Synchronization

Permite que los usuarios se autentiquen con el mismo nombre de usuario y contraseña que utilizan localmente.

Connect Sync sincroniza un hash criptográfico del hash de la contraseña y lo almacena en el objeto correspondiente de Microsoft Entra ID.

La contraseña no puede reconstruirse a partir del hash.

### No implementar Password Hash Synchronization

Si una organización no desea almacenar hashes de contraseñas de Active Directory fuera de la organización, debe utilizar:

* Active Directory Federation Services (AD FS).
* Microsoft Entra Pass-Through Authentication.

También puede utilizarse una contraseña independiente para la cuenta de Microsoft Entra.

---

# Requisitos previos de Microsoft Entra Connect Sync

## Microsoft Entra ID

Se necesita un tenant de Microsoft Entra.

La organización debe:

* Tener un tenant.
* Agregar y verificar el dominio que utilizará.
* Evitar depender únicamente del dominio predeterminado `onmicrosoft.com` cuando se utilizará un dominio propio.

Un tenant permite inicialmente **50.000 objetos**.

Después de verificar un dominio, el límite aumenta a **300.000 objetos**.

Para superar ese límite se debe abrir un caso de soporte. Para más de **500.000 objetos**, se necesita una licencia como:

* Microsoft 365.
* Microsoft Entra Premium.
* Enterprise Mobility + Security.

## Datos locales

Antes de sincronizar:

* Utilizar IdFix para detectar errores, duplicados y problemas de formato.
* Revisar las funcionalidades opcionales de sincronización y decidir cuáles habilitar.

## Active Directory local

Requisitos:

* La versión del esquema y el nivel funcional del bosque deben ser Windows Server 2003 o posteriores.
* El controlador de dominio utilizado debe ser escribible.
* No se admite un Read-Only Domain Controller (RODC).
* No se siguen write redirects.
* No se admiten bosques o dominios con nombres NetBIOS que contengan puntos.
* Microsoft recomienda habilitar Active Directory Recycle Bin.

## PowerShell

Microsoft Entra Connect Sync ejecuta scripts PowerShell firmados durante la instalación.

La política de ejecución debe permitir ejecutar scripts.

La política recomendada durante la instalación es:

`RemoteSigned`

## Servidor Microsoft Entra Connect Sync

El servidor contiene datos críticos de identidad.

Por ello:

* Debe protegerse adecuadamente el acceso administrativo.
* Debe considerarse un componente **Tier 0**.
* Debe endurecerse como un activo del plano de control.

## SQL Server

Connect Sync requiere una base de datos SQL Server para almacenar información de identidad.

Por defecto instala:

* **SQL Server 2019 Express LocalDB**.

SQL Server Express tiene un límite de **10 GB**, suficiente para aproximadamente **100.000 objetos**.

Para volúmenes mayores se debe utilizar otra instalación de SQL Server.

Requisitos para una instalación externa:

* Se admiten versiones mainstream soportadas hasta SQL Server 2019.
* No se admite Azure SQL Database.
* No se admite Azure SQL Managed Instance.
* La collation debe ser **case-insensitive** (`_CI_`).
* No se admite una collation case-sensitive (`_CS_`).
* Solo puede existir un sync engine por instancia SQL.
* No se admite compartir una instancia con FIM/MIM Sync, DirSync o Microsoft Entra Sync.

---

# Cuentas necesarias

La organización necesita una cuenta:

* **Microsoft Entra Global Administrator**, o
* **Hybrid Identity Administrator**.

Debe ser una cuenta de escuela u organización y no una Microsoft Account.

Para Express Settings o una actualización desde DirSync se necesita además una cuenta:

* **Enterprise Administrator** de Active Directory local.

La instalación con Custom Settings proporciona más opciones.

---

# Conectividad de Microsoft Entra Connect Sync

El servidor debe disponer de:

* Resolución DNS para intranet e Internet.
* Resolución hacia Active Directory local.
* Resolución hacia endpoints de Microsoft Entra.
* Conectividad de red con todos los dominios configurados.
* Conectividad con el dominio raíz de cada bosque configurado.

Si existen restricciones de proxy o firewall, deben permitirse las URLs necesarias de Microsoft 365 y Azure Portal.

## TLS

Desde la versión **1.1.614.0**, Connect Sync utiliza TLS 1.2 de forma predeterminada.

Desde la versión **2.0**, TLS 1.0 y TLS 1.1 no están soportados.

La instalación falla si TLS 1.2 no está habilitado.

Antes de la versión 1.1.614.0, TLS 1.0 se utilizaba de forma predeterminada y podía configurarse TLS 1.2.

---

# Proxy saliente

Cuando la organización utiliza un proxy saliente, deben configurarse los parámetros correspondientes en:

`C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config`

Si el proxy requiere autenticación, su dominio debe incluir la cuenta de servicio.

Para especificar una cuenta de servicio personalizada debe utilizarse Custom Settings.

Si la configuración del proxy se realiza sobre una instalación existente, debe reiniciarse el servicio de Microsoft Entra Sync para que lea la nueva configuración.

Microsoft Entra ID puede tardar hasta **5 minutos** en responder a una solicitud web durante la sincronización.

Por ello, el timeout de conexión idle del proxy debe configurarse en **al menos 6 minutos**.

Un timeout demasiado corto puede producir:

* Sincronizaciones fallidas.
* Sincronizaciones retrasadas.
* Errores.
* Procesos de sincronización más lentos de lo esperado.

---

# Requisitos de hardware de Microsoft Entra Connect Sync

| Objetos en Active Directory |     CPU | Memoria |  Disco |
| --------------------------- | ------: | ------: | -----: |
| Menos de 10.000             | 1,6 GHz |    4 GB |  70 GB |
| 10.000–50.000               | 1,6 GHz |    4 GB |  70 GB |
| 50.000–100.000              | 1,6 GHz |   16 GB | 100 GB |
| 100.000–300.000             | 1,6 GHz |   32 GB | 300 GB |
| 300.000–600.000             | 1,6 GHz |   32 GB | 450 GB |
| Más de 600.000              | 1,6 GHz |   32 GB | 500 GB |

Para **100.000 o más objetos** se requiere la versión completa de SQL Server. Por razones de rendimiento se recomienda instalarla localmente.

## AD FS y Web Application Proxy

Requisitos mínimos:

* CPU: dual core de 1,6 GHz o superior.
* Memoria: 2 GB o superior.
* Azure VM: configuración A2 o superior.

---

# Topologías de Microsoft Entra Cloud Sync

Cloud Sync admite las siguientes topologías:

## Single forest, single Microsoft Entra tenant

Un único bosque local, con uno o varios dominios, y un único tenant de Microsoft Entra.

Es la topología más sencilla.

## Multi-forest, single Microsoft Entra tenant

Múltiples bosques de Active Directory, con uno o varios dominios, y un único tenant de Microsoft Entra.

## Forest existente con Connect Sync y nuevo forest con Cloud Sync

Un entorno existente utiliza Connect Sync y un nuevo bosque se incorpora mediante Cloud Sync.

## Piloto de Cloud Sync en un bosque AD híbrido existente

Connect Sync y Cloud Sync funcionan en el mismo bosque.

En este escenario, cada objeto debe estar en scope de una sola de las herramientas.

## Consideraciones entre bosques

* Los usuarios y grupos deben identificarse de forma única entre todos los bosques.
* Cloud Sync no realiza matching entre bosques.
* Un usuario o grupo debe representarse una sola vez entre todos los bosques.
* El sistema selecciona automáticamente el source anchor.
* Utiliza `ms-DS-ConsistencyGuid` si está presente.
* Si no está presente, utiliza `ObjectGUID`.
* No se puede cambiar el atributo utilizado como source anchor.

Microsoft no admite modificar u operar Cloud Sync fuera de las configuraciones o acciones documentadas. Las configuraciones no soportadas pueden producir un estado inconsistente o no soportado.

---

# Prerrequisitos de Microsoft Entra Cloud Sync

## gMSA

Cloud Sync utiliza una **group Managed Service Account (gMSA)** para ejecutar el agente ligero.

Una gMSA proporciona:

* Administración automática de contraseñas.
* Administración simplificada de SPN.
* Delegación de administración a otros administradores.
* Extensión de estas capacidades a múltiples servidores.

Se requieren credenciales de:

* Domain Administrator, o
* Enterprise Administrator

para crear la gMSA utilizada por el agente.

## Cuenta Microsoft Entra

Se necesita una cuenta:

* **Hybrid Identity Administrator**.
* No puede ser un usuario invitado.

## Servidor del agente

Se necesita un servidor local para el agente de Cloud Sync:

* Windows Server 2016 o posterior.
* Debe tratarse como servidor Tier 0 según el modelo de niveles administrativos de Active Directory.
* El agente puede instalarse en un Domain Controller.

## Alta disponibilidad

Cloud Sync puede utilizar múltiples agentes activos para continuar funcionando si uno falla.

Microsoft recomienda **tres agentes activos** para alta disponibilidad.

## Firewall

La organización debe contemplar la configuración del firewall local necesaria para permitir la comunicación requerida por Cloud Sync.

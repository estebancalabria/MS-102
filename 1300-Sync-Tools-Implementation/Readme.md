# Implementación de herramientas de sincronización de directorios

## Introducción

Una vez planificada la implementación de sincronización de directorios, se despliega la herramienta seleccionada. Las dos herramientas de sincronización de directorios de Microsoft Entra son:

* **Microsoft Entra Connect Sync**
* **Microsoft Entra Cloud Sync**

El módulo aborda los prerrequisitos, instalación y configuración de ambas herramientas. Para **Microsoft Entra Connect Sync**, también se aborda la supervisión mediante **Microsoft Entra Connect Health**.

---

# Microsoft Entra Connect Sync

## Prerrequisitos

### Microsoft Entra ID

* Se necesita un **tenant de Microsoft Entra**.
* Puede administrarse desde:

  * Microsoft Entra admin center.
  * Office portal.
* Se debe **agregar y verificar el dominio** que se utilizará, en lugar de utilizar solamente el dominio predeterminado `onmicrosoft.com`.
* Un tenant permite inicialmente **50.000 objetos**.
* Al verificar el dominio, el límite aumenta a **300.000 objetos**.
* Para superar este límite se puede solicitar un aumento mediante soporte.
* Para más de **500.000 objetos** se necesita una licencia, como Microsoft 365, Microsoft Entra ID P1/P2 o Enterprise Mobility + Security.

### Preparación de los datos locales

* Utilizar **IdFix** para identificar errores antes de sincronizar, como duplicados y problemas de formato.
* Revisar y evaluar las características opcionales de sincronización disponibles en Microsoft Entra ID.

### Active Directory local

* El esquema de Active Directory y el nivel funcional del bosque deben ser **Windows Server 2003 o posteriores**.
* Los controladores de dominio pueden ejecutar cualquier versión que cumpla los requisitos de esquema y nivel funcional.
* El controlador de dominio utilizado por Microsoft Entra debe ser **escribible**.
* Los controladores de dominio de solo lectura (RODC) no son compatibles.
* Microsoft Entra Connect Sync no sigue redirecciones de escritura.
* No se admiten bosques o dominios con nombres NetBIOS que contengan puntos.
* Microsoft recomienda habilitar la **papelera de reciclaje de Active Directory**.

### Directiva de ejecución de PowerShell

* Microsoft Entra Connect Sync ejecuta scripts de PowerShell firmados durante la instalación.
* La directiva debe permitir la ejecución de scripts.
* La directiva recomendada durante la instalación es **RemoteSigned**.

---

## Servidor de Microsoft Entra Connect Sync

El servidor contiene datos críticos de identidad y debe protegerse adecuadamente.

* No se admiten múltiples servidores Microsoft Entra Connect Sync **activos** sincronizando con un mismo tenant.
* Se pueden instalar servidores adicionales en **staging mode** para redundancia y recuperación.
* El servidor debe tratarse como un componente **Tier 0 / Control Plane**.
* Se recomienda restringir y proteger cuidadosamente el acceso administrativo.

### Requisitos de instalación

* Puede instalarse en:

  * Controladores de dominio.
  * Servidores miembro.
  * Servidores que no estén unidos a un dominio.
* Debe ejecutarse en **Windows Server 2016 o posterior**.
* Se recomienda **Windows Server 2022**.
* Windows Server 2016 está en soporte extendido.
* Requiere como mínimo **.NET Framework 4.6.2**.
* .NET 4.8 o superior proporciona el mejor cumplimiento de accesibilidad.
* No puede instalarse en Small Business Server ni en Windows Server Essentials anteriores a 2019.
* Windows Server Essentials 2019 sí es compatible.
* El servidor debe utilizar Windows Server Standard o superior.
* Se requiere una instalación completa con **GUI**.
* Windows Server Core no es compatible.
* PowerShell Transcription Group Policy no puede estar habilitado si el asistente se utiliza para administrar la configuración de AD FS. Puede habilitarse para administrar la configuración de sincronización.

### Si se utiliza AD FS

* Los servidores de AD FS y Web Application Proxy deben utilizar **Windows Server 2012 R2 o posterior**.
* Se debe habilitar Windows Remote Management para instalaciones remotas.
* Se deben configurar certificados TLS/SSL.
* Se debe configurar la resolución de nombres.

### Otras condiciones

* No se admite interceptar y analizar el tráfico entre Microsoft Entra Connect Sync y Microsoft Entra ID, ya que puede interrumpir el servicio.
* Si los Hybrid Identity Administrators utilizan MFA, `https://secure.aadcdn.microsoftonline-p.com` debe estar en la lista de sitios de confianza.
* Si se utiliza Microsoft Entra Connect Health para sincronización, deben cumplirse sus prerrequisitos.

---

# Protección del servidor Microsoft Entra Connect Sync

Microsoft recomienda endurecer el servidor para reducir la superficie de ataque.

* Tratarlo como un activo **Control Plane / Tier 0**.
* Restringir el acceso administrativo a administradores de dominio u otros grupos de seguridad estrictamente controlados.
* Crear cuentas dedicadas para el acceso privilegiado.
* Los administradores no deberían utilizar cuentas privilegiadas para navegación web, correo electrónico o tareas cotidianas.
* Denegar autenticación **NTLM** en el servidor.
* Garantizar una contraseña de administrador local única por máquina mediante **Windows LAPS**.
* Implementar estaciones de trabajo dedicadas para acceso privilegiado.
* Aplicar directrices adicionales para reducir la superficie de ataque de Active Directory local.
* Configurar alertas para supervisar cambios en la relación de confianza entre el IdP y Microsoft Entra ID.
* Habilitar **MFA** para todos los usuarios con acceso privilegiado en Microsoft Entra ID o Active Directory local.
* Deshabilitar **Soft Matching** si no es necesario debido a sus riesgos de seguridad.
* Deshabilitar **Hard Match Takeover**, ya que puede permitir que Microsoft Entra Connect Sync tome el control de objetos administrados en la nube y cambie su origen de autoridad a Active Directory.

---

# Microsoft Entra Connect Sync en Staging Mode

Solo puede existir un servidor Microsoft Entra Connect Sync **activo** conectado a un tenant. La excepción es el uso de **staging mode**.

En staging mode:

* Se pueden conectar varios servidores al mismo tenant.
* Solo uno funciona como servidor activo.
* Los demás funcionan como servidores de staging.
* Un servidor de staging se instala en paralelo al servidor activo.
* Importa y sincroniza datos, pero **no exporta cambios a Microsoft Entra ID**.
* Se utiliza para:

  * Alta disponibilidad.
  * Probar cambios de configuración.
  * Recuperación ante desastres.
  * Migraciones y actualizaciones.
  * Validar configuraciones antes de aplicarlas en producción.
* Mientras está en staging mode no ejecuta **Password Hash Synchronization** ni **Password Writeback**.
* Puede haber varios servidores de staging.
* Los servidores de staging adicionales pueden actuar como respaldo para mantener la continuidad del entorno de staging.

---

# SQL Server utilizado por Microsoft Entra Connect Sync

Microsoft Entra Connect Sync necesita una base de datos SQL Server para almacenar datos de identidad.

* De forma predeterminada se instala **SQL Server 2019 Express LocalDB**.
* SQL Server Express tiene un límite de **10 GB**, suficiente aproximadamente para **100.000 objetos**.
* Para mayores volúmenes se puede utilizar otra instalación de SQL Server.
* La elección de SQL Server puede afectar al rendimiento.

### Requisitos de SQL externo

* Se admiten versiones de SQL Server con soporte mainstream hasta **SQL Server 2022** ejecutándose en Windows.
* **SQL Server 2012 ya no es compatible**.
* **Azure SQL Database** y **Azure SQL Managed Instance** no son compatibles como base de datos.
* Se requiere una intercalación SQL **case-insensitive (`_CI_`)**.
* Las intercalaciones case-sensitive (`_CS_`) no son compatibles.
* Solo puede existir un motor de sincronización por instancia SQL.
* Una instancia SQL no puede compartirse con FIM/MIM Sync, DirSync u otro Microsoft Entra Connect Sync.

---

# Cuentas

* Se necesita una cuenta **Global Administrator** o **Hybrid Identity Administrator** para el tenant.
* Debe ser una cuenta escolar o corporativa; no puede ser una Microsoft account.
* Con **Express Settings** o al actualizar desde DirSync, se necesita una cuenta **Enterprise Administrator** para Active Directory local.
* La instalación Custom ofrece opciones adicionales de cuentas y permisos.

---

# Conectividad

El servidor Microsoft Entra Connect Sync necesita resolución DNS tanto para la red interna como para Internet.

* El DNS debe resolver nombres de Active Directory local y endpoints de Microsoft Entra.
* Se necesita conectividad con todos los dominios configurados.
* También se necesita conectividad con el dominio raíz de cada bosque configurado.
* Si existen firewalls internos, deben abrirse los puertos necesarios entre el servidor y los controladores de dominio.
* Si existen restricciones de URLs mediante proxy o firewall, deben permitirse las URLs requeridas por Microsoft 365 y Microsoft Entra.
* Desde Microsoft Entra Connect Sync **1.1.614.0**, TLS 1.2 es el protocolo utilizado por defecto.
* Desde la versión **2.0**, TLS 1.0 y TLS 1.1 ya no son compatibles y TLS 1.2 debe estar habilitado.
* Antes de la versión 1.1.614.0, TLS 1.0 era utilizado por defecto.
* Si se utiliza un proxy saliente, debe configurarse el archivo `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config` para permitir la conexión a Internet y Microsoft Entra ID.

---

# Configuración de Microsoft Entra Connect Sync

La instalación se realiza mediante el programa de configuración más reciente, que inicia el asistente de instalación.

Existen dos modos:

* **Express**
* **Custom**

## Express Setup

Es la opción predeterminada y está orientada al escenario de instalación más común.

Utiliza **Password Hash Synchronization (PHS)** y está orientada a un único bosque.

Ventajas principales:

* Simplicidad y facilidad de uso.
* Configuración basada en prácticas recomendadas.
* Configuración automática de componentes.
* Sincronización de usuarios, contraseñas y otros atributos.
* Integración con características de Microsoft Entra ID.
* Facilita las actualizaciones y mantenimiento futuros.

Durante Express Settings se:

* Instala el motor de sincronización.
* Configura Microsoft Entra Connect Sync.
* Configura el conector de Active Directory local.
* Habilita PHS.
* Configuran los servicios de sincronización.
* Configura opcionalmente la sincronización para Exchange híbrido.
* Habilita la actualización automática.

También se puede elegir iniciar la sincronización al finalizar la instalación.

---

# Custom Setup

Custom permite mayor flexibilidad y control granular.

Se utiliza, entre otros casos, cuando:

* Existen múltiples bosques.
* Se necesita PHS, PTA, SSO o AD FS.
* Se utiliza un proveedor de identidad no Microsoft.
* Se requieren características personalizadas de sincronización, filtrado o writeback.

Permite:

* Especificar una ubicación personalizada de instalación.
* Utilizar un SQL Server existente.
* Utilizar una cuenta de servicio existente.
* Especificar grupos de sincronización personalizados.

Por defecto, Microsoft Entra Connect Sync crea grupos locales para:

* Administradores.
* Operadores.
* Browse.
* Password Reset.

Los grupos personalizados deben ser locales al servidor y no pueden pertenecer al dominio.

## Características disponibles en Custom

| Característica                              | Concepto                                                                                                  | Cuándo utilizarla                                                          |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Método de SSO                               | Permite elegir PHS, PTA, AD FS o no configurar SSO.                                                       | Cuando se desea SSO.                                                       |
| Múltiples directorios o bosques             | Permite conectar varios dominios o bosques de Active Directory.                                           | Cuando existen múltiples bosques.                                          |
| Matching entre bosques                      | Define cómo representar usuarios provenientes de distintos bosques.                                       | Cuando existen múltiples bosques.                                          |
| Filtrado por OU                             | Permite sincronizar únicamente objetos de determinadas OUs.                                               | Para sincronizar elementos específicos o realizar pilotos.                 |
| Source anchor                               | Define la clave primaria, como ImmutableID, que vincula al usuario local con Microsoft Entra ID.          | Cuando se necesita modificar el source anchor.                             |
| Sign-in attribute                           | Define el atributo utilizado para iniciar sesión, normalmente UPN; también puede utilizarse Alternate ID. | Cuando se requiere un atributo de inicio de sesión diferente.              |
| Exchange hybrid deployment                  | Sincroniza atributos necesarios para coexistencia entre Exchange local y Microsoft 365.                   | Cuando existe Exchange local y se planea migrar buzones a Exchange Online. |
| Exchange mail public folders                | Sincroniza public folders habilitados para correo.                                                        | Cuando existen mail-enabled public folders locales.                        |
| Microsoft Entra app and attribute filtering | Permite adaptar los atributos sincronizados según las aplicaciones de Microsoft Entra.                    | Cuando se utilizan Microsoft Entra apps.                                   |
| Password writeback                          | Escribe en Active Directory local los cambios de contraseña originados en Microsoft Entra ID.             | Para escenarios de Self-Service Password Reset.                            |
| Group writeback                             | Permite representar Microsoft 365 Groups en Active Directory local como grupos de distribución.           | Con Exchange híbrido y Microsoft 365 Groups.                               |
| Device writeback                            | Escribe objetos de dispositivos de Microsoft Entra ID en Active Directory local.                          | Para escenarios de Conditional Access.                                     |
| Directory extension attribute sync          | Extiende el esquema de Microsoft Entra ID con atributos personalizados.                                   | Cuando Active Directory local tiene atributos personalizados.              |

---

# SSO, PHS y PTA

Una de las razones principales para utilizar Custom Setup es configurar **Single Sign-On (SSO)**.

Si se habilita SSO:

* Se configuran **PHS + Pass-through Authentication (PTA)**.
* Los usuarios pueden autenticarse utilizando sus credenciales de Active Directory local.
* Se reduce la necesidad de introducir credenciales repetidamente.
* Se simplifica la administración de contraseñas.
* Se mantienen las políticas de contraseñas locales.
* PTA proporciona autenticación en tiempo real contra Active Directory local.
* PHS puede proporcionar continuidad cuando la infraestructura local no está disponible.
* Resulta útil en entornos híbridos.

Si no se habilita SSO:

* Se utiliza **PHS** únicamente.

Las razones para utilizar PHS sin SSO pueden incluir:

* Simplicidad y menor infraestructura.
* Necesidad de mantener la administración de contraseñas en Active Directory local.
* Requisitos de cumplimiento o regulación.
* Infraestructura existente de identidad y acceso.
* Limitaciones de disponibilidad o conectividad de la infraestructura local.

PHS permite sincronizar hashes de contraseñas manteniendo el control de las políticas y restablecimientos de contraseña en Active Directory local.

Si existe una implementación de **AD FS**, puede identificarse durante la instalación. El asistente puede solicitar información como:

* Nombre de la granja AD FS.
* Cuenta de servicio.
* Certificado TLS/SSL.

También se puede iniciar la sincronización al finalizar la instalación y habilitar staging mode.

---

# Microsoft Entra Connect Health

**Microsoft Entra Connect Health** permite supervisar la infraestructura de identidad local y los servicios de sincronización proporcionados por Microsoft Entra Connect Sync.

Permite consultar:

* Alertas.
* Rendimiento.
* Patrones de uso.
* Configuración.

Utiliza un agente instalado en los servidores para mantener información sobre la infraestructura y la conexión con Microsoft 365.

### Componentes

* **Microsoft Entra Connect Health for AD FS**: supervisa el entorno AD FS local.
* **Microsoft Entra Connect Health for Sync**: supervisa las sincronizaciones entre Active Directory local y Microsoft Entra ID.
* También puede supervisar Active Directory Domain Services y el estado de replicación.

### Capacidades de Health for Sync

* Consultar y actuar sobre alertas.
* Recibir notificaciones por correo electrónico para alertas críticas.
* Consultar datos de rendimiento.

Microsoft Entra Connect Health forma parte de **Microsoft Entra Premium** y requiere las licencias correspondientes.

### Portal de Microsoft Entra Connect Health

La primera vez que se accede aparece la página **Quick Start**, desde donde se puede:

* Descargar el agente apropiado.
* Acceder a documentación.
* Enviar comentarios.

Incluye:

* **Microsoft Entra Connect (Sync)**: servidores Microsoft Entra Connect Sync supervisados.
* **Active Directory Federation Services**: servicios AD FS supervisados.
* **Active Directory Domain Services**: bosques de Active Directory supervisados.
* **Configure**: configuración de actualización automática del agente y acceso de Microsoft a los datos de estado para troubleshooting.

La actualización automática permite mantener el agente en la última versión. El acceso de Microsoft a los datos de health para troubleshooting está deshabilitado de forma predeterminada.

---

# Microsoft Entra Cloud Sync

## Prerrequisitos

Antes de instalar Microsoft Entra Cloud Sync se debe:

* Crear el **gMSA (group Managed Service Account)** para ejecutar el servicio del agente.
* Crear una cuenta **Hybrid Identity Administrator** para el tenant.
* Identificar un servidor local para el provisioning agent con **Windows Server 2016 o posterior**.
* El servidor debe tratarse como un servidor **Tier 0**.
* Cloud Sync permite instalar el agente en un controlador de dominio.
* Configurar alta disponibilidad mediante varios agentes activos.
* Microsoft recomienda **tres agentes activos** para alta disponibilidad.
* Completar la configuración del firewall local.

---

# gMSA

Una **gMSA** es una cuenta de dominio administrada que proporciona:

* Administración automática de contraseñas.
* Administración simplificada de SPN.
* Delegación de administración a otros administradores.
* Uso de estas capacidades en múltiples servidores.

Microsoft Entra Cloud Sync utiliza una gMSA para ejecutar el agente ligero.

La cuenta creada durante la configuración aparece como:

`domain\provAgentgMSA$`

### Requisitos para crear la gMSA

1. Actualizar el esquema de Active Directory del bosque a **Windows Server 2012 o posterior**.
2. Instalar los módulos de **PowerShell RSAT** en un controlador de dominio.
3. Contar con al menos un controlador de dominio con Windows Server 2012 o posterior.
4. El servidor donde se instala el agente debe estar unido al dominio y ejecutar **Windows Server 2016 o posterior**.

---

# Hybrid Identity Administrator

Se necesita una cuenta **cloud-only Hybrid Identity Administrator**.

* No puede ser una cuenta guest.
* Se crea en Microsoft Entra admin center.
* Se le asignan permisos Hybrid Identity Administrator.
* Permite administrar el tenant si los servicios locales fallan o dejan de estar disponibles.
* Se deben agregar uno o más dominios personalizados al tenant para que los usuarios puedan iniciar sesión con ellos.

---

# Servidor del provisioning agent

El servidor debe:

* Estar unido al dominio.
* Ejecutar **Windows Server 2016 o posterior**.
* Tener como mínimo **4 GB de RAM**.
* Tener **.NET 4.7.1 o posterior**.
* Tener la política de ejecución de PowerShell configurada como **Undefined** o **RemoteSigned**.

---

# Firewall y proxy de Cloud Sync

Los agentes necesitan realizar solicitudes **salientes** hacia Microsoft Entra ID.

| Puerto | Uso                                                                                       |
| ------ | ----------------------------------------------------------------------------------------- |
| 80     | Descarga de CRL durante la validación de certificados TLS/SSL.                            |
| 443    | Comunicación saliente con el servicio.                                                    |
| 8080   | Opcional; permite informar el estado cada 10 minutos si el puerto 443 no está disponible. |

Si el firewall aplica reglas según el usuario de origen, los puertos deben abrirse para el tráfico de los servicios de Windows que ejecutan como Network Service.

---

# Otras consideraciones de Cloud Sync

### NTLM

No se debe habilitar NTLM en el Windows Server que ejecuta Microsoft Entra Connect Provisioning Agent. Si está habilitado, debe deshabilitarse.

### Delta synchronization

Limitaciones:

* El filtrado por alcance de grupos para delta sync no admite más de **50.000 miembros**.
* Si se elimina un grupo utilizado en un filtro de alcance, sus usuarios miembros no se eliminan.
* Si se cambia el nombre de una OU o grupo incluido en el alcance, delta sync no elimina los usuarios.

### Provisioning logs

Los logs pueden no diferenciar claramente entre operaciones de creación y actualización. Puede aparecer una operación de creación para una actualización y viceversa.

### Renombrado de grupos u OUs

Si se cambia el nombre de un grupo u OU local incluido en una configuración, Cloud Sync no reconoce el cambio de nombre. El job no entra en quarantine y permanece en estado healthy.

### Scoping filter por OU

* Se pueden sincronizar hasta **59 OUs separadas** por configuración.
* Se admiten OUs anidadas.
* Se puede sincronizar una OU que contenga 130 OUs anidadas, pero no 60 OUs separadas dentro de la misma configuración.

---

# Configuración de Microsoft Entra Cloud Sync

Después de cumplir los prerrequisitos se deben realizar cuatro tareas:

1. Instalar el **Microsoft Entra Connect provisioning agent**.
2. Verificar que el agente está instalado.
3. Verificar que el agente está ejecutándose.
4. Configurar el provisioning de Microsoft Entra Cloud Sync.

## 1. Instalar el provisioning agent

El provisioning agent solo es compatible con sistemas operativos **Windows Server**.

Proceso:

1. Iniciar sesión en Microsoft 365 admin center con una cuenta con permisos Global Admin.
2. Seleccionar **Show all → Admin centers → Identity**.
3. En Microsoft Entra admin center, seleccionar **Show more**.
4. Seleccionar **Hybrid management → Microsoft Entra Connect**.
5. En **Microsoft Entra Connect | Get started**, seleccionar **Cloud Sync**.
6. En **Cloud sync | Configurations**, seleccionar **Agents**.
7. Seleccionar **Download on-premises agent**.
8. Seleccionar **Accept terms & download**.
9. Abrir el archivo descargado para iniciar el asistente.
10. Aceptar los términos y seleccionar **Install**.
11. En el asistente de configuración del provisioning agent, seleccionar **Next**.
12. Seleccionar la extensión correspondiente.
13. Iniciar sesión con una cuenta Global Administrator.
14. Si se seleccionó HR-driven provisioning:

    * Crear o especificar una gMSA.
    * Conectar con Active Directory.
    * Agregar dominios adicionales si es necesario.
    * Opcionalmente establecer la prioridad de los controladores de dominio.
15. Confirmar la configuración del agente.
16. Esperar a que finalice la instalación y seleccionar **Exit**.
17. Cerrar el instalador si permanece abierto.

---

## 2. Verificar que el agente está instalado

En **Microsoft Entra admin center → Cloud sync → Agents**:

1. Actualizar la página.
2. Verificar que el agente instalado aparece.
3. Confirmar que su estado es **Active**.

---

## 3. Verificar que el agente está ejecutándose

En el servidor local:

1. Iniciar sesión con una cuenta administrativa.
2. Abrir **Services**.
3. Verificar que estén presentes y en estado **Running**:

   * **Microsoft Azure AD Connect Agent Updater**
   * **Microsoft Azure AD Connect Provisioning Agent**

---

## 4. Configurar el provisioning de Cloud Sync

Después de instalar y verificar el agente:

1. En **Cloud sync | Agents**, seleccionar **Configurations**.
2. Seleccionar **+ New configuration**.
3. Elegir **AD to Microsoft Entra ID sync**.
4. Seleccionar el dominio que se sincronizará y decidir si se habilita Password Hash Sync.
5. Seleccionar **Create**.
6. Configurar la nueva sincronización:

### Scope

Definir si todos los usuarios están dentro del alcance o utilizar filtros para seleccionar usuarios y grupos específicos.

### Manage attributes

Permite mapear atributos entre objetos de usuarios/grupos locales y Microsoft Entra ID.

Se pueden:

* Modificar mappings existentes.
* Eliminar mappings.
* Crear nuevos mappings.

### Validate

Se recomienda utilizar **Provision a user** para comprobar la sincronización antes de habilitar la configuración.

Permite probar la sincronización con usuarios individuales.

### Settings

* Introducir una dirección de **Notification email**.
* Mantener seleccionada la opción **Prevent accidental deletion**.
* Definir el **Accidental deletion threshold** para recibir notificaciones.

### Deploy

Seleccionar **Enable** para sincronizar los usuarios y grupos incluidos en el alcance.

Finalmente, mover el selector a **Enable** y seleccionar **Save**.

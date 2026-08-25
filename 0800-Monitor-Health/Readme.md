# Resumen — Monitor tenant health using Microsoft 365

## Monitoreo de la salud de Microsoft 365

Microsoft 365 incluye herramientas para monitorear la salud de los servicios desde el **Microsoft 365 admin center**. La página **Health** proporciona información sobre el estado de los servicios online y sobre tareas de mantenimiento previstas.

### Health dashboard

El **Health dashboard** ofrece una vista resumida de la salud del entorno Microsoft 365 y permite observar:

* Estado de los servicios.
* Alertas críticas.
* Uso diario promedio de productos.
* Utilización de licencias.
* Recomendaciones para mejorar la salud de la organización.

### Critical alerts

Muestra problemas que requieren atención:

* Incidentes generales de servicio.
* Problemas de facturación, como una tarjeta de crédito próxima a vencer.

Si no existen alertas, aparece un indicador verde.

### Service health and usage

Muestra el estado actual de una selección de aplicaciones y servicios, junto con:

* Uso diario promedio.
* Utilización de licencias.
* Advisories asociados a servicios que no están en estado **Healthy**.

### Estados de Service Health

| Estado                             | Definición                                                                                                                                                                                                           |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Investigating**                  | Microsoft conoce un posible problema y recopila información sobre su alcance e impacto.                                                                                                                              |
| **Service degradation**            | Existe un problema que puede afectar el uso del servicio o una funcionalidad, como lentitud o interrupciones intermitentes.                                                                                          |
| **Service interruption**           | El problema impide a los usuarios acceder al servicio y es significativo y reproducible.                                                                                                                             |
| **Restoring service**              | Se identificó la causa y Microsoft está aplicando la acción correctiva para recuperar el servicio.                                                                                                                   |
| **Extended recovery**              | El servicio fue corregido para la mayoría de los usuarios, pero puede tomar tiempo recuperar todos los sistemas afectados. También puede indicar una solución temporal mientras se espera una corrección permanente. |
| **Investigation suspended**        | Microsoft necesita información adicional de los clientes para continuar investigando.                                                                                                                                |
| **Service restored**               | Microsoft confirmó que la acción correctiva resolvió el problema y el servicio volvió a un estado saludable.                                                                                                         |
| **False positive**                 | Microsoft confirmó que el servicio funciona correctamente y que no hubo impacto o que el origen del incidente era externo.                                                                                           |
| **Post-incident report published** | Microsoft publicó un informe posterior al incidente con la causa raíz y próximos pasos.                                                                                                                              |

### Indicadores visuales

En **Health dashboard** y **Service Health**:

* ✓ indica servicio saludable.
* X indica servicio no disponible.
* ! indica servicio degradado.

### Recommended actions

El Health dashboard puede mostrar recomendaciones como:

* **Activate multifactor authentication**: muestra cuántas cuentas administrativas tienen MFA habilitado y permite acceder al asistente para habilitarlo.
* **Enable monthly updates for Office**: indica si Office está configurado para recibir actualizaciones con la frecuencia recomendada.
* **Share OneDrive training**: permite compartir capacitación sobre OneDrive para fomentar su uso y mejorar la recuperación ante ransomware o fallos del dispositivo.

## Microsoft 365 Service Health

La página **Service Health** muestra todos los servicios y su disponibilidad.

Incluye:

* **Overview**: problemas activos y estado de todos los servicios.
* **Issue History**: historial de incidentes y advisories; permite filtrar la actividad de los últimos siete días.
* **Reported Issues**: problemas reportados por el tenant y su estado.

Si existe un problema que no aparece en Service Health, se puede utilizar **Report an issue** para comunicarlo a Microsoft. Microsoft analiza otros reportes y determina si el problema tiene origen en su servicio.

### Personalización y notificaciones

La vista de Service Health puede personalizarse para mostrar únicamente determinados servicios.

Para recibir notificaciones por email:

1. Ir a **Service health > Issue history**.
2. Seleccionar **Customize**.
3. Abrir la pestaña **Email**.
4. Activar **Send me email notifications about service health**.
5. Configurar:

   * Hasta dos direcciones de email.
   * Incidentes o advisories.
   * Servicios de interés.
6. Seleccionar **Save**.

También se pueden configurar notificaciones para un incidente individual mediante **Manage notifications for this issue**.

El límite de dos direcciones es por cuenta de administrador.

La aplicación móvil **Microsoft 365 Admin** también permite consultar Service Health y recibir notificaciones push.

---

# Microsoft 365 Adoption Score

El **Adoption Score** incluye áreas de **People experiences** y **Technology experiences**.

El benchmark de **Endpoint Analytics** incluye objetivos para el rendimiento de inicio del dispositivo y configuraciones de software recomendadas, basados en valores medianos agregados entre tenants.

Para **Network Connectivity**, el benchmark recomendado es de **80 puntos**.

### Score breakdown

Muestra el desglose del Adoption Score mediante benchmarks para las áreas de experiencia de personas y tecnología.

### Score history

Muestra cómo evolucionó el score de cada categoría durante los últimos seis meses.

### Category details pages

Cada página de categoría muestra:

* Insight principal.
* Métricas de soporte.
* Investigación relacionada.
* Acciones recomendadas.

Categorías:

* Content collaboration.
* Communication.
* Meetings.
* Mobility.
* Teamwork.
* Microsoft 365 Apps health.
* Endpoint Analytics.

### Business resilience report

El **Business resilience report** es un informe temporal que ayuda a comprender:

* Cómo el trabajo remoto afecta la colaboración y comunicación.
* Cómo afecta al equilibrio entre vida laboral y personal.
* Cómo las reuniones remotas afectan la toma de decisiones.

Los usuarios también pueden consultar insights de productividad desde **MyAnalytics**.

### Group level aggregates

Permiten analizar el rendimiento de distintos grupos utilizando información de **Microsoft Entra ID**.

Sirven para:

* Comparar la adopción entre diferentes grupos.
* Identificar grupos con buen desempeño y grupos que necesitan mejorar.
* Analizar un grupo específico de forma aislada.

### Organizational messages

Permiten a los administradores enviar mensajes para fomentar la adopción de funcionalidades.

Actualmente permiten impulsar escenarios de adopción relacionados con:

* OneDrive.
* SharePoint.
* Teams Chat.
* @mentions en Outlook.
* Cloud attachments en Outlook.

---

# Microsoft 365 Usage Analytics

Microsoft 365 Usage Analytics permite:

* Visualizar y analizar datos de uso de Microsoft 365.
* Crear reportes personalizados.
* Compartir insights dentro de la organización.
* Analizar cómo regiones o departamentos específicos utilizan Microsoft 365. 

Proporciona un dashboard predefinido con una visión cross-product de los últimos **12 meses**. La información específica de usuarios está disponible para el último mes calendario completo.

Los datos están disponibles en los **Activity reports** del Microsoft 365 admin center y opcionalmente en la aplicación de plantilla de **Power BI**.

La aplicación de Power BI requiere **Power BI Pro**. Los datos subyacentes coinciden con los Activity reports, pero:

* Admin center: datos de los últimos 7, 30, 90 o 180 días.
* Power BI: datos mensuales de hasta 12 meses.
* Power BI: detalles a nivel de usuario únicamente del último mes completo, para usuarios licenciados que realizaron actividad. 

La aplicación de Power BI combina los datos de uso de Microsoft 365 con información de Active Directory, permitiendo analizar los datos por propiedades como departamentos y ubicación, crear reportes personalizados y compartir insights.

Al conectarse por primera vez, carga automáticamente los datos de los últimos 12 meses. Después, los datos se actualizan semanalmente.

El servicio backend de Microsoft 365 actualiza los datos diariamente, con una latencia de **5 a 8 días**.

### Habilitar Microsoft 365 Usage Analytics

Se requiere el rol **Global administrator**.

1. Ir a **Microsoft 365 admin center > Reports > Usage**.
2. Buscar **Microsoft 365 usage analytics** y seleccionar **Get started**.
3. Activar **Make organizational usage data available to Microsoft 365 usage analytics for Power BI**.
4. Seleccionar **Save**.
5. Actualizar la página.

Aparecerá un mensaje indicando que Microsoft está recopilando datos y que puede tardar hasta **48 horas**.

Una vez finalizada la recopilación, aparece **Go to Power BI**. 

### Iniciar la aplicación de Power BI

Para utilizar la aplicación se necesita **Power BI Pro** y uno de estos roles:

* Global Administrator.
* Report Reader.
* Exchange Administrator.
* Skype for Business Administrator.
* SharePoint Administrator.

Proceso:

1. Ir a **Reports > Usage**.
2. Copiar el tenant ID y seleccionar **Go to Power BI**.
3. En Power BI seleccionar **Apps**.
4. Seleccionar **Get apps**.
5. Buscar **Microsoft 365**.
6. Seleccionar **Microsoft 365 Usage Analytics**.
7. Seleccionar **Get It Now**.
8. Confirmar con **Get it now**.
9. Seleccionar **Install**.
10. Abrir la aplicación instalada.
11. Seleccionar **Connect your data**.
12. Introducir el tenant ID sin guiones.
13. Mantener activado **Automatically refresh my data daily** y seleccionar **Next**.
14. Seleccionar **OAuth2** y **Sign in and connect**.
15. Esperar a que se carguen los datos.

La carga inicial del dashboard puede tardar entre **2 y 30 minutos**.

Los agregados a nivel de tenant están disponibles después del opt-in. Los detalles a nivel de usuario aparecen aproximadamente el quinto día del mes calendario siguiente. 

### Reportes principales de Power BI

**Executive Summary**

Ofrece una vista general de:

* Adopción.
* Uso.
* Movilidad.
* Comunicación.
* Colaboración.
* Almacenamiento.

Los valores corresponden al último mes completo.

**Microsoft 365 Overview**

Incluye:

* **Adoption**: tendencias de adopción, usuarios habilitados, usuarios activos, usuarios recurrentes y usuarios que utilizan el producto por primera vez.
* **Usage**: volumen de usuarios activos y actividades principales por producto durante los últimos 12 meses.
* **Communication**: uso de Teams, Yammer, email y llamadas de Skype.
* **Collaboration**: uso de OneDrive y SharePoint, colaboración y documentos compartidos.
* **Storage**: almacenamiento de mailboxes, OneDrive y SharePoint.
* **Mobility**: clientes y dispositivos utilizados para conectarse a email, Teams, Skype o Yammer. 

**Activation and Licensing**

* **Activation**: activaciones de planes de servicio y dispositivos donde se instalaron aplicaciones de Office.
* **Licensing**: tipos de licencia, usuarios asignados y distribución mensual de licencias.

Un usuario con licencia de Office puede instalar productos en hasta **cinco dispositivos**. Para considerar un plan activado, el usuario debe instalar la aplicación e iniciar sesión. 

**Product usage**

Incluye reportes individuales para:

* Exchange.
* Microsoft 365 Groups.
* OneDrive.
* SharePoint.
* Skype.
* Teams.
* Yammer.

Muestra usuarios habilitados frente a usuarios activos, entidades como mailboxes, sitios, grupos y cuentas, y actividades correspondientes. 

**User activity**

Proporciona información detallada de uso a nivel de usuario combinada con atributos de Active Directory.

El reporte **Department Adoption** permite segmentar usuarios activos mediante atributos de Active Directory.

Los roles **Global Reader** y **Usage Summary Reports Reader** no tienen permisos para visualizar los reportes de actividad de usuarios. 

### Información identificable de usuarios

Los reportes pueden contener nombres identificables de usuarios, grupos y sitios.

Desde el **1 de septiembre de 2021**, Microsoft oculta esta información de forma predeterminada.

Los Global Administrators pueden permitir nuevamente la visualización:

1. **Microsoft 365 admin center > Settings > Org Settings**.
2. Seleccionar **Services > Reports**.
3. Desactivar **Display concealed user, group, and site names in all reports**.
4. Seleccionar **Save**.

La configuración aplica a los reportes de uso de Microsoft 365 en:

* Microsoft 365 admin center.
* Microsoft Graph.
* Power BI.
* Microsoft Teams admin center.

Mostrar información identificable queda registrado como evento en el audit log del portal de Microsoft Purview. 

---

# Microsoft 365 Network Connectivity Assessments and Insights

Microsoft recopila métricas agregadas de conectividad de red provenientes de clientes de Office desktop y web. Estas métricas permiten obtener:

* Insights de arquitectura de red.
* Recomendaciones de rendimiento.
* Network assessments.

Se encuentran en **Health > Network connectivity** del Microsoft 365 admin center. 

Los insights ayudan a diseñar los perímetros de red de las oficinas. Las recomendaciones indican cambios específicos de arquitectura para mejorar la experiencia de Microsoft 365.

Los network assessments muestran cómo la conectividad afecta la experiencia de usuario y permiten comparar conexiones de diferentes ubicaciones.

## Requisitos para Network Connectivity Assessments

Para obtener los datos se debe configurar la información de las ubicaciones.

Opciones:

1. Activar la recopilación automática mediante **Windows Location Services**.
2. Agregar o cargar manualmente las ubicaciones.
3. Ejecutar el **Microsoft 365 network connectivity test** desde las oficinas. 

### Opción 1 — Windows Location Services

Requisitos:

* Al menos dos computadoras por ubicación.
* OneDrive para Windows actualizado e instalado.
* Windows Location Services habilitado.
* Consentimiento para acceder a la ubicación.
* Preferentemente Wi-Fi; Ethernet no proporciona información de ubicación precisa.

Las pruebas se ejecutan como máximo una vez al día en un momento aleatorio.

Las ubicaciones se identifican automáticamente con resolución de ciudad. No se muestran múltiples oficinas dentro de una misma ciudad.

La ubicación se redondea a un área de **300 × 300 metros**.

La función está desactivada por defecto y debe habilitarse en **Network Connectivity Settings**.

Los primeros datos pueden aparecer después de **24 horas**. Las ubicaciones descubiertas se conservan durante **90 días** después de dejar de recibir muestras. 

### Opción 2 — Agregar ubicaciones manualmente

No requiere Windows Location Services ni Wi-Fi.

Requiere:

* OneDrive para Windows actualizado.
* Al menos un equipo en la ubicación.
* Información de LAN subnet.

Las ubicaciones pueden:

* Agregarse manualmente.
* Importarse mediante CSV.
* Cargarse desde otras fuentes.

Permite definir múltiples oficinas en una ciudad y asignarles nombres.

Las LAN subnets son obligatorias. También pueden configurarse múltiples LAN subnets y public egress IP subnets.

Las LAN subnets normalmente son rangos privados definidos por **RFC1918**.

Las public egress IP se utilizan como diferenciador secundario cuando varias oficinas utilizan el mismo rango LAN. Si se configuran, el resultado debe coincidir tanto con la LAN subnet como con la public egress IP.

Los datos pueden comenzar a aparecer después de **24 horas**. 

### Opción 3 — Microsoft 365 network connectivity test

Desde un equipo Windows de cada ubicación:

1. Acceder al **Microsoft 365 network connectivity test**.
2. Iniciar sesión con una cuenta Microsoft 365 de la organización.
3. Seleccionar **Run test**.
4. Ejecutar el archivo Connectivity Test EXE descargado.
5. Esperar a que finalicen las pruebas.

Los resultados se cargan en el Microsoft 365 admin center.

Si la ubicación fue configurada con LAN subnet, el reporte queda asociado a ella; de lo contrario, aparece en la ubicación de ciudad descubierta.

Los resultados pueden comenzar a aparecer **2-3 minutos** después de completar la prueba. 

Actualmente, las LAN subnets y egress IP utilizadas para agregar ubicaciones deben ser **IPv4**. 

## Network Connectivity en el admin center

La información aproximada de ubicación identifica la ciudad de los dispositivos.

El **Overview** muestra un network assessment ponderado para todo el tenant.

En **Locations** se pueden consultar métricas e incidentes específicos por ubicación y, cuando corresponde, una estimación de la mejora potencial de latencia.

El acceso requiere ser administrador.

* **Report Reader**: acceso de lectura.
* **Service Support Administrator**: puede configurar ubicaciones y otros elementos de Network Connectivity.

Network Connectivity en Admin Center soporta tenants **WW Commercial**, pero no GCC Moderate, GCC High, DoD ni China. 

## Network assessments

Los network assessments condensan múltiples métricas de rendimiento en un valor de **0 a 100**.

Existen evaluaciones:

* Para todo el tenant.
* Para cada ubicación geográfica.

Son especialmente útiles para empresas complejas con múltiples oficinas y arquitecturas de perímetro de red no simples. Las empresas con más de **500 usuarios y múltiples oficinas** son las que más probablemente se beneficien. 

Las configuraciones de perímetro diseñadas principalmente para navegación web pueden degradar el rendimiento de Microsoft 365 debido a mecanismos de seguridad, proxies y otros intermediarios.

Microsoft recomienda utilizar los **Office 365 connectivity principles** y la funcionalidad Network Connectivity del admin center para mejorar latencia, confiabilidad y rendimiento. 

## Microsoft 365 Network Insights

Los Network Insights son métricas de rendimiento recopiladas del tenant. Solo son accesibles para administradores.

Ayudan a diseñar los perímetros de red y muestran información de rendimiento para problemas comunes en cada ubicación geográfica. 

### Principales Network Insights

* **Backhauled network egress**: detecta cuando la distancia entre la ubicación del usuario y el network egress supera **500 millas / 800 km**. Microsoft recomienda que el egress esté lo más cerca posible de la oficina.
* **Network intermediary device**: detecta dispositivos intermedios como proxies, VPN o dispositivos DLP. Microsoft recomienda evitar estos dispositivos para tráfico de Microsoft 365 sensible a la latencia.
* **Better performance detected for customers near you**: aparece cuando la latencia promedio de los usuarios es al menos **10 % mayor** que la de tenants cercanos de la misma ciudad.
* **Use of a non-optimal Exchange Online service front door**: detecta conexiones a un front door de Exchange Online no óptimo y puede recomendar egress local y directo.
* **Use of a non-optimal SharePoint Online service front door**: detecta conexiones a un front door de SharePoint Online que no es el más cercano.
* **Low download speed from SharePoint front door**: aparece cuando el ancho de banda entre la ubicación y SharePoint Online es inferior a **1 MBps**.
* **China user optimal network egress**: para usuarios de China, Microsoft recomienda egress hacia Hong Kong, Japón, Taiwán, Corea del Sur, Singapur o Malasia cuando se utiliza conectividad WAN privada. 

La recomendación general es mantener el **network egress lo más cerca posible de las oficinas** para mejorar el rendimiento y reducir la latencia. 

---

# Microsoft 365 Backup (Preview)

**Microsoft 365 Backup** es un servicio de consumo **pay-as-you-go** destinado a continuidad del negocio mediante capacidades de backup y restauración.

Está disponible mundialmente en todos los entornos comerciales.

Su objetivo es permitir recuperar rápidamente grandes cantidades de datos ante:

* Ransomware.
* Eliminación accidental.
* Eliminación maliciosa.
* Sobrescritura accidental o maliciosa.

### Beneficios

* Backup rápido en horas.
* Restauración rápida en horas.
* Restauración completa de sitios de SharePoint y cuentas de OneDrive a un estado anterior mediante rollback.
* En el futuro, restauraciones granulares de archivos en OneDrive y SharePoint.
* Restauración completa o granular de elementos de Exchange mediante búsqueda.
* Administración consolidada de seguridad y compliance.

Microsoft también trabaja con ISV que pueden ofrecer aplicaciones integradas con **Microsoft 365 Backup Storage**. En estas aplicaciones, la operación y el pago pueden gestionarse completamente desde la aplicación del partner.

## Pricing

Microsoft 365 Backup utiliza un modelo **pay-as-you-go**.

Precio de lista:

**$0.15/GB/mes de contenido protegido.**

El tamaño facturado considera:

* Tamaño acumulado de mailboxes, SharePoint sites y OneDrive accounts protegidos.
* Contenido eliminado de Recycle Bin y Second-stage Recycle Bin.
* Mailboxes: mailbox + online archives + deleted items retenidos para Backup.

Microsoft no cobra por:

* Restore points.
* Tamaño de las restauraciones.
* Costos adicionales de Azure API o almacenamiento asociados al servicio.

El cargo cubre **365 días** desde que los datos se incorporan a la protección.

El contenido eliminado continúa afectando el tamaño facturado mientras permanezca retenido por Backup durante ese período.

El pricing calculator estima almacenamiento y costos utilizando datos actuales y tendencias históricas, con una proyección de hasta **24 meses**.

Considera:

* Cantidad de almacenamiento agregado o eliminado mensualmente.
* Nuevas protection units agregadas o eliminadas.
* Mayor cantidad de almacenamiento requerida durante los últimos 12 meses.

## Arquitectura

Microsoft 365 Backup proporciona recuperación rápida para escenarios BCDR.

OneDrive, SharePoint y Exchange Online ya mantienen copias replicadas en datacenters geográficamente separados para proteger contra desastres físicos.

Los backups:

* No abandonan el límite de confianza de Microsoft 365 ni la ubicación geográfica de residencia de datos.
* Son inmutables, salvo eliminación explícita mediante offboarding.
* Utilizan múltiples copias físicamente redundantes.

OneDrive, SharePoint y Exchange utilizan almacenamiento **Append-Only** para proteger las copias frente a sobrescrituras maliciosas.

## Backup policy performance

Al crear una protection policy para SharePoint, OneDrive y Exchange:

* La activación tarda en promedio hasta **60 minutos**.
* La creación de restore points requiere otros **60 minutos** aproximadamente.

Los restore points se crean físicamente cuando la política queda activada, aunque pueden tardar más en aparecer en la herramienta de restauración.

## Restoration performance

Para restaurar OneDrive y SharePoint:

* El **in-place restore** es más rápido que restaurar hacia una nueva URL.
* Los restore points recomendados como **faster** proporcionan los mejores tiempos de recuperación.

El primer protection unit de un nuevo restore session tarda en promedio menos de **una hora**.

Para un tenant con:

* **1.000 cuentas, sitios o mailboxes**
* **30 GB de tamaño promedio**

se espera completar la restauración de todas las protection units en **menos de 12 horas**.

Una **protection unit** es una cuenta de OneDrive, un sitio de SharePoint o un mailbox de Exchange.

---

# Incident Response Plan

Microsoft 365 es un entorno **Managed Evergreen**, que cambia y se actualiza continuamente. Estos cambios pueden generar incidentes como interrupciones o degradaciones de servicios.

El Microsoft 365 Administrator debe monitorear los incidentes y desarrollar un plan de mitigación.

Un mismo servicio puede presentar diferentes estados según la ubicación del tenant.

## Pasos para desarrollar un Incident Response Plan

1. **Validar el incidente y confirmar que el entorno está afectado**
   No todos los incidentes afectan a todos los tenants. Se pueden utilizar self-assessments para confirmar el impacto y evitar falsos positivos.

2. **Determinar si el incidente es relevante para la empresa**
   Analizar si el servicio afectado impacta las operaciones diarias, colaborando con administradores especializados.

3. **Revisar los tiempos estimados de recuperación**
   Determinar si Microsoft estableció un timeframe para recuperar el servicio. Si no existe, se puede abrir un service request incluyendo el número del incidente.

4. **Desarrollar una solución alternativa**
   Preparar una alternativa para continuar trabajando si la degradación dura más de lo aceptable, ya sea utilizando servicios cloud alternativos o sistemas locales confiables.

Los administradores deben revisar continuamente **Service Health** y utilizar service requests cuando sea necesario.

---

# Request assistance from Microsoft

Microsoft Support proporciona soporte global para:

* Técnico.
* Presales.
* Billing.
* Subscription.

Está disponible para suscripciones Microsoft 365 Enterprise, Business, Education y Government, tanto online desde el portal como por teléfono para suscripciones pagas y trial.

## Technical support

Incluye asistencia para instalación, configuración y uso técnico general.

### Installation and setup

Ejemplos:

**Exchange Online**

* Migración de mailboxes.
* Configuración de destinatarios.
* Permisos.
* Mail forwarding.
* Shared mailboxes.
* Autodiscover.

**SharePoint Online**

* Permisos y grupos.
* Configuración de usuarios externos.

**Skype for Business Online**

* Instalación.
* Creación de contactos.

**Microsoft 365 Apps for enterprise**

* Instalación y configuración.

### Configuration

Incluye:

* Provisioning.
* Configuración y redelegación de dominios.
* Single sign-on (SSO).
* Active Directory synchronization.
* Problemas de configuración de servicios.

## Severity levels

| Severidad                    | Descripción                                                                                                                                                                                         |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Severity A — Critical**    | Uno o más servicios no están disponibles o son inutilizables. Puede existir un impacto grave sobre producción, operaciones, deadlines o rentabilidad. Puede afectar múltiples usuarios o servicios. |
| **Severity B — High**        | El servicio funciona pero está afectado. Existe impacto empresarial moderado y puede tratarse durante el horario laboral. Puede afectar parcialmente a un usuario, cliente o servicio.              |
| **Severity C — Noncritical** | Impacto empresarial mínimo. El problema es importante pero no genera un impacto significativo sobre el servicio o productividad. Puede existir un workaround aceptable.                             |

### Administrator role and responsibilities

Solo los usuarios con roles administrativos de Microsoft 365 pueden acceder al Microsoft 365 admin center y comunicarse directamente con Microsoft para service requests.

El administrador:

* Administra los servicios y mantiene las cuentas.
* Es el contacto principal para configurar y dar soporte a los usuarios.
* Está autorizado a enviar service requests.
* Configura cuentas y acceso.
* Atiende problemas de conectividad, software cliente y movilidad.
* Atiende problemas de disponibilidad dentro del control de la organización.
* Utiliza recursos de self-service para resolver problemas.

### Microsoft Support

Microsoft Support:

* Troubleshootea y proporciona orientación técnica.
* Recopila y valida información.
* Coordina y gestiona la resolución.
* Mantiene comunicación con los administradores.
* Ayuda con licencias, facturación, suscripciones, compras y trials.
* Recopila feedback de clientes.

## Crear un Service Request

1. En el Microsoft 365 admin center seleccionar **Show all**.
2. Seleccionar **Support**.
3. Seleccionar **New service request**.
4. Completar los campos requeridos y describir detalladamente el problema.
5. Seleccionar **Submit**.

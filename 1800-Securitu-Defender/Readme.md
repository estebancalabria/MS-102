# Soluciones de seguridad de Microsoft 365 Defender

## Introducción

Los atacantes pueden utilizar distintos vectores de amenaza para acceder a una organización y avanzar por diferentes etapas de la cadena de ataque después de comprometer un usuario o equipo.

Las funcionalidades analizadas ayudan a:

* Proteger la organización contra ciberamenazas.
* Detectar usuarios o equipos comprometidos.
* Supervisar actividades sospechosas.

Estas capacidades forman parte de **Microsoft Defender XDR (Extended Detection and Response)**:

* Microsoft Defender for Office 365
* Microsoft Defender for Identity
* Microsoft Defender for Endpoint
* Microsoft Defender for Cloud Apps

> **Nota:** Microsoft 365 Defender ahora se denomina Microsoft Defender XDR.

También se introduce **Microsoft 365 Threat Intelligence**.

La mayoría de las capacidades de Microsoft Defender for Office 365, Threat Intelligence, Advanced Security Management y Alert requieren **Microsoft 365 E5**.

---

# Exchange Online Protection (EOP)

**Exchange Online Protection (EOP)** proporciona protección de correo electrónico contra spoofing, phishing, spam y malware mediante:

* Reputación de IP y URL.
* Reputación de dominio.
* Filtrado de spam.
* Filtrado de malware.
* Filtrado de contenido.
* Filtrado de conexiones.
* Spoof intelligence.

EOP está incluido en las organizaciones de Microsoft 365 que utilizan buzones de Exchange Online. También puede utilizarse como producto independiente para proteger buzones locales y entornos híbridos.

## Proceso de protección de EOP

1. **Connection filtering:** comprueba la reputación del remitente y bloquea gran parte del spam.
2. **Malware filtering:** detecta malware en mensajes o archivos adjuntos y los envía a cuarentena.
3. **Policy filtering:** evalúa las reglas de flujo de correo configuradas.
4. **Microsoft Purview DLP:** en determinadas organizaciones locales, realiza comprobaciones de prevención de pérdida de datos.
5. **Content filtering:** identifica:

   * Spam.
   * Spam de alta confianza.
   * Phishing.
   * Phishing de alta confianza.
   * Bulk.
   * Spoofing.
6. **Acciones:** según el resultado del filtrado, el mensaje puede ponerse en cuarentena, moverse a Junk Email u otra acción configurada.

Los mensajes que superan todas las capas de protección se entregan a los destinatarios.

---

# Microsoft Defender for Office 365

Microsoft Defender for Office 365 extiende la protección de EOP frente a amenazas avanzadas como:

* Malware de día cero.
* Determinados ataques de phishing.
* URL maliciosas en correos y documentos.

Las políticas determinan el comportamiento y nivel de protección para las amenazas y pueden configurarse con distintos niveles de granularidad.

## Características principales

### Safe Attachments

Analiza archivos adjuntos sospechosos o desconocidos en un entorno de hypervisor para detectar actividad maliciosa, incluso antes de que existan firmas antivirus.

### Safe Links

Proporciona protección en el momento de hacer clic, evitando que los usuarios accedan a sitios web maliciosos o campañas de phishing desde enlaces en correos y documentos.

### Spoof intelligence

Detecta remitentes que aparentan enviar mensajes en nombre de cuentas de los dominios de la organización. Permite revisar esos remitentes y decidir si permitirlos o bloquearlos.

### Quarantine

EOP puede enviar a cuarentena mensajes identificados como:

* Spam.
* Bulk mail.
* Phishing.
* Malware.
* Coincidentes con una regla de flujo de correo.

Los usuarios autorizados pueden revisar, eliminar o administrar los mensajes en cuarentena.

### Anti-phishing policies

Utilizan modelos de machine learning y algoritmos de detección de suplantación para proteger contra:

* Phishing común.
* Spear phishing.
* Suplantación de usuarios.
* Suplantación de dominios.

---

## Defender for Office 365 Plan 1 y Plan 2

### Plan 1

Incluye capacidades de configuración, protección y detección:

* Safe Attachments.
* Safe Links.
* Safe Attachments para SharePoint, OneDrive y Microsoft Teams.
* Protección anti-phishing.
* Detecciones en tiempo real.

### Plan 2

Incluye todo lo de Plan 1 y agrega capacidades de:

* Automatización.
* Investigación.
* Remediación.
* Educación.
* Threat Trackers.
* Threat Explorer.
* Automated Investigation and Response.
* Attack Simulation Training.
* Advanced Hunting en Microsoft Defender XDR.
* Investigación de incidentes y alertas en Microsoft Defender XDR.

## Investigación y respuesta

* **Threat Trackers:** proporciona inteligencia sobre problemas de ciberseguridad actuales, malware y amenazas.
* **Threat Explorer:** permite analizar amenazas recientes mediante informes en tiempo real y períodos personalizados.
* **Attack Simulation Training:** permite ejecutar escenarios de ataque realistas para identificar vulnerabilidades, incluyendo phishing, ataques con archivos adjuntos, password spray y fuerza bruta.

---

# Microsoft Defender for Identity

Microsoft Defender for Identity es una solución de seguridad basada en la nube que utiliza señales de **Active Directory local** para identificar, detectar e investigar:

* Amenazas avanzadas.
* Identidades comprometidas.
* Acciones maliciosas de insiders.

Permite:

* Monitorizar usuarios, entidades y actividades mediante análisis basado en aprendizaje.
* Proteger identidades y credenciales almacenadas en Active Directory.
* Identificar e investigar actividades sospechosas y ataques avanzados durante toda la cadena de ataque.
* Mostrar información de incidentes mediante una línea temporal.

## Monitorización del comportamiento

Defender for Identity analiza las actividades de los usuarios y crea una **línea base de comportamiento** para cada usuario. Estas líneas base permiten identificar anomalías mediante inteligencia adaptativa.

También utiliza sensores que monitorizan los controladores de dominio y proporcionan una visión de las actividades de los usuarios desde los distintos dispositivos.

## Protección de identidades y reducción de superficie de ataque

Proporciona información sobre configuraciones de identidad, recomendaciones de seguridad, informes y análisis de perfiles.

Sus **Lateral Movement Paths** permiten visualizar cómo un atacante podría desplazarse lateralmente para comprometer cuentas sensibles.

También identifica:

* Usuarios y dispositivos que utilizan contraseñas en texto claro.
* Riesgos relacionados con las configuraciones de identidad.
* Ataques contra Active Directory Federation Services (AD FS).
* Eventos de autenticación generados por AD FS.

## Detección durante la cadena de ataque

Defender for Identity identifica amenazas en diferentes etapas:

* **Reconnaissance:** identifica usuarios sospechosos y actividades destinadas a obtener información sobre usuarios, grupos, IP, dispositivos y recursos.
* **Compromised credentials:** detecta intentos de comprometer credenciales mediante fuerza bruta, autenticaciones fallidas y cambios en grupos.
* **Lateral movements:** detecta técnicas como Pass the Ticket, Pass the Hash y Overpass the Hash.
* **Domain dominance:** identifica comportamientos asociados con el dominio comprometido, incluyendo:

  * Ejecución remota de código en el controlador de dominio.
  * DC Shadow.
  * Replicación maliciosa del controlador de dominio.
  * Golden Ticket.

## Investigación

Reduce el ruido de alertas y presenta alertas relevantes en una **attack timeline** en tiempo real.

Permite investigar amenazas y obtener información sobre:

* Usuarios.
* Dispositivos.
* Recursos de red.

La integración con Microsoft Defender for Endpoint agrega detección y protección adicional frente a amenazas persistentes avanzadas.

---

# Microsoft Defender for Endpoint

Microsoft Defender for Endpoint es una plataforma de seguridad de endpoints para:

* Prevenir amenazas.
* Detectarlas.
* Investigarlas.
* Responder ante ellas.

Utiliza:

### Endpoint behavioral sensors

Sensores integrados en Windows 10 y 11 que recopilan señales de comportamiento del sistema operativo y las envían al servicio cloud de Microsoft Defender for Endpoint.

### Cloud security analytics

Analiza grandes volúmenes de datos y señales del ecosistema Windows, Microsoft 365, Azure y otros recursos para generar:

* Insights.
* Detecciones.
* Respuestas recomendadas.

### Threat intelligence

Permite identificar herramientas, técnicas y procedimientos utilizados por atacantes y generar alertas a partir de los datos recopilados.

---

# Threat and Vulnerability Management

Permite identificar, evaluar y remediar vulnerabilidades de los endpoints para reducir la exposición y fortalecer su seguridad.

Detecta vulnerabilidades y configuraciones incorrectas en tiempo real mediante sensores y las clasifica según:

* Panorama de amenazas.
* Detecciones existentes en la organización.
* Información sensible presente en los dispositivos vulnerables.
* Contexto empresarial.

---

# Attack Surface Reduction

Reduce la superficie de ataque mediante configuraciones y técnicas destinadas a resistir ataques y explotación.

Incluye:

* **Attack surface reduction:** reduce vulnerabilidades mediante reglas inteligentes que ayudan a detener malware.
* **Hardware-based isolation:** protege la integridad del sistema y utiliza aislamiento mediante contenedores para Microsoft Edge.
* **Application control:** permite ejecutar aplicaciones que hayan obtenido confianza.
* **Exploit protection:** protege sistemas operativos y aplicaciones frente a explotación.
* **Network protection:** extiende la protección al tráfico y conectividad de red.
* **Web protection:** protege dispositivos contra amenazas web y permite regular contenido no deseado.
* **Controlled folder access:** evita que aplicaciones maliciosas o sospechosas modifiquen archivos en carpetas importantes.
* **Network firewall:** evita tráfico no autorizado hacia o desde los dispositivos mediante filtrado bidireccional.

---

# Microsoft Defender Antivirus

La protección de nueva generación combina:

* Machine learning.
* Big-data analysis.
* Investigación de resistencia frente a amenazas.
* Infraestructura cloud de Microsoft.

Incluye:

* **Protección antivirus basada en comportamiento, heurística y tiempo real:** monitorización continua del comportamiento de archivos y procesos y bloqueo de aplicaciones inseguras.
* **Cloud-delivered protection:** detección y bloqueo casi instantáneo de amenazas nuevas y emergentes.
* **Actualizaciones de protección y producto:** mantienen Microsoft Defender Antivirus actualizado.

---

# Endpoint Detection and Response (EDR)

Detecta, investiga y responde ante amenazas avanzadas que superan las primeras capas de seguridad.

**Advanced Hunting** proporciona una herramienta basada en consultas para:

* Buscar amenazas de forma proactiva.
* Detectar brechas.
* Crear detecciones personalizadas.

Las capacidades EDR proporcionan detecciones casi en tiempo real y permiten:

* Priorizar alertas.
* Obtener visibilidad del alcance de una brecha.
* Ejecutar acciones de respuesta.
* Remediar amenazas.

Las alertas relacionadas con las mismas técnicas de ataque o con el mismo atacante se agrupan en **incidentes**, facilitando su investigación conjunta.

---

# Automated Investigation and Remediation (AIR)

Defender for Endpoint puede automatizar la investigación y remediación de ataques avanzados.

AIR:

* Reduce el volumen de alertas.
* Analiza alertas mediante algoritmos de inspección.
* Ejecuta acciones inmediatas para resolver brechas.
* Permite que los equipos de seguridad se concentren en amenazas más complejas.

El **Action Center** registra las acciones de remediación pendientes y completadas. Los administradores pueden aprobar, rechazar o deshacer acciones.

---

# Microsoft Secure Score for Devices

Permite:

* Evaluar dinámicamente el estado de seguridad de la red empresarial.
* Identificar sistemas sin protección.
* Aplicar acciones recomendadas para mejorar la seguridad.

El score refleja la configuración de seguridad de los dispositivos en:

* Aplicaciones.
* Sistema operativo.
* Red.
* Cuentas.
* Controles de seguridad.

Un score más alto indica endpoints más resistentes frente a ataques.

---

# Microsoft Threat Experts

Es un servicio de **managed threat hunting** que proporciona monitorización y análisis especializado para los SOC.

Incluye:

* **Targeted attack notifications.**
* **Acceso a expertos bajo demanda.**

Realiza hunting proactivo de:

* Intrusiones de adversarios humanos.
* Hands-on-keyboard attacks.
* Ataques avanzados, como ciberespionaje.

Capacidades principales:

* **Threat monitoring and analysis:** reduce el tiempo de permanencia de los atacantes y el riesgo empresarial.
* **Hunter-trained AI:** descubre y clasifica ataques conocidos y desconocidos.
* **Risk identification:** identifica los riesgos más importantes.
* **Scope of compromise:** proporciona contexto para responder rápidamente.

Los expertos pueden ayudar con:

* Consultas sobre alertas.
* Dispositivos potencialmente comprometidos.
* Causa raíz de conexiones de red sospechosas.
* Inteligencia adicional sobre campañas de amenazas persistentes avanzadas.

---

# Microsoft 365 Threat Intelligence

Es un servicio cloud que proporciona visibilidad sobre el panorama de amenazas, información accionable y capacidades de defensa proactiva.

Permite conocer:

* Cómo se manifiestan las amenazas.
* A quiénes afectan.
* Qué tipos de amenazas existen.
* Con qué frecuencia ocurren.

Está disponible con **Microsoft 365 Enterprise E5** y puede adquirirse como complemento para otras suscripciones Microsoft 365 Enterprise.

Se integra con capacidades como EOP y Microsoft Defender for Office 365 y utiliza señales del **Microsoft Intelligent Security Graph**.

## Capacidades

Permite:

* Monitorizar y responder a amenazas graves en tiempo real.
* Proteger datos y reducir riesgos.
* Detectar ataques avanzados antes de que alcancen la organización.
* Obtener información de la presencia global de Microsoft.
* Recibir recomendaciones dinámicas de políticas.
* Actuar sobre malware en tiempo real.
* Identificar usuarios más atacados.
* Utilizar dashboards desde tendencias globales hasta puntos de inicio para investigaciones.

También proporciona información sobre:

* Amenazas avanzadas.
* Malware.
* Phishing.
* Otros ataques.
* Amenazas bloqueadas o detenidas dentro del ecosistema Microsoft 365.

Muestra métricas como:

* Amenazas detectadas por día.
* Mensajes analizados.
* Amenazas detenidas, bloqueadas o eliminadas.

Integra datos de especialistas de seguridad de Microsoft que buscan amenazas avanzadas.

## Threat Dashboard

Proporciona visibilidad global sobre el panorama de amenazas y ayuda a determinar:

* Origen de las amenazas.
* Posibles actores.
* Tipos de amenazas.
* Cómo remediarlas.
* Estrategias frente a amenazas futuras.

## Threat Explorer

Proporciona informes y vistas gráficas del panorama de amenazas del tenant.

Permite obtener:

* Insights accionables.
* Recomendaciones sobre políticas y enforcement.
* Información sobre familias de malware.
* Información sobre amenazas globales.
* Usuarios más atacados.

### Investigación de malware con Threat Explorer

Permite:

* Analizar el historial de una amenaza.
* Filtrar por remitente, destinatario, IP del remitente y tecnología de detección.
* Determinar si una amenaza fue bloqueada por Defender for Office 365 o EOP.
* Consultar el comportamiento de una familia de malware.
* Obtener definición y detalles técnicos.
* Consultar información global sobre el impacto de una amenaza.
* Realizar análisis avanzados sobre su impacto en la organización.
* Identificar instancias en las que usuarios recibieron archivos adjuntos con un malware específico.
* Bloquear un correo antes de que llegue al usuario o tratarlo como spam.

---

# Microsoft Defender for Cloud Apps

Microsoft Cloud App Security proporciona visibilidad sobre actividades sospechosas en Microsoft 365 y mejora el control sobre el tenant.

Sus tres áreas principales son:

### Threat detection

Detecta:

* Uso anormal o de alto riesgo.
* Incidentes de seguridad.
* Amenazas potenciales.

Por ejemplo, puede alertar cuando un administrador realiza una actividad inusual, como reenviar correo a diferentes personas.

### Enhanced control

Monitoriza actividades mediante controles y políticas granulares.

Por ejemplo, puede generar una alerta ante una descarga masiva de información.

### Discovery and insights

Proporciona información sobre las aplicaciones cloud utilizadas por la organización y permite determinar cuáles están aprobadas.

Cloud App Security admite:

* Log collection.
* API connectors.
* Reverse proxy.

Proporciona visibilidad sobre los servicios cloud propios y de terceros, control sobre el movimiento de datos y análisis para detectar y combatir amenazas.

---

# Cloud App Security Framework

Sus principales capacidades incluyen:

* **Discover and control Shadow IT:** identifica aplicaciones cloud, servicios IaaS y PaaS utilizados por la organización, analiza patrones de uso y evalúa riesgos.
* **Protect sensitive information:** permite comprender, clasificar y proteger información sensible almacenada en la nube mediante políticas y procesos automatizados.
* **Protect against cyberthreats and anomalies:** detecta comportamientos anómalos, ransomware, usuarios comprometidos y aplicaciones sospechosas, permitiendo remediación automática.
* **Assess cloud app compliance:** evalúa el cumplimiento de aplicaciones cloud y permite evitar filtraciones hacia aplicaciones que no cumplen requisitos.

La integración con la nube incluye:

* **Cloud Discovery:** identifica el entorno cloud y las aplicaciones utilizadas.
* **Sanctioning/unsanctioning:** permite aprobar o desaprobar aplicaciones.
* **App connectors:** utilizan APIs de proveedores para obtener visibilidad y aplicar gobernanza.
* **Conditional Access App Control:** proporciona visibilidad y control en tiempo real sobre acceso y actividades.
* **Políticas:** permiten mantener un control continuo mediante configuración y ajuste permanente.

---

# Informes de seguridad en Microsoft Defender XDR

Microsoft Defender XDR organiza sus informes en tres categorías:

## Security

Muestra tendencias de seguridad y el estado de protección de:

* Identidades.
* Datos.
* Dispositivos.
* Aplicaciones.
* Infraestructura.

## Email and collaboration

Muestra acciones recomendadas por Microsoft para mejorar la seguridad del correo y la colaboración.

## Endpoints

Muestra información sobre:

* Protección contra amenazas.
* Estado y cumplimiento de dispositivos.
* Dispositivos vulnerables.
* Web protection.

## Roles necesarios

Para consultar estos informes se requiere pertenecer a uno de estos grupos del portal Microsoft Defender:

* Organization Management.
* Security Administrator.
* Security Reader.
* Global Reader.

La asignación de los roles correspondientes de Microsoft Entra en el centro de administración de Microsoft 365 proporciona los permisos necesarios en el portal Microsoft Defender.

---

# Informes de Security

Los informes de seguridad se dividen en:

### Identities

* Users at risk.
* Global admins.

### Data

* Users with the most shared files.
* DLP policy matches.
* Third-party DLP policy matches.
* DLP false positives and overrides.

### Devices

* Devices at risk.
* Threat analytics.
* Device compliance.
* Devices with active malware.
* Types of malware on devices.
* Malware on devices.
* Devices with malware detections.
* Users with malware detections.

### Apps

* Privileged OAuth apps.
* Cloud app accounts for review.
* Discovered cloud apps.
* Cloud app activity locations.

---

# Informes de Microsoft Defender for Endpoint

Incluyen:

* Threat protection.
* Device health and compliance.
* Vulnerable devices.
* Web protection.

# Informes de Microsoft Defender for Office 365

Incluyen:

* Top malware.
* Mail latency report.
* Top senders and recipients.
* Mail flow status summary.
* Threat protection status.
* URL protection report.
* Spoof detections.
* Compromised users.
* Exchange transport rule.
* User reported messages.
* Submissions.

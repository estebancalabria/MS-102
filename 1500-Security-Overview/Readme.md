# Resumen — Vectores de amenaza y filtraciones de datos

## Introducción

Un **vector de amenaza** es el camino o medio mediante el cual un atacante puede acceder a un objetivo de valor, como:

* Computadoras y servidores.
* Nombres de usuario y contraseñas.
* Información personal.
* Información financiera.
* Planes internos de una organización.

Las organizaciones deben identificar los distintos vectores de amenaza y sus posibles consecuencias, especialmente las técnicas utilizadas para engañar a usuarios, obtener información sensible o ejecutar contenido malicioso.

## Panorama actual de amenazas

La mayoría de los ataques siguen un proceso denominado **Kill Chain**, en el que el atacante avanza por distintas etapas hasta alcanzar su objetivo. Las organizaciones pueden defenderse aplicando controles de seguridad en cada etapa, ya que los atacantes pueden intentar evadir cualquiera de ellas.

El panorama de amenazas se volvió más sofisticado mientras las organizaciones adoptaron servicios cloud. Actualmente deben proteger identidades, dispositivos, aplicaciones y datos distribuidos entre entornos locales, PCs, teléfonos y la nube.

Los empleados también pueden utilizar aplicaciones de terceros y servicios de almacenamiento no aprobados para guardar información corporativa sensible.

En entornos locales existen controles como firewalls, gateways de correo y proxies. La protección también se extendió a dispositivos móviles y recursos cloud, aunque algunas organizaciones tienen un control limitado sobre los dispositivos y sobre los datos cuando salen de su entorno administrado.

Microsoft busca ayudar a las organizaciones a **proteger, detectar y responder** frente a distintos vectores de amenaza.

## Phishing

El **phishing** utiliza mensajes que aparentan provenir de fuentes legítimas para obtener información sensible, como credenciales o números de tarjetas.

Generalmente:

1. El usuario recibe un correo aparentemente legítimo.
2. El mensaje intenta generar urgencia o confianza.
3. El usuario selecciona un enlace.
4. El enlace lleva a un sitio malicioso que imita al legítimo.
5. El usuario introduce información sensible o descarga malware.

### Malware

El malware puede llegar mediante archivos adjuntos o enlaces a sitios maliciosos y suele funcionar en dos etapas:

* **Etapa 1:** el usuario abre un archivo infectado o visita un sitio comprometido. Se explota el equipo mediante código, macros o JavaScript.
* **Etapa 2:** se entrega el payload malicioso.

Tipos mencionados:

* **Virus:** se replica modificando otros programas e insertando su propio código.
* **Trojan horse:** funciona como una puerta trasera y puede bloquear antivirus, instalar aplicaciones, robar contraseñas y tarjetas o infectar otros dispositivos.
* **Rootkit:** proporciona acceso administrativo y normalmente permite acceso completo y no detectado; puede robar o falsificar documentos, ocultar malware y utilizar el equipo para atacar otros sistemas.
* **Spyware:** recopila actividad de Internet, pulsaciones de teclado, contraseñas y otros datos sensibles; también puede utilizarse como adware para mostrar anuncios y rastrear comportamiento.

### Spear phishing

Es phishing dirigido a individuos específicos. El **whaling** suele apuntar a ejecutivos y personas de alto perfil, generalmente con fines económicos.

Los correos de phishing suelen utilizar:

* Branding aparentemente legítimo.
* URLs que parecen confiables.
* Mensajes con sensación de urgencia.
* Solicitudes de información sensible.
* Enlaces capaces de instalar malware.

## Spoofing

El **spoofing** aprovecha SMTP para hacer que un correo parezca provenir de otro dominio o de una fuente confiable.

Existen usos legítimos, como:

* Envío de correos masivos internos mediante terceros.
* Empresas externas que envían comunicaciones en nombre de una organización.
* Asistentes que envían mensajes en nombre de otra persona.
* Aplicaciones internas que generan notificaciones.
* Listas de distribución.
* Empresas externas que envían reportes o comunicaciones en nombre de otras empresas.

Los atacantes utilizan spoofing para falsificar encabezados y engañar a los destinatarios con el objetivo de obtener credenciales, información financiera u otros datos sensibles.

Un correo contiene dos direcciones de remitente:

* **5321.MailFrom:** identifica al remitente utilizado por el servidor de correo y aparece como `Return-Path`.
* **5322.From:** es la dirección que muestra el cliente de correo como remitente.

**Exchange Online Protection (EOP)** protege automáticamente los mensajes entrantes contra spoofing y utiliza **spoof intelligence** como parte de la defensa contra phishing.

## Spam y malware

El spam y el correo masivo normalmente son molestias que afectan la productividad, pero los atacantes pueden utilizarlos como vehículo para distribuir malware.

El malware suele recibirse mediante:

* Archivos adjuntos.
* Enlaces incrustados hacia sitios o archivos maliciosos.

## Compromiso de cuentas

Un **account breach** ocurre cuando individuos no autorizados obtienen acceso a una cuenta.

Métodos principales:

* **Password attacks:** ataques de fuerza bruta, contraseñas débiles, fáciles de adivinar, reutilizadas o robadas.
* **Phishing:** engaño para obtener credenciales.
* **Credential stuffing:** utilización de combinaciones de usuario y contraseña obtenidas de otras filtraciones.
* **Key loggers:** software o hardware que registra las pulsaciones del usuario para capturar credenciales, números de tarjetas y otros datos.
* **Social engineering:** manipulación de personas mediante suplantación, escenarios elaborados o explotación de vulnerabilidades psicológicas.

Una cuenta comprometida puede permitir acceder a correos, archivos e información personal, enviar mensajes o realizar acciones en nombre del usuario y provocar filtraciones de datos, violaciones de privacidad, pérdidas financieras, robo de identidad y nuevos ataques.

### Mitigación de compromisos de cuentas

* **Autenticación fuerte:** implementar MFA o 2FA.
* **Microsoft Entra ID Protection:** detectar y responder a riesgos de identidad mediante análisis y machine learning.
* **Políticas de contraseñas:** utilizar contraseñas fuertes y únicas, evitar su reutilización y considerar gestores de contraseñas.
* **Security awareness training:** capacitar a los usuarios para reconocer y reportar phishing, ingeniería social y solicitudes sospechosas.
* **Least privilege:** otorgar únicamente los permisos necesarios.
* **Monitoreo y Activity Logs:** registrar inicios de sesión, intentos fallidos y comportamientos inusuales; utilizar alertas y SIEM.
* **Patching y actualizaciones:** mantener sistemas y aplicaciones actualizados.
* **Evaluaciones de seguridad:** realizar evaluaciones, escaneos de vulnerabilidades y pruebas de seguridad.
* **Incident response plan:** definir roles, responsabilidades y canales para responder ante compromisos.
* **Cifrado y protección de datos:** proteger información en reposo y tránsito, utilizando TLS y soluciones DLP. Azure Information Protection permite clasificar, etiquetar, cifrar y controlar el acceso a documentos y correos.
* **Monitoreo continuo:** utilizar monitoreo de seguridad e inteligencia de amenazas para adaptarse a riesgos emergentes.

Microsoft recomienda MFA en lugar de depender de la expiración periódica de contraseñas, ya que el cambio periódico de contraseñas no proporciona beneficios de contención significativos cuando las credenciales ya fueron comprometidas.

## Elevación de privilegios

En una **elevation of privilege attack**, el atacante busca aumentar sus permisos después de comprometer una o más cuentas.

En Microsoft 365, normalmente busca obtener privilegios de **Global Administrator**. También puede intentar obtener privilegios específicos sobre el servicio que contiene los datos objetivo.

Una técnica consiste en crear una nueva cuenta y convertirla en Global Administrator para **ocultarse a plena vista**.

### Prevención

* Implementar **Microsoft Entra MFA**, especialmente en cuentas administrativas y con acceso a información sensible.
* Mantener reducido el número de Global Administrators.
* Microsoft recomienda entre **2 y 5 Global Administrators** por tenant.
* Revisar periódicamente los Global Administrators y su actividad.
* Auditar y configurar alertas.

Después de un compromiso se deben revisar:

* Nuevas cuentas.
* Cuentas recientemente modificadas.
* Cuentas promovidas a Global Administrator.
* Cambios de configuración global.
* Interacciones con datos realizadas por las cuentas afectadas.
* ACL de documentos.
* Permisos de delegación de buzones.
* Reglas de forwarding de buzones.
* Reglas de transporte de correo.

## Exfiltración de datos

La **data exfiltration** es la recuperación o extracción no autorizada de datos desde una computadora o servicio.

Los atacantes pueden utilizar:

* Cuentas comprometidas con acceso a los datos.
* Ataques contra sistemas e infraestructura para obtener privilegios locales o administrativos.

Motivaciones:

* Robar propiedad intelectual.
* Extorsionar.
* Vender datos en el mercado negro.
* Mantenerse dentro de los sistemas.

Los datos de interés pueden incluir correos, documentos, conversaciones de mensajería, hilos de Yammer e información del directorio.

### Prevención de la exfiltración

* **Access Control Lists:** definir quién puede acceder a cada tipo de información, aplicar el mínimo privilegio y revisar regularmente los permisos.
* **External sharing policies:** restringir el intercambio de documentos con personas externas cuando sea necesario.
* **Least privilege:** otorgar únicamente el nivel mínimo de permisos requerido.
* **Data classification:** clasificar los datos según niveles de riesgo, como alto, medio o bajo impacto empresarial.
* **Data Loss Prevention (DLP):** utilizar Microsoft Purview DLP para controlar el movimiento de información dentro y fuera del tenant y evitar el envío de información sensible a terceros.

También se pueden utilizar auditorías, alertas y Advanced Security Management para detectar comportamientos sospechosos.

## Eliminación de datos

La **data deletion** ocurre cuando un atacante elimina información, generalmente buscando dificultar o impedir su recuperación.

Una variante es el **ransomware**, donde el atacante compromete la red, cifra los datos y exige un pago para obtener la clave de descifrado.

Motivaciones:

* Ocultar rastros del ataque.
* Causar daños irreparables al negocio.
* Perjudicar a la organización o a sus empleados.

### Métodos de eliminación

* Comprometer una cuenta administrativa mediante phishing o ataques de contraseñas.
* Explotar vulnerabilidades en aplicaciones integradas.
* Engañar a usuarios para que eliminen información mediante enlaces o archivos maliciosos.
* Utilizar ransomware para cifrar y eliminar archivos.
* Robar credenciales mediante phishing o malware y utilizarlas para eliminar datos.
* Utilizar una cuenta que ya tenga permisos para eliminar información.

### Prevención

* **MFA:** especialmente para administradores.
* **Role-based access controls:** limitar quién puede eliminar datos.
* **Alertas y monitoreo:** detectar inicios de sesión o eliminaciones sospechosas.
* **Backups offline:** mantener copias de datos críticos fuera de las cuentas online.
* **Cifrado:** proteger datos en reposo y tránsito.
* **Actualizaciones de seguridad:** corregir vulnerabilidades.
* **Herramientas de seguridad:** como Microsoft Defender for Office 365 para detectar y bloquear malware y phishing.
* **Capacitación de usuarios.**
* **Data labeling:** clasificar y etiquetar información sensible.
* **Incident response plan.**
* **Access termination:** revisar permisos y finalizar sesiones/tokens de empleados que abandonan la organización.

La protección requiere combinar controles preventivos y detectivos para lograr una defensa en profundidad.

Microsoft 365 mantiene redundancia y realiza backups para disponibilidad, pero un atacante puede eliminar datos de SharePoint y de las papelera de reciclaje, dificultando su recuperación. Por eso es importante mantener backups críticos en almacenamiento offline que pueda restaurarse.

## Data spillage

El **data spillage** ocurre cuando un usuario libera un documento confidencial en un entorno no confiable.

Ante un incidente se debe:

1. Evaluar el tamaño y las ubicaciones afectadas.
2. Examinar las actividades de los usuarios.
3. Eliminar permanentemente los datos expuestos.

Puede ocurrir, por ejemplo, cuando un empleado comparte accidentalmente un documento altamente confidencial por correo con múltiples personas.

### Gestión de un incidente de data spillage

#### Paso 1: Controlar el acceso al caso

Se puede controlar quién accede al caso de eDiscovery mediante grupos de roles y límites de cumplimiento.

Puede crearse un grupo **Data Spillage Investigator** con roles como:

* Export.
* RMS Decrypt.
* Review.
* Preview.
* Compliance Search.
* Case Management.

#### Paso 2: Crear un caso de eDiscovery

Permite:

* Administrar investigadores.
* Realizar búsquedas iterativas.
* Exportar reportes.
* Seguir el estado del caso.
* Consultar sus detalles posteriormente.

Se recomienda utilizar una convención de nombres que facilite localizar los casos.

#### Paso 3: Buscar los datos expuestos

Se realizan búsquedas iterativas para localizar los mensajes y buzones afectados.

Las palabras clave pueden contener el propio dato expuesto; por eso, si una búsqueda utiliza información sensible como criterio, la consulta debe eliminarse posteriormente para evitar una nueva exposición.

#### Paso 4: Revisar y validar los resultados

Se debe verificar que los resultados contienen únicamente mensajes que deben eliminarse.

Una búsqueda de contenido permite previsualizar una muestra aleatoria de hasta **1.000 mensajes** sin exportarlos.

Cuando hay demasiados resultados, se pueden dividir las búsquedas utilizando:

* Palabras clave.
* Rangos de fechas.
* Remitentes.
* Destinatarios.

Con **Microsoft Purview eDiscovery (Premium)**, los usuarios o custodios con licencia Microsoft 365 E5 pueden examinar hasta **10.000 resultados** simultáneamente.

También pueden utilizarse:

* Etiquetado de resultados.
* OCR.
* Email threading.
* Predictive coding.

Al identificar un mensaje con datos expuestos, se deben revisar sus destinatarios para determinar si fue compartido externamente.

#### Paso 5: Revisar Message Trace

Los registros de **message trace** permiten investigar cómo se compartieron los mensajes.

Se utilizan los datos del remitente y el rango de fechas obtenidos durante la revisión.

Retención:

* **30 días:** datos en tiempo real.
* **90 días:** datos históricos.

Puede utilizarse Message Trace en Microsoft Purview o los cmdlets correspondientes de Exchange Online PowerShell. El seguimiento de mensajes no garantiza que los resultados sean completamente exhaustivos.

#### Paso 6: Preparar los buzones

Se recopilan las direcciones de los buzones afectados para realizar la eliminación.

Puede ser necesario preparar los buzones dependiendo de si:

* Está habilitada la recuperación de elementos eliminados.
* Los buzones están sujetos a algún hold.

#### Paso 7: Eliminar permanentemente los datos

Se utiliza la búsqueda refinada para eliminar los mensajes que contienen los datos expuestos.

El usuario debe pertenecer a:

* **Organization Management**, o
* Tener el rol **Search And Purge**.

#### Paso 8: Verificar y generar evidencia

Se vuelve a ejecutar la misma búsqueda utilizada para eliminar los datos y se confirma que no devuelve resultados.

Después:

* Se exporta un reporte como prueba de eliminación.
* Se cierra el caso.
* Se conserva el reporte para futuras referencias.
* Se pueden revertir los buzones a su estado anterior.
* Se elimina la consulta utilizada.
* Se revisan los registros de auditoría de las tareas realizadas.

## Otros tipos de ataques

### Password cracking

El atacante obtiene acceso a una aplicación, servicio o almacén de datos que permite probar numerosas combinaciones de contraseñas.

Utiliza software especializado para probar miles de combinaciones rápidamente.

Las contraseñas:

* Cortas.
* Débiles.
* Comunes.
* Reutilizadas.

aumentan las posibilidades de compromiso.

### Prevención del password cracking

Cuando las organizaciones utilizan Microsoft Entra ID para autenticación sin federation, Microsoft Entra ID deshabilita temporalmente una cuenta después de múltiples intentos fallidos mediante **smart password lockout**.

Cuando las credenciales se almacenan en otros lugares, las organizaciones deben implementar controles de directorio contra múltiples intentos fallidos. El número de intentos permitidos debe determinarse según las necesidades de la organización.

### Malicious insider

Un **malicious insider** es un usuario autorizado que realiza actividades ilícitas dentro del tenant.

Puede ser especialmente peligroso porque conoce:

* La organización.
* Sus sistemas.
* Sus datos.
* Cómo maximizar el impacto.

Motivaciones:

* Empleados descontentos que buscan obtener dinero.
* Personas que quieren causar problemas antes de abandonar la empresa.
* Personas que buscan perjudicar a individuos o a la organización.

Un insider malicioso puede:

* Crear cuentas backdoor para mantener acceso.
* Exfiltrar información.
* Eliminar datos sensibles.

Los usuarios con privilegios administrativos suelen ser los insiders más peligrosos.

### Prevención del malicious insider

Las organizaciones deben:

* Proteger las cuentas.
* Administrar correctamente los privilegios.
* Proteger los datos.
* Contar con procesos para identificar posibles motivaciones.
* Detectar empleados descontentos o insatisfechos.
* Protegerse frente a proveedores temporales y personal eventual mediante controles de acceso y auditoría.

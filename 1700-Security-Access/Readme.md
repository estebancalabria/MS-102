# Seguridad de acceso de usuarios en Microsoft 365

## Introducción
Microsoft 365 contiene datos sensibles (correos, documentos, información de clientes, propiedad intelectual). El acceso no autorizado puede provocar filtraciones de datos, robo de identidad y otras actividades maliciosas. La autenticación multifactor (MFA) reduce significativamente el riesgo de acceso no autorizado, ya que exige un paso de verificación adicional aunque la contraseña se vea comprometida.

Asegurar el acceso de usuarios ayuda a:
- Prevenir el mal uso o filtración de datos.
- Mantener privacidad e integridad de la información.
- Proteger contra phishing e ingeniería social (MFA, políticas de acceso condicional).
- Garantizar continuidad del negocio ante incidentes de seguridad.
- Controlar TI en la sombra (shadow IT) y BYOD.

Métodos cubiertos: cambio periódico de contraseñas, contraseñas complejas, restablecimiento propio, MFA, acceso condicional, autenticación sin contraseña, Smart Lockout.

## Herramientas de identidad y acceso en Microsoft 365

**Microsoft Entra ID**: servicio de directorio e identidad basado en la nube. Da a cada usuario una identidad única usable en múltiples dispositivos/apps sin recordar varias contraseñas. Soporta modelos de identidad (cloud-only, híbrido, federado), múltiples métodos de autenticación (contraseña, MFA, certificados, Windows Hello for Business) y aplicación de políticas (acceso condicional, protección de identidad, PIM, revisiones de acceso).

**Centro de administración de Microsoft 365**: portal web unificado para gestionar usuarios, grupos, licencias, facturación, seguridad, cumplimiento y configuración. Se integra con Entra ID, SharePoint, Exchange, Teams y OneDrive, usando Entra ID para autenticar usuarios y dispositivos.

**Single Sign-On (SSO)**: permite iniciar sesión en múltiples apps con un solo set de credenciales. Mejora la experiencia de usuario, aumenta productividad y refuerza seguridad/cumplimiento. Soporta apps en la nube y on-premises (vía Application Proxy, Connect Sync o ADFS) y protocolos como SAML, OAuth, OpenID Connect y WS-Federation.

**PowerShell para Microsoft 365 (Graph PowerShell SDK)**: automatiza tareas y gestiona recursos (usuarios, grupos, licencias, buzones, calendarios, archivos, sitios, equipos, etc.) mediante la API de Microsoft Graph. Ofrece control granular, gestión/automatización simplificada, seguridad reforzada (MFA, acceso condicional, RBAC) e integración con Azure, Dynamics 365 y Power Platform.

**Microsoft Graph API**: servicio web RESTful que expone datos y funcionalidades de Microsoft 365 y otros servicios Microsoft (Azure, Dynamics 365, Power Platform), incluyendo relaciones entre recursos (membresías, permisos, mensajes, eventos, tareas). Ofrece acceso de datos consistente, integración/personalización simplificada, seguridad reforzada e innovación (bots, dashboards, workflows, analítica).

## Gestión de contraseñas de usuario

Roles requeridos:
- Global Administrator, Security Administrator y Privileged Role Administrator: pueden realizar todas las tareas de gestión de contraseñas.
- User Administrator y Password Administrator: pueden restablecer contraseñas.

**Expiración de contraseñas**: por defecto, las contraseñas nunca expiran, porque forzar cambios periódicos hace que los usuarios elijan contraseñas más débiles o predecibles. Microsoft recomienda MFA en vez de expiración periódica. Si se configura, puede establecerse entre 14 y 730 días desde el Centro de administración (Configuración > Configuración de la organización > Seguridad y privacidad > Política de expiración de contraseñas).

**Restablecimiento de contraseñas de usuarios**: un administrador puede asignar una contraseña nueva (aleatoria o elegida) desde la página de usuarios activos, y exigir cambio en el próximo inicio de sesión. Existe también el restablecimiento de contraseña autoservicio (SSPR), que debe habilitarse explícitamente.

**Restablecimiento de contraseñas de administradores**: otro administrador (Global, User Management o Password admin) puede restablecerla, o el propio usuario mediante el enlace "¿No puede acceder a su cuenta?" (requiere correo alternativo y, en ciertos casos, teléfono). El proceso debe completarse en 10 minutos.

**Eliminación de contraseñas débiles**: recomendaciones básicas (no reutilizar, evitar variantes de "password", evitar nombres/números simples). Microsoft Entra Password Protection detecta y bloquea contraseñas débiles conocidas y sus variantes, además de términos específicos de la organización. Requiere rol Global Administrator, Security Administrator o Privileged Role Administrator.

- **Lista global de contraseñas prohibidas**: basada en telemetría de seguridad de Entra ID (no en fuentes externas), se actualiza constantemente y se aplica automáticamente a todos los usuarios del tenant; no se puede deshabilitar ni se publica su contenido.
- **Lista personalizada de contraseñas prohibidas**: hasta 1000 términos específicos de la empresa (marcas, productos, ubicaciones, términos internos). Es insensible a mayúsculas, detecta sustituciones de caracteres comunes (o/0, a/@), longitud de 4 a 16 caracteres. Se configura en Entra admin center > Protection > Authentication methods > Password protection, habilitando "Enforce custom list" y "Enable password protection on Windows Server Active Directory". Los cambios pueden tardar varias horas en aplicarse.
- Protege contra ataques de password spray, que prueban pocas contraseñas débiles conocidas contra muchas cuentas para evitar bloqueos por intentos.
- Mensajes de error típicos indican que la contraseña es fácil de adivinar o está bloqueada por el administrador.

**Requisitos de licencia**:
- Usuarios solo en la nube: Entra Free (lista global) / Entra Premium P1 o P2 (lista personalizada).
- Usuarios sincronizados desde AD DS on-premises: Entra Premium P1 o P2 para ambas listas.

## Políticas de acceso condicional

El acceso condicional (Conditional Access) de Microsoft Entra ID permite controlar el acceso a recursos según condiciones como identidad, dispositivo, ubicación, red, app y nivel de riesgo. Funciona como reglas "si-entonces" (ej.: si el usuario quiere acceder a nómina, entonces debe usar MFA). Requiere licencia Entra ID Premium P1 (o Microsoft 365 Business Premium).

Se aplica después de la autenticación de primer factor; no reemplaza defensas contra ataques DoS.

**Integración con Defender for Endpoint e Intune**: si Defender for Endpoint marca un dispositivo como no conforme, el servicio de acceso condicional puede bloquear su acceso a recursos corporativos. Incluye:
- Acceso condicional basado en dispositivo (solo dispositivos administrados/conformes).
- Acceso condicional basado en apps (solo apps administradas).

**Señales comunes**: membresía de usuario/grupo, ubicación de IP, dispositivo (plataforma/estado), aplicación, detección de riesgo en tiempo real (vía Entra ID Protection), Microsoft Defender for Cloud Apps.

**Decisiones comunes**: bloquear acceso (más restrictivo) o conceder acceso (requiriendo MFA, dispositivo conforme, dispositivo unido a Entra híbrido, app cliente aprobada, etc.).

**Políticas comunes**: MFA para roles administrativos, MFA para tareas de gestión de Azure, bloqueo de autenticación heredada, MFA para todos los usuarios, MFA basada en riesgo de inicio de sesión, cambio de contraseña para usuarios de riesgo, requerir dispositivos conformes/híbridos, requerir apps aprobadas, bloqueo/concesión por ubicación.

**Creación de una política** (ejemplo, basada en conformidad de dispositivo): desde Intune admin center > Endpoint security > Conditional Access > Nueva política. Se configuran:
- **Asignaciones**: usuarios/grupos objetivo, recursos objetivo (apps, acciones de usuario, contexto de autenticación), red (ubicaciones con nombre: rangos IP, países/regiones, ubicaciones de confianza — máx. 195 ubicaciones con nombre y 2000 rangos IP cada una, máscaras CIDR mayores a /8).
- **Condiciones**: riesgo de inicio de sesión, ubicación de red, información del dispositivo.
- **Controles de acceso**: en concesión (MFA, fuerza de autenticación, dispositivo conforme, dispositivo híbrido, app aprobada, política de protección de apps, cambio de contraseña); en sesión (restricciones aplicadas por la app, control de apps de acceso condicional, frecuencia de inicio de sesión, sesión de navegador persistente, evaluación de acceso continuo, protección de tokens, perfil de seguridad de Global Secure Access).
- **Habilitación de política**: modo "solo informe" (evalúa sin aplicar, resultados visibles en logs), "activado" o "desactivado".

**Fuerza de autenticación** (authentication strength): especifica qué combinaciones de métodos de autenticación son válidas para acceder a un recurso. Tipos integrados:
- MFA: combina dos o más factores (ej. contraseña + SMS, tarjeta inteligente + PIN).
- MFA sin contraseña: biometría o claves de seguridad (FIDO2, Windows Hello).
- MFA resistente a phishing: FIDO2, biometría de Windows Hello.

También se pueden crear fuerzas de autenticación personalizadas. Durante el inicio de sesión, el sistema verifica métodos permitidos, registrados por el usuario y requeridos por la política; si el usuario no tiene un método registrado que satisfaga la fuerza requerida, se le redirige al registro combinado o se le bloquea el acceso.

## Autenticación de paso a través (Pass-Through Authentication, PTA)

Permite a los usuarios autenticarse en servicios de Microsoft 365 usando sus credenciales de Active Directory on-premises, sin almacenar contraseñas en la nube. Reduce riesgo de ataques relacionados con contraseñas (phishing, spraying) y permite aplicar MFA y acceso condicional. Ofrece validación de autenticación en tiempo real enviando solicitudes directamente al AD on-premises.

Es una alternativa más simple que AD FS (que requería infraestructura compleja y costosa). Si PTA falla, puede haber conmutación automática a sincronización de hash de contraseñas si está habilitada.

**Proceso**: se configura mediante Microsoft Entra Connect Sync, usando un agente on-premises que escucha solicitudes de validación de contraseña (solo comunicación saliente, no requiere red perimetral). El agente debe unirse al dominio de AD que contiene los usuarios. Flujo: el usuario ingresa credenciales en la página de Entra > el sistema coloca las credenciales en cola del conector > el agente conector las valida contra AD local > la respuesta de AD vuelve al conector > al servicio de Entra ID.

**Habilitación**: ejecutar el asistente de configuración de Microsoft Entra Connect Sync y seleccionar la opción de autenticación de paso a través. Se recomienda desplegar un conector adicional en otro servidor para alta disponibilidad. Puertos requeridos: 80, 443, 8080/443, 9090, 9091, 9352, 5671, 9350 (opcional), 10100–10120.

## Autenticación multifactor (MFA)

Combina algo que el usuario sabe (contraseña), algo que tiene (teléfono) y/o algo que es (biometría). El segundo factor se solicita después de verificar la contraseña.

**Métodos soportados**: llamada telefónica o SMS (método por defecto), app Microsoft Authenticator (notificaciones push o códigos), tokens de hardware OATH, claves de seguridad FIDO2, otras apps de terceros basadas en TOTP (Google Authenticator, Authy).

**Formas de habilitar MFA**:
1. **Políticas de acceso condicional** (recomendado por Microsoft): requiere licencia Microsoft 365 Business Premium, E3/E5, o Entra ID P1/P2. Permite exigir MFA por grupo, app o dispositivo. Debe desactivarse el MFA por usuario y los valores de seguridad predeterminados antes de habilitar acceso condicional, para evitar conflictos. Con Entra ID Protection (E5/P2) se puede exigir MFA según nivel de riesgo de inicio de sesión.
2. **Valores de seguridad predeterminados (Security Defaults)**: opción sencilla que activa MFA para todos, bloquea autenticación heredada y exige registro de MFA. Es todo o nada (no personalizable); recomendado para organizaciones pequeñas/medianas con recursos de TI limitados.
3. **MFA heredado por usuario** (no recomendado para organizaciones grandes): habilitado desde el Centro de administración, de forma individual o por archivo CSV masivo. Desventajas: complejidad de gestión, riesgo de mala configuración, no bloquea autenticación heredada, falta de control contextual, problemas de escalabilidad.

**Configuración por usuario**: desde Configuración > Configuración de la organización > Autenticación multifactor, se puede habilitar/deshabilitar por usuario, gestionar métodos de contacto, contraseñas de aplicación, IPs de confianza, opciones de verificación y recordar MFA en dispositivos de confianza (entre 1 y 365 días, por defecto 90 días).

**Optimización de reautenticación**: Microsoft recomienda usar frecuencia de inicio de sesión de acceso condicional en vez de "recordar MFA en dispositivos de confianza"; solicitar credenciales con demasiada frecuencia puede aumentar la vulnerabilidad a ataques y afectar la productividad.

## Autenticación sin contraseña

Reemplaza la contraseña por algo que el usuario tiene, es o sabe. Opciones disponibles en Microsoft Entra ID:

- **Windows Hello for Business**: reemplaza contraseñas con autenticación de dos factores ligada al dispositivo (requiere TPM), usando PIN o biometría almacenada localmente en el dispositivo. Soporta SSO e integración con PKI, AD on-premises y Entra ID. También soporta MFA. Resuelve problemas de contraseñas débiles, reutilizadas, filtradas en brechas de servidor, ataques de repetición (replay) y phishing.
- **Platform Credential para macOS**: usa la extensión SSO empresarial (SSOe) de Microsoft con una clave criptográfica vinculada a hardware (enclave seguro); permite Touch ID sin afectar la contraseña local de la cuenta. Requiere habilitar el método FIDO2 y, si se usan políticas de restricción de claves, añadir el AAGUID correspondiente.
- **Platform SSO (PSSO) para macOS con SmartCard**: usa una tarjeta inteligente o token físico compatible (ej. Yubikey) junto con autenticación basada en certificados (CBA); se configura vía Intune u otro MDM.
- **Microsoft Authenticator**: convierte el teléfono en credencial fuerte sin contraseña, mediante notificación push (con coincidencia de número y confirmación biométrica/PIN) o código TOTP. Las notificaciones push son el método preferido por ser más seguras y rápidas. Requisitos: habilitar MFA con notificaciones push, instalar la última versión de la app, registrar el dispositivo (Android: registro individual; iOS: registro por tenant).
- **Passkeys (FIDO2)**: claves de seguridad basadas en el estándar FIDO2/WebAuthn, no phishables, en forma de USB, Bluetooth o NFC. Permiten SSO en dispositivos Windows unidos a Entra ID/híbridos y en navegadores compatibles. Útiles para escenarios sin teléfono (PCs compartidas, mesa de ayuda, kioscos).
- **Autenticación basada en certificados (CBA)**: permite autenticar directamente con certificados X.509 contra Entra ID, sin depender de AD FS federado. Es una función gratuita, no requiere despliegues on-premises complejos, no almacena contraseñas on-premises en la nube, y se integra con acceso condicional y MFA resistente a phishing.

## Restablecimiento de contraseña autoservicio (SSPR)

Permite a los usuarios restablecer su propia contraseña sin intervención de un administrador. No está habilitado por defecto; debe activarse para todos los usuarios o grupos específicos.

**Métodos de verificación**: correo alternativo, llamada a teléfono de oficina, llamada a móvil, SMS a móvil, preguntas de seguridad. Los administradores deben usar dos métodos de verificación y no pueden usar preguntas de seguridad.

**Limitaciones**: solo disponible para usuarios con identidades en la nube cuyas contraseñas no estén vinculadas a AD DS on-premises, salvo que se use Microsoft Entra Connect Sync con "password writeback" habilitado (requiere licencias Entra ID Premium). Esto permite sincronizar la nueva contraseña de vuelta al AD on-premises.

## Microsoft Entra Smart Lockout

Bloquea a atacantes que intentan adivinar contraseñas o usar fuerza bruta, diferenciando entre inicios de sesión válidos y de atacantes.

**Comportamiento por defecto**: tras 10 intentos fallidos, bloquea la cuenta 1 minuto; el bloqueo se repite y aumenta con cada intento fallido sucesivo a partir del 11°. Rastrea las últimas 3 contraseñas fallidas para no incrementar el contador si se repite la misma contraseña incorrecta.

Está siempre activo para todos los clientes de Entra ID con valores por defecto; personalizar estos valores requiere licencias pagas. Distingue ubicaciones familiares de no familiares con contadores de bloqueo separados. Cada centro de datos de Entra ID rastrea el bloqueo de forma independiente (umbral x cantidad de centros de datos).

**Integración con PTA**: el umbral de bloqueo de Entra debe ser menor que el umbral de bloqueo de AD, y la duración de bloqueo de Entra debe ser mayor que el contador de reinicio de bloqueo de AD (Entra se define en segundos, AD en minutos). Nota: con PTA habilitado no está disponible el rastreo por hash.

**Gestión de valores**: desde Entra admin center > Protection > Authentication methods > Password protection, se configura el umbral de bloqueo (por defecto 10) y la duración de bloqueo en segundos (por defecto 60).

**Mensaje al activarse**: informa que la cuenta está bloqueada temporalmente para prevenir uso no autorizado.

## Valores de seguridad predeterminados (Security Defaults)

Conjunto de configuraciones de seguridad preconfiguradas que ofrecen protección básica para todos los usuarios y apps de un tenant de Entra ID, sin configurar cada función por separado.

**Funciones habilitadas automáticamente**:
- MFA para todos los usuarios.
- Bloqueo de protocolos de autenticación heredada.
- Registro obligatorio de MFA cuando sea necesario.
- MFA obligatoria para administradores.
- Protección de actividades privilegiadas (ej. acceso al centro de administración de Entra).

**Público objetivo**: organizaciones que quieren mejorar su seguridad pero no saben por dónde empezar, que usan el nivel gratuito de licencias de Entra, o que no usan acceso condicional. Los valores predeterminados de seguridad y el acceso condicional son mutuamente excluyentes (no se pueden usar ambos). Los tenants creados a partir del 22 de octubre de 2019 pueden tenerlos habilitados por defecto.

**Habilitación**: Entra admin center > Identity > Overview > pestaña Properties > sección Security defaults > Manage security defaults > Enabled > Save. Antes de habilitar, se debe notificar a los usuarios, ya que exige MFA inmediatamente y bloquea autenticación heredada.

**Detalle de políticas aplicadas**:
- Registro de MFA obligatorio: todos los usuarios tienen 14 días desde su primer inicio de sesión exitoso tras la habilitación para registrarse (Authenticator o app compatible con OATH TOTP); pasado ese plazo no pueden iniciar sesión hasta completar el registro.
- MFA obligatoria para administradores: aplica a roles como Global, Application, Authentication, Billing, Cloud application, Conditional Access, Exchange, Helpdesk, Password, Privileged authentication, Security, SharePoint y User administrator.
- MFA para usuarios cuando sea necesario: el sistema decide cuándo solicitarla según ubicación, dispositivo, rol y tarea; aplica a todas las apps registradas en Entra ID, incluidas SaaS. Usuarios B2B direct connect deben satisfacer este requisito en su tenant de origen.
- Bloqueo de autenticación heredada: bloquea clientes que no usan autenticación moderna (ej. Office 2010, IMAP, SMTP, POP3) y autenticación básica de Exchange Active Sync, ya que estos protocolos no soportan MFA y son el origen de la mayoría de los inicios de sesión comprometidos.
- Protección de actividades privilegiadas: exige MFA para acceder a servicios gestionados vía Azure Resource Manager (centro de administración de Entra, Azure PowerShell, Azure CLI), tanto para administradores como no administradores.

**Consideraciones de implementación**:
- Los usuarios deben registrarse y usar Microsoft Authenticator con notificaciones (el registro solo puede hacerse con esa opción, aunque luego puedan usar códigos); también se admite OATH TOTP de terceros. No se deben deshabilitar métodos de autenticación, para evitar quedar bloqueados del tenant.
- Se recomienda configurar al menos dos cuentas de administrador de emergencia (acceso de emergencia) con rol Global Administrator, protegidas con contraseñas largas y complejas, credenciales almacenadas de forma segura offline (ej. caja fuerte), no usadas a diario, y opcionalmente sin expiración de contraseña (vía PowerShell).
- Usuarios B2B invitados o direct connect se tratan igual que los usuarios propios de la organización.
- Si la organización usaba MFA por usuario previamente, el estado en la página de MFA puede figurar como "Disabled" para usuarios bajo valores predeterminados o acceso condicional.
- El acceso condicional ofrece más granularidad que los valores predeterminados (permite elegir métodos de autenticación y excluir usuarios), pero ambos son mutuamente excluyentes; para pasar a acceso condicional, primero hay que deshabilitar los valores predeterminados.

## Investigación de problemas de autenticación mediante registros de inicio de sesión

El centro de administración de Microsoft Entra ofrece tres registros de actividad:
- **Registros de inicio de sesión**: información sobre inicios de sesión y uso de recursos.
- **Registros de auditoría**: cambios aplicados al tenant (gestión de usuarios/grupos, actualizaciones de recursos).
- **Registros de aprovisionamiento**: actividades del servicio de aprovisionamiento (ej. creación de grupo en ServiceNow, usuario importado de Workday).

**Registro de inicio de sesión**: registra todos los inicios de sesión de usuarios en el tenant, incluyendo apps y recursos internos. Permite responder preguntas como cuántos usuarios accedieron a una app, cuántos intentos fallidos hubo, desde qué navegadores/SO se conectan los usuarios, y qué recursos acceden las identidades administradas y entidades de servicio. Identifica quién (identidad), cómo (aplicación/cliente) y qué (recurso) se accede. Las entradas son generadas por el sistema y no pueden modificarse ni eliminarse.

**Tipos de registro de inicio de sesión**:
- **Inicios de sesión interactivos de usuario**: el usuario provee un factor de autenticación (contraseña, respuesta a MFA, biometría, código QR), incluyendo inicios de sesión federados. Ejemplos: ingreso de usuario/contraseña, superar un desafío MFA por SMS, gesto biométrico con Windows Hello for Business, federación con AD FS/SAML. Incluye campos adicionales como ubicación del inicio de sesión y si aplica acceso condicional. Limitaciones conocidas: algunos inicios de sesión no interactivos (ej. con claves FIDO2) pueden aparecer marcados como interactivos; los "passthrough sign-ins" (tokens sin autorización entre tenants) no se registran en el tenant de origen; los inicios de sesión de entidades de servicio de aplicaciones internas de Microsoft (first-party, app-only) no se incluyen.
- **Inicios de sesión no interactivos de usuario**: ocurren cuando una app cliente o componente del SO renueva el token del usuario en segundo plano, sin requerir un factor de autenticación explícito. Ejemplos: uso de un refresh token OAuth 2.0, SSO en un dispositivo unido a Entra ID, inicio de sesión en una segunda app de Office usando FOCI. Incluye campos como el ID del recurso y cantidad de inicios de sesión agrupados; no se pueden personalizar los campos mostrados. El sistema agrupa inicios de sesión idénticos salvo por fecha/hora (mismos: aplicación, usuario, IP, estado, ID de recurso), con filtro de agregación de 1, 6 o 24 horas. La IP de inicios de sesión no interactivos de clientes confidenciales muestra la IP original de emisión del token, no la IP real de la solicitud de renovación.
- **Inicios de sesión de entidades de servicio (service principal)**: no involucran a un usuario, sino a apps/entidades de servicio que usan sus propias credenciales (certificado o secreto de app). Ejemplos: autenticación con certificado para acceder a Microsoft Graph, uso de client secret en flujo OAuth Client Credentials. Se agrupan por nombre/ID de entidad de servicio, estado, IP y nombre/ID de recurso; no se pueden personalizar los campos mostrados.
- **Inicios de sesión de identidades administradas (managed identity)**: realizados por recursos con credenciales gestionadas por Azure (ej. una VM que obtiene un token de acceso vía Entra ID). Se agrupan por nombre/ID de identidad administrada, estado y nombre/ID de recurso; no se pueden personalizar los campos mostrados.

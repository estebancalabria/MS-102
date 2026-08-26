# Identidad y sincronización en Microsoft 365

## Modelos de identidad

Microsoft 365 utiliza **Microsoft Entra ID** para administrar identidades y autenticación. Existen dos modelos:

* **Identidad solo en la nube (Cloud-only identity)**: las cuentas de usuario existen únicamente en Microsoft Entra ID.
* **Identidad híbrida (Hybrid identity)**: las cuentas se originan en **Active Directory Domain Services (AD DS)** local y tienen una copia en Microsoft Entra ID.

### Identidad solo en la nube

* Adecuada para organizaciones que no tienen o no necesitan AD DS local.
* Los usuarios se autentican directamente contra Microsoft Entra ID utilizando sus cuentas y contraseñas.
* No requiere herramientas o servidores adicionales de directorio.
* Las identidades se administran mediante herramientas como el **Microsoft 365 admin center** y **Windows PowerShell**.
* Puede utilizar grupos de Microsoft Entra ID para:

  * Asignar licencias automáticamente mediante pertenencia a grupos.
  * Incorporar usuarios dinámicamente según atributos, como el departamento.
  * Aprovisionar usuarios para aplicaciones SaaS y protegerlas mediante MFA y políticas de Conditional Access.
  * Asignar permisos y niveles de acceso a equipos y sitios de SharePoint Online.
* Los tipos de usuarios pueden incluir cuentas del tenant, cuentas B2B y usuarios externos sin cuentas que reciben acceso específico a servicios y recursos.

### Identidad híbrida

* Las cuentas originales se encuentran en **AD DS local** y una copia se sincroniza con Microsoft Entra ID.
* La mayoría de los cambios fluyen **unidireccionalmente**, desde AD DS hacia Microsoft Entra ID.
* El AD DS local es la **fuente autoritativa** de la información de las cuentas.
* La administración de identidades se realiza principalmente en AD DS y los cambios se sincronizan con Microsoft Entra ID.
* Los usuarios pueden utilizar las mismas credenciales para recursos locales y servicios de Microsoft 365.
* Se puede utilizar:

  * **Microsoft Entra Connect Sync**: solución instalada y administrada en un servidor local. Comprueba cambios en AD DS y los sincroniza con Microsoft Entra ID. Incluye sincronización de contraseñas, registro de dispositivos e integración con AD FS. Es escalable para entornos empresariales grandes y complejos.
  * **Microsoft Entra Cloud Sync**: solución basada en la nube, alojada y administrada por Microsoft. Sincroniza usuarios, grupos y contactos desde AD DS hacia Microsoft Entra ID y está orientada a organizaciones con entornos de AD más simples.

## Autenticación en el modelo híbrido

El modelo híbrido permite sincronizar objetos y atributos de AD DS con Microsoft Entra ID, incluyendo actualizaciones de usuarios, grupos y contactos.

Cuando se sincronizan cuentas de AD DS por primera vez:

1. No se asigna automáticamente una licencia de Microsoft 365.
2. Primero se debe asignar una **ubicación de uso (usage location)**.
3. Después se debe asignar una licencia individualmente o mediante pertenencia a un grupo.

Existen dos categorías de autenticación:

* **Autenticación administrada (Managed authentication)**: Microsoft Entra ID gestiona la autenticación.
* **Autenticación federada (Federated authentication)**: Microsoft Entra ID redirige la autenticación a otro proveedor de identidad.

### Autenticación administrada

Tiene dos métodos:

#### Password Hash Synchronization (PHS)

* Microsoft Entra ID realiza la autenticación.
* Permite utilizar el mismo usuario y contraseña que en el entorno local.
* No requiere infraestructura adicional aparte de Microsoft Entra Connect Sync o Microsoft Entra Cloud Sync.
* Utiliza un proceso seguro de sincronización unidireccional del hash de la contraseña.
* El hash se cifra durante la transmisión y se almacena de forma segura en Microsoft Entra ID.
* **Nunca se envía ni almacena la contraseña real en Microsoft Entra ID.**
* Beneficios:

  * Uso de las contraseñas locales para servicios cloud.
  * Menor cantidad de contraseñas que los usuarios deben recordar.
  * Posibilidad de aplicar políticas de contraseñas locales en la nube.
* Cuando cambia o se restablece una contraseña local, se sincroniza el nuevo hash con Microsoft Entra ID.
* Algunas características premium de Microsoft Entra ID, como **Identity Protection**, requieren PHS independientemente del método de autenticación utilizado.

#### Pass-through Authentication (PTA)

* Microsoft Entra ID utiliza AD DS para validar la autenticación.
* Las credenciales se validan mediante un **agente de software ligero** instalado en uno o más servidores locales.
* El agente valida las credenciales directamente contra AD DS y devuelve el resultado a Microsoft 365.
* **Nunca envía ni almacena las contraseñas en Microsoft 365.**
* Permite:

  * Autenticación mediante contraseña.
  * Autenticación con smart cards.
  * Otras formas de MFA.
* Funcionalidades:

  * Excluir usuarios o grupos específicos.
  * Especificar un puerto personalizado para el agente.
  * Configurar failover hacia otros métodos de autenticación.
* Beneficios:

  * Uso de contraseñas locales para servicios cloud.
  * Menor cantidad de contraseñas que los usuarios deben recordar.
  * Aplicación de políticas de contraseñas locales en la nube.
* Requiere instalar y mantener un agente local.
* Es adecuado cuando se necesita aplicar inmediatamente los estados de las cuentas, las políticas de contraseñas y los horarios de inicio de sesión definidos en AD DS.
* La validación de la contraseña se realiza directamente contra AD DS sin almacenar hashes de contraseñas en Microsoft Entra ID.

## Autenticación federada

* Microsoft Entra ID delega la autenticación a un sistema de autenticación confiable independiente.
* Está orientada principalmente a organizaciones empresariales grandes con requisitos de autenticación más complejos.
* Sincroniza las identidades de AD DS con Microsoft 365 y mantiene la administración de cuentas localmente.
* El usuario mantiene la misma contraseña en el entorno local y en la nube.
* Puede utilizar:

  * **Active Directory Federation Services (AD FS)**.
  * Proveedores de identidad de terceros.
* AD FS proporciona **Single Sign-On (SSO)** y capacidades de federación de identidades.
* Permite utilizar las credenciales de AD local para acceder a recursos cloud o de partners sin identidades o credenciales separadas.
* Utiliza **SAML** y otros protocolos para intercambiar información de autenticación y autorización.
* Beneficios de AD FS:

  * Autenticación mediante Active Directory local.
  * SSO para múltiples aplicaciones cloud.
  * Compatibilidad con MFA y políticas de Conditional Access.

### Proceso original de autenticación federada

1. El usuario solicita acceso a un recurso de Microsoft 365.
2. La solicitud llega primero a un **federation proxy server**.
3. El proxy redirige al usuario al proveedor de identidad correspondiente.
4. El proveedor puede ser un servidor AD FS local o un proveedor externo compatible con SAML u OIDC.
5. El proveedor autentica al usuario.
6. Envía un token de seguridad al federation proxy.
7. El proxy lo envía a Microsoft 365.
8. Microsoft 365 utiliza el token para autorizar al usuario y conceder acceso.

El federation proxy actuaba como intermediario y podía proporcionar capacidades de balanceo de carga y failover.

### Web Application Proxy (WAP)

Desde **Windows Server 2012 R2**, el **Web Application Proxy (WAP)** asumió la función del federation server proxy.

* Funciona como proxy del servidor de federación AD FS.
* También proporciona funcionalidad de reverse proxy para aplicaciones web internas.
* Permite acceso externo desde distintos dispositivos.
* Ofrece:

  * Soporte para protocolos modernos como OAuth y OpenID Connect, además de SAML.
  * Publicación flexible de aplicaciones mediante preautenticación y pass-through authentication.
  * Soporte para HTTP y HTTPS, además de SAML y WS-Federation.
  * Integración con Microsoft Entra ID.
  * Mayor escalabilidad y rendimiento frente al antiguo federation proxy.

### Proveedores de identidad de terceros

Microsoft 365 admite federación con proveedores como:

* Microsoft Entra ID.
* PingFederate.
* Okta.
* Otros proveedores compatibles con **SAML** o **WS-Federation**.

Las organizaciones pueden utilizar AD FS local o un proveedor de identidad externo para autenticar usuarios en Microsoft 365. Las soluciones de terceros pueden sincronizar objetos del directorio local con Microsoft 365 y gestionar principalmente el acceso a recursos cloud.

## Administración

En un entorno híbrido:

* Las cuentas originales y autoritativas se almacenan en **AD DS local**.
* Las identidades deben administrarse con las herramientas utilizadas para administrar AD DS.
* Las cuentas sincronizadas **no pueden administrarse en Microsoft Entra ID mediante el Microsoft 365 admin center o PowerShell**.

## Sincronización de directorios

La **sincronización de directorios** es el proceso de sincronizar identidades u objetos —usuarios, grupos, contactos y equipos— entre dos directorios diferentes.

En Microsoft 365 normalmente sincroniza entre:

* **Active Directory local**.
* **Microsoft Entra ID**.

También puede involucrar otros directorios, como:

* Bases de datos de RR. HH.
* Directorios LDAP.

Habitualmente la sincronización se realiza en una dirección, desde el entorno local hacia Microsoft Entra ID. Sin embargo, **Microsoft Entra Connect Sync** y **Microsoft Entra Cloud Sync** pueden escribir determinados objetos y atributos de vuelta al directorio local, creando una forma de sincronización bidireccional.

Microsoft Entra Connect Sync también puede proporcionar sincronización bidireccional de contraseñas y debe instalarse en un equipo dedicado dentro del entorno local.

### Beneficios de integrar directorios locales con Microsoft Entra ID

* **Identidad híbrida**: proporciona una identidad común entre servicios locales y cloud, incluyendo pertenencia consistente a grupos.
* **Single Sign-On (SSO)**: permite utilizar una identidad común para acceder a servidores y servicios.
* **Multifactor Authentication (MFA)**: requiere dos o más factores de autenticación:

  * Algo que el usuario conoce, como una contraseña.
  * Algo que posee, como un token físico o smart card.
  * Algo que es, como una huella digital o reconocimiento facial.
* **Microsoft Entra policies / Conditional Access**: permite aplicar acceso condicional basándose en:

  * Aplicación o recurso.
  * Dispositivo.
  * Identidad del usuario.
  * Ubicación de red.
  * MFA.
* **Identidad común**: la identidad de Microsoft Entra ID puede utilizarse para Microsoft 365, Intune, aplicaciones SaaS y aplicaciones que no son de Microsoft.
* **Common identity model**: los desarrolladores pueden crear aplicaciones que utilicen el modelo de identidad común e integrarlas con Active Directory local mediante servicios como Microsoft Entra App Proxy o Azure para aplicaciones cloud.

## Recomendaciones sobre autenticación

Microsoft recomienda **utilizar o habilitar Password Hash Synchronization (PHS)** independientemente del método de autenticación principal elegido.

### Alta disponibilidad y recuperación ante desastres

PTA y la autenticación federada dependen de infraestructura local:

* **PTA** requiere servidores y redes para los agentes de PTA.
* **Federación** requiere una infraestructura mayor, incluyendo servidores proxy en la red perimetral y servidores de federación internos.
* También dependen de los controladores de dominio para responder a las solicitudes de autenticación.
* Para evitar puntos únicos de fallo se deben implementar servidores redundantes.
* Muchos componentes requieren mantenimiento, y una planificación incorrecta puede provocar interrupciones.

### Resistencia ante una interrupción del entorno local

Una interrupción del entorno local causada por un ciberataque o desastre puede impedir el acceso a las aplicaciones cloud.

Las organizaciones que habilitaron PHS junto con PTA o federación pueden utilizar posteriormente PHS como método principal de autenticación y recuperar el acceso a Microsoft 365 aunque el entorno local esté fuera de servicio.

Las organizaciones que no habilitaron PHS pueden perder el acceso a las aplicaciones cloud hasta restaurar su infraestructura de identidad local.

### Protección de identidades

**Microsoft Entra Identity Protection**, con Microsoft Entra Premium P2, analiza continuamente Internet en busca de listas de usuarios y contraseñas comprometidas disponibles para actores maliciosos.

Microsoft Entra ID puede utilizar esta información para detectar credenciales comprometidas.

Por ello, Microsoft recomienda habilitar **PHS independientemente del método de autenticación utilizado**, incluso con autenticación federada o PTA.

Identity Protection puede presentar las credenciales filtradas en un informe y permitir que las organizaciones bloqueen a los usuarios o les obliguen a cambiar sus contraseñas cuando intentan iniciar sesión con credenciales filtradas.

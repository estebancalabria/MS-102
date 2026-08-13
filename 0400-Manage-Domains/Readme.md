# Introduction

Este módulo proporciona información sobre cómo una organización puede implementar sus servicios de dominio. Se centra específicamente en cómo agregar dominios personalizados a Microsoft 365.

Una organización puede necesitar varios nombres de dominio para diferentes propósitos. Por ejemplo, puede querer agregar una escritura diferente del nombre de su empresa porque los clientes ya la utilizan y sus comunicaciones no llegaban correctamente.

Los dominios personalizados permiten a las empresas utilizar su propia identidad de marca en correos electrónicos y cuentas. Este diseño permite a los clientes verificar quién les está enviando un correo electrónico (por ejemplo, **@contoso.com**).

En este módulo se examinan las consideraciones que deben abordarse al planificar un nuevo dominio en Microsoft 365, incluidos los requisitos de DNS del dominio.

También se revisan los pasos que deben seguirse y los factores que deben considerarse para agregar y configurar un nuevo dominio. Estos pasos incluyen la planificación de las zonas DNS y de los requisitos de registros DNS en un dominio personalizado.

# Plan a custom domain for your Microsoft 365 deployment

Existen varios factores que una organización debe considerar al planificar la incorporación de dominios personalizados a Microsoft 365. Estos factores pueden variar según la suscripción de Microsoft 365 que seleccione.

## Factores de planificación

| Factor                        | Consideraciones                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Multiple domains**          | Una organización debe planificar agregar el dominio principal que utiliza actualmente (por ejemplo, **adatum.com** para Adatum Corporation). También debe agregar cualquier otro dominio que utilice para mensajes de correo electrónico dentro de la organización. Este escenario es común cuando la empresa en general es un grupo empresarial. También es común cuando una organización atraviesa un proceso de fusión y algunos empleados todavía tienen direcciones de correo electrónico alternativas.                   |
| **Subdomains**                | Una organización puede querer registrar subdominios. Los planes Microsoft 365 Business Premium y Enterprise permiten agregar subdominios bajo el dominio raíz. Por ejemplo, dentro del dominio raíz **adatum.com** de Adatum Corporation, la empresa agregó un subdominio específico para el departamento de Ventas denominado **sales.adatum.com**.                                                                                                                                                                           |
| **Domain numbers**            | Una organización puede registrar hasta 900 dominios con Microsoft 365.                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| **Domain adding order**       | Los dominios raíz deben agregarse antes que los subdominios. En el ejemplo anterior, el dominio raíz **adatum.com** debe registrarse antes de agregar el subdominio **sales.adatum.com**.                                                                                                                                                                                                                                                                                                                                      |
| **DNS record hosting**        | Los servidores DNS de una organización o un proveedor de alojamiento externo pueden alojar los registros DNS.                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **Access to the DNS console** | Una organización debe consultar con su proveedor de alojamiento DNS sobre el nivel de acceso que tiene a la consola DNS. Para configurar sus servicios de Microsoft 365, una organización debe tener acceso para agregar registros **A**, **CNAME**, **TXT**, **MX** y **SRV**. Si el proveedor de alojamiento DNS no proporciona ese nivel de acceso, la organización puede tener que enviar una solicitud al proveedor de alojamiento DNS para cambiar los registros DNS necesarios para su implementación de Microsoft 365. |
| **Not registering DNS**       | Es poco frecuente que una organización no quiera registrar un dominio DNS con Microsoft 365. Sin embargo, ocasionalmente sucede. Por ejemplo, una organización puede querer un servicio de correo electrónico y directorio separado para sus usuarios de Microsoft 365. Un posible escenario es una universidad que quiere alojar a sus profesores en el entorno local y tener a los estudiantes en Microsoft 365 con un nombre de dominio diferente.                                                                          |
| **Not changing all records**  | Una organización puede no querer cambiar todos los registros DNS para que apunten a Microsoft 365. Una unidad posterior de este módulo identifica cómo gestionar el proceso de verificación cuando no se cambian todos los registros DNS.                                                                                                                                                                                                                                                                                      |

# Plan the DNS zones for a custom domain

Una configuración de zona DNS disponible públicamente es fundamental durante la implementación de Microsoft 365 para las organizaciones que desean utilizar dominios personalizados, tanto en una implementación híbrida como en un entorno exclusivamente en la nube.

Al configurar Microsoft 365 con dominios personalizados, el Domain Name System (DNS) desempeña un papel fundamental para permitir el funcionamiento correcto de diversos servicios y características, como correo electrónico, SharePoint, Teams y otras aplicaciones de Microsoft 365.

Una zona DNS disponible públicamente es necesaria para publicar los registros DNS requeridos que asocian el dominio personalizado con los servicios de Microsoft 365.

## Razones para disponer de una zona DNS pública

### Domain Verification

Durante la implementación de Microsoft 365, se debe verificar la propiedad del dominio personalizado. Este proceso normalmente implica agregar un registro **TXT** o **CNAME** específico a la zona DNS del dominio personalizado. La zona DNS debe ser accesible públicamente para que el proceso de verificación tenga éxito.

### Email Delivery

Si se desea utilizar Microsoft 365 para servicios de correo electrónico con el dominio personalizado, los registros DNS deben configurarse correctamente. Esto incluye configurar registros **MX (Mail Exchanger)** que especifican los servidores de correo responsables de aceptar correo electrónico en nombre del dominio.

Estos registros MX deben publicarse en la zona DNS disponible públicamente para garantizar la correcta entrega del correo electrónico.

### Autodiscover and Federation

Microsoft 365 depende de la funcionalidad de autodiscover para configurar automáticamente los clientes de correo electrónico y establecer la federación para determinadas características, como el inicio de sesión único (**SSO**).

Estos procesos requieren agregar registros DNS específicos, como registros **Autodiscover** y registros **Federation**, a la zona DNS disponible públicamente.

### Web Services and Applications

Si una organización utiliza aplicaciones web o servicios personalizados alojados dentro de Microsoft 365, es necesario configurar correctamente el DNS. Esto incluye crear registros DNS relevantes, como registros **CNAME** o **A**, para apuntar el dominio personalizado a los servicios web o aplicaciones correctos.

Tanto en implementaciones híbridas como en entornos exclusivamente en la nube, una zona DNS disponible públicamente es fundamental porque permite que entidades externas, como usuarios de Internet u otros servicios fuera de la red de la organización, resuelvan y accedan a los servicios de Microsoft 365 asociados con el dominio personalizado.

> **Important**
>
> Aunque la zona DNS debe estar disponible públicamente, todavía se pueden implementar medidas de seguridad, como **Domain Name System Security Extensions (DNSSEC)** y controles de acceso, para proteger la integridad y confidencialidad de los registros DNS y del dominio.

La primera parte de esta unidad de capacitación se centra en la planificación de zonas DNS en una configuración híbrida. Aunque los principios de planificación de zonas DNS para un entorno exclusivamente en la nube son similares a los de un entorno híbrido, existen algunas diferencias que se examinan en la sección final de esta unidad.

# DNS Zone planning in a hybrid deployment

En una implementación híbrida, una organización distribuye su infraestructura entre entornos locales y en la nube. En este escenario, la planificación de zonas DNS implica consideraciones que permiten la coexistencia y comunicación entre estos entornos.

Los principios de planificación de zonas DNS para una implementación híbrida incluyen:

### Understand the Hybrid Infrastructure

Se debe obtener una comprensión clara de la infraestructura híbrida de la organización, incluida la red local y el entorno de nube.

Se deben identificar la estructura de dominios, el esquema de direccionamiento IP y la infraestructura DNS existente en ambos entornos.

### Namespace Integration

Se debe determinar cómo se integra el espacio de nombres DNS entre los entornos locales y en la nube.

Se debe decidir si se mantiene un único espacio de nombres o si se utilizan espacios de nombres separados para cada entorno.

Los enfoques habituales incluyen subdominios, como **cloud.example.com** para el entorno de nube e **internal.example.com** para el entorno local.

### DNS Forwarding

Se debe configurar el reenvío DNS entre los servidores DNS locales y el servicio DNS en la nube.

El reenvío DNS permite que las consultas DNS que no son autoritativas localmente se reenvíen al servicio DNS apropiado para su resolución. Este proceso garantiza una resolución de nombres fluida en toda la infraestructura híbrida.

### Split DNS

Las organizaciones deben considerar la implementación de **split DNS** para gestionar la resolución de nombres de manera diferente para usuarios internos y externos.

Este enfoque permite que los usuarios internos resuelvan recursos internos mediante servidores DNS internos, mientras que los usuarios externos resuelven los mismos recursos mediante servidores DNS públicos.

Split DNS proporciona seguridad y control sobre la resolución DNS de los recursos internos.

### DNS Synchronization

Se deben implementar mecanismos de sincronización DNS entre la infraestructura DNS local y el servicio DNS en la nube.

Esto garantiza que los cambios realizados en un entorno, como agregar o modificar registros DNS, se propaguen al otro entorno para mantener la coherencia y sincronización.

### Service Discovery

Se deben considerar los mecanismos de descubrimiento de servicios necesarios para las implementaciones híbridas.

Estos mecanismos incluyen soluciones de descubrimiento de servicios basadas en DNS, como registros **SRV (Service)**, o herramientas especializadas como **Azure Service Discovery**.

Estos mecanismos permiten que las aplicaciones y servicios se descubran dinámicamente y se comuniquen entre sí a través de la infraestructura híbrida.

### Security and Compliance

Las organizaciones deben implementar medidas de seguridad, como firewalls, **Domain Name System Security Extensions (DNSSEC)** y controles de acceso en los entornos DNS locales y en la nube.

Se deben cumplir las políticas de seguridad y las regulaciones que rigen la infraestructura híbrida de la organización.

### Monitoring and Troubleshooting

Se deben configurar capacidades de supervisión y solución de problemas para la resolución DNS en ambos entornos.

Estas características deben incluir la supervisión del tráfico DNS, la latencia y el estado, además de mecanismos de registro y alertas para identificar y abordar rápidamente los problemas relacionados con DNS.

Los principios específicos de planificación de zonas DNS en una implementación híbrida pueden variar según las soluciones DNS elegidas, la arquitectura de red y los requisitos de la organización.

Es importante consultar la documentación proporcionada por los proveedores de DNS y las guías de implementación híbrida relevantes para obtener instrucciones detalladas adaptadas al entorno específico.

# DNS zone planning for a custom domain

Una organización puede demostrar que es propietaria de una zona DNS si puede editar los registros dentro de esa zona.

Cuando una organización es propietaria de la zona DNS, el asistente de configuración de Microsoft 365 puede crear el tenant con el dominio personalizado de la organización, como **adatum.com**.

Durante la configuración, el asistente de configuración de Microsoft 365 indica a las organizaciones qué registros DNS deben agregar a la zona DNS pública.

Una vez que la organización configura la zona DNS siguiendo estas instrucciones, el software cliente, como Outlook o Skype for Business Client, utiliza servicios de autodiscover y resuelve los nombres de dominio personalizados con las direcciones IP de los servidores de Microsoft 365.

Este proceso permite que los equipos cliente de una organización se conecten a servicios de Microsoft 365, como Exchange Online o Skype for Business Online.

Las organizaciones utilizan zonas DNS internas configuradas en servidores DNS internos para que los clientes internos puedan resolver nombres de equipos y servicios.

También utilizan zonas DNS externas y públicas configuradas en servidores DNS accesibles desde Internet para que los clientes ubicados en Internet puedan resolver nombres de equipos y servicios.

Existen dos opciones para alojar la zona DNS de un dominio personalizado:

* Un proveedor externo, como GoDaddy, puede alojar la zona DNS del dominio personalizado. Este escenario permite a una organización administrar DNS mediante un portal web. Si utiliza el nombre para recursos locales, todavía necesita una forma de gestionar la resolución de nombres interna. Las empresas normalmente eligen alojar una zona DNS interna para el dominio.
* Alojar la zona DNS localmente mediante servidores DNS existentes o implementados. Este escenario permite que una organización tenga servidores DNS en la red perimetral para que los usuarios de Internet puedan resolver los recursos de dominio orientados a Internet de la organización. También se pueden utilizar servidores DNS internos para gestionar la resolución de nombres de los recursos de la red de área local.

Cuando una organización planifica las zonas DNS para un dominio personalizado, puede elegir entre los siguientes escenarios:

* Las zonas DNS internas y externas tienen nombres diferentes.
* Las zonas DNS internas y externas tienen el mismo nombre. Este escenario se denomina **"split brain DNS"** o, abreviadamente, **"split DNS"**.

# Internal DNS zones and external DNS zones have different names

Las empresas en este escenario pueden configurar su propio DNS interno para su dominio interno, como **adatum.local**.

Luego pueden utilizar un reenviador DNS en los servidores DNS internos para redirigir a un servidor de nombres externo las solicitudes de resolución de nombres para dominios externos.

Por ejemplo, una solicitud para **mail.adatum.local** se redirigiría a una dirección IP interna, como **192.168.20.10**.

Por el contrario, una solicitud para **mail.adatum.com** podría dirigirse a **131.107.43.19**, que es la dirección IP externa de la empresa para ese nombre de host.

Los clientes internos que se conectan a servicios de Microsoft 365 desde la red interna envían solicitudes de resolución a los servidores DNS locales.

A continuación, un servidor DNS local reenvía la solicitud del cliente al servidor DNS externo. El servidor DNS resuelve la solicitud y devuelve la respuesta al servidor DNS interno de la empresa.

Finalmente, el servidor DNS local reenvía la solicitud resuelta a los clientes internos.

# Internal DNS zones and external DNS zones have the same name

Este escenario se denomina **split brain DNS** o, abreviadamente, **split DNS**.

Split DNS es una configuración en la que los entornos DNS internos y externos proporcionan diferentes direcciones IP para solicitudes del mismo nombre de host.

La dirección IP proporcionada depende del servidor utilizado para la resolución de nombres.

Por ejemplo, si una solicitud para **mail.adatum.com** proviene del interior de la red **adatum.com**, la dirección devuelta puede ser **192.168.20.10**, una dirección IP privada.

Sin embargo, si un usuario conectado directamente a Internet realiza la misma solicitud para **mail.adatum.com**, la dirección IP devuelta puede ser **131.107.43.19**, una dirección IP pública.

Esta configuración se consigue creando una zona en el servidor DNS interno para **adatum.com**.

Cuando un cliente de la red interna solicita **mail.adatum.com**, el servidor DNS interno responde con la dirección IP correspondiente a ese host. Para ello, utiliza los registros **A (Address)** o **CNAME (common name)** que el servidor mantiene para esa zona.

No es necesario reenviar la solicitud de resolución de nombres a los servidores DNS externos.

Sin embargo, los clientes externos que intentan contactar con **mail.adatum.com** reciben una respuesta del servidor DNS externo que es autoritativo para esa zona.

Los clientes internos que se conectan a servicios de Microsoft 365 desde la red interna envían solicitudes de resolución a los servidores DNS locales.

Para que un servidor DNS local pueda resolver la solicitud hacia los servicios de Microsoft 365, las zonas DNS locales y las zonas DNS externas deben estar configuradas con los mismos registros solicitados por el asistente de configuración de Microsoft 365.

Una vez que las zonas DNS internas y externas están configuradas con los mismos registros, los clientes pueden conectarse a los servicios de Microsoft 365 tanto desde el interior de la empresa como a través de Internet.

# DNS zone planning when moving an entire tenant to the cloud

Las secciones anteriores de esta unidad se centraron en la planificación de zonas DNS internas en una configuración híbrida.

Las organizaciones también deben planificar las zonas DNS cuando trasladan todo su tenant a la nube.

Los principios de planificación de zonas DNS en un entorno exclusivamente en la nube son similares a los de un entorno híbrido, aunque existen otros aspectos que deben abordarse.

## Consideraciones clave

### Understand DNS Zones

Una zona DNS es una parte del espacio de nombres DNS que administra una organización o entidad específica. Normalmente representa un dominio o subdominio.

Antes de planificar las zonas DNS, se debe tener una comprensión clara de la estructura de dominios y los requisitos de la organización.

### Choose a DNS Provider

En un entorno exclusivamente en la nube, existe flexibilidad para elegir un proveedor DNS que se adapte mejor a las necesidades de la organización.

Microsoft Azure ofrece **Azure DNS**, un servicio de alojamiento DNS escalable y de alta disponibilidad.

También se pueden utilizar otros proveedores DNS, como **Amazon Route 53** o **Google Cloud DNS**.

### DNS Zone Hierarchy

Se debe establecer una jerarquía lógica para las zonas DNS basada en la estructura de dominios.

Esta jerarquía normalmente se alinea con la estructura de **Active Directory (AD)** de la organización, aunque también puede personalizarse según los requisitos específicos.

Se debe considerar la creación de zonas DNS independientes para diferentes dominios, subdominios o ubicaciones geográficas con el objetivo de administrarlos eficientemente.

### DNS Zone Design

Las zonas DNS deben diseñarse en función de los servicios y recursos alojados en la nube.

Se debe considerar la creación de zonas DNS independientes para diversos servicios en la nube, como aplicaciones web, bases de datos, máquinas virtuales y otros recursos.

Esta segregación ayuda en la administración eficiente, la seguridad y la delegación de registros DNS.

### DNS Record Types

Se deben identificar los diferentes tipos de registros DNS necesarios para los servicios basados en la nube.

Algunos tipos de registros comunes incluyen:

* **A records:** asignan un dominio o subdominio a una dirección IPv4.
* **AAAA records:** asignan un dominio o subdominio a una dirección IPv6.
* **CNAME records:** crean un alias para un dominio o subdominio, redirigiéndolo a otro dominio o subdominio.
* **MX records:** especifican los servidores de correo responsables de aceptar correo electrónico en nombre de un dominio.
* **TXT records:** permiten agregar información adicional o registros de verificación.

### DNS Zone Delegation

Si existen varias zonas DNS y se desea delegar el control a diferentes equipos o departamentos, se debe configurar la delegación de zonas de manera adecuada.

Esto permite que diferentes equipos administren sus propios registros DNS dentro de su zona delegada.

### DNS Security

Se debe garantizar que existan medidas de seguridad adecuadas para proteger las zonas DNS.

Se debe implementar **Domain Name System Security Extensions (DNSSEC)** para agregar una capa adicional de seguridad a la infraestructura DNS y evitar ataques relacionados con DNS.

### Monitoring and Maintenance

Se deben supervisar y mantener regularmente las zonas DNS para garantizar su integridad y rendimiento.

Se deben configurar herramientas de supervisión adecuadas para realizar un seguimiento de la resolución DNS, la latencia y el estado general.

Es esencial mantenerse actualizado con cualquier cambio o actualización del proveedor DNS para garantizar la compatibilidad y la seguridad.

Estos pasos proporcionan una guía general, pero es esencial que las organizaciones consideren sus requisitos específicos y consulten la documentación proporcionada por el proveedor DNS elegido para obtener instrucciones detalladas sobre la planificación de zonas en un entorno exclusivamente en la nube.

# Knowledge check

## Check your knowledge

### 1. Escenario

Como administrador de Microsoft 365 para Tailspin Toys, estás planificando una implementación de Microsoft 365.

Quieres agregar un nuevo dominio personalizado donde la zona DNS interna y la zona DNS externa tengan el mismo nombre.

Quieres diseñar una solución DNS para el nuevo dominio que permita la conectividad con Microsoft 365 y cumpla este requisito de DNS.

**¿Qué deberías hacer?**

* Configurar **split brain DNS**.
* Utilizar zonas DNS integradas con **Active Directory**.
* Utilizar una zona primaria para el dominio para uso externo y una zona secundaria que apunte a la zona primaria para uso interno.

# Plan the DNS record requirements for a custom domain

Cuando se configura un dominio personalizado en Microsoft 365, se deben configurar los registros DNS (Domain Name System) para una correcta administración del dominio y entrega de correo electrónico. Los registros DNS específicos que se deben agregar dependen de los servicios que se quieran utilizar con el dominio personalizado en Microsoft 365.

Después de que el asistente de configuración de Microsoft 365 verifica que la organización es propietaria del dominio personalizado, el administrador debe agregar otros registros DNS a la zona DNS personalizada. Estos registros deben permitir que los clientes de la organización localicen los servicios de Microsoft 365.

Cada zona DNS puede contener varios tipos diferentes de registros DNS que proporcionan distintos servicios de resolución de nombres.

* Si la organización aloja su propio servidor DNS externo, un administrador DNS debe agregar los registros DNS necesarios para proporcionar conectividad de los clientes a los servicios de Microsoft 365.
* Si un proveedor DNS aloja la zona DNS de la organización, los administradores deben agregar los registros DNS necesarios mediante la consola de administración correspondiente creada por el proveedor DNS. Algunos proveedores DNS, como GoDaddy, proporcionan configuración automatizada de registros DNS para Microsoft 365. Este diseño evita que las organizaciones tengan que crear manualmente sus registros DNS para Microsoft 365. Las organizaciones también pueden seleccionar la opción de permitir que Microsoft 365 configure y aloje los registros DNS.

Si se adquirió un dominio personalizado de un proveedor de alojamiento externo, se puede conectar a Microsoft 365 actualizando los registros DNS en la cuenta del registrador. Una vez que el dominio se agrega a Microsoft 365, permanece registrado con el proveedor donde se adquirió. Sin embargo, Microsoft 365 puede utilizarlo para las direcciones de correo electrónico (como **[user@yourdomain.com](mailto:user@yourdomain.com)**) y otros servicios.

Si no se agrega un dominio personalizado, las personas de la organización deben utilizar el dominio **onmicrosoft.com** para sus direcciones de correo electrónico hasta que se agregue.

> **Tip**
>
> Se debe agregar el dominio personalizado antes de agregar usuarios para evitar tener que configurarlos dos veces.

Si anteriormente se crearon usuarios y se desea cambiar su dominio, se deben seguir los pasos descritos en **Change your email address to use your custom domain using the Microsoft 365 admin center**.

Las siguientes secciones examinan cada uno de los registros DNS utilizados por Microsoft 365.

## External DNS records required for Microsoft 365 (core services)

Microsoft 365 requiere el registro **TXT**, que demuestra que la organización es propietaria del dominio. El sistema requiere este registro para todos los clientes.

Microsoft 365 solo requiere el registro **CNAME** para clientes de China que utilizan 21Vianet para operar Microsoft 365. 21Vianet es el mayor proveedor neutral de servicios de centros de datos de Internet en China.

El registro CNAME garantiza que Microsoft 365 pueda dirigir las estaciones de trabajo para autenticarse con la plataforma de identidad adecuada.

| Registro DNS                  | Propósito                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Valor a utilizar                                                                                                                                                                                                                                                                 | Se aplica a                        |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| **TXT (Domain verification)** | Microsoft 365 lo utiliza para verificar que la organización es propietaria del dominio. No afecta a ninguna otra cosa.                                                                                                                                                                                                                                                                                                                                                                   | **Host:** @ (o, para algunos proveedores de alojamiento DNS, el nombre del dominio). **TXT Value:** una cadena de texto proporcionada por Microsoft 365. El asistente de configuración del dominio de Microsoft 365 proporciona los valores utilizados para crear este registro. | Todos los clientes                 |
| **CNAME (Suite)**             | Microsoft 365 lo utiliza para dirigir la autenticación a la plataforma de identidad correcta. Este registro CNAME solo se aplica a Microsoft 365 operado por 21Vianet en China. Si el registro está presente y 21Vianet no opera el plan Microsoft 365 de la organización, los usuarios del dominio personalizado reciben un mensaje de error indicando que el dominio personalizado no está en el sistema. Como resultado, los usuarios no pueden activar su licencia de Microsoft 365. | **Alias:** msoid. **Target:** clientconfig.partner.microsoftonline-p.net.cn                                                                                                                                                                                                      | Solo clientes de 21Vianet en China |

## External DNS records required for email in Microsoft 365 (Exchange Online)

El correo electrónico en Microsoft 365 requiere varios registros diferentes. Todos los clientes de Microsoft 365 deben utilizar los siguientes registros DNS:

* **Autodiscover:** permite que los equipos cliente encuentren automáticamente Exchange y configuren correctamente el cliente.
* **MX:** indica a otros sistemas de correo dónde enviar el correo electrónico para el dominio de la empresa.
* **Sender policy framework (SPF):** los registros SPF son en realidad registros TXT utilizados por los sistemas de correo de los destinatarios para validar si el servidor que envía el correo electrónico es uno que la empresa autoriza. Este registro ayuda a prevenir problemas como la suplantación de correo electrónico y el phishing.

> **Note**
>
> Cuando una organización cambia su correo electrónico a Microsoft 365 actualizando el registro MX de su dominio, **todo el correo electrónico enviado a ese dominio comienza a llegar a Microsoft 365**.

Los clientes de correo electrónico que utilizan federación de Exchange también necesitan los registros CNAME y TXT indicados al final de la tabla.

| Registro DNS                    | Propósito                                                                                                                                                                                                                                                                              | Valor a utilizar                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **CNAME (Exchange Online)**     | Ayuda a los clientes de Outlook a conectarse fácilmente al servicio Exchange Online mediante el servicio Autodiscover. Autodiscover encuentra automáticamente el host correcto de Exchange Server y configura Outlook para los usuarios.                                               | **Alias:** Autodiscover. **Target:** autodiscover.outlook.com                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **MX (Exchange Online)**        | Envía el correo entrante del dominio de una organización al servicio Exchange Online de Microsoft 365. Una vez que el correo electrónico de la organización fluye hacia Exchange Online, la empresa debe eliminar los registros MX que apuntan al sistema anterior.                    | **Domain:** por ejemplo, contoso.com. **Target email server:** [MX token].mail.protection.outlook.com. **TTL:** 3600. **Preference/Priority:** menor que cualquier otro registro MX. Este valor garantiza que el sistema entregue el correo a Exchange Online, por ejemplo, 1 o "low". El [MX token] se obtiene desde el centro de administración de Microsoft 365, en **Domains**, seleccionando **Fix issues** para el dominio y luego **What do I fix?** en la sección **MX records**. |
| **SPF (TXT) (Exchange Online)** | Ayuda a una organización a evitar que otras personas utilicen su dominio para enviar spam u otros correos electrónicos maliciosos. Los registros SPF identifican los servidores que una organización autoriza para enviar correo electrónico desde su dominio.                         | Registros DNS externos requeridos para SPF.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| **TXT (Exchange federation)**   | Se utiliza para la federación de Exchange en implementaciones híbridas.                                                                                                                                                                                                                | **TXT record 1:** por ejemplo, contoso.com y el texto hash personalizado generado para la prueba del dominio, como Y96nu89138789315669824. **TXT record 2:** por ejemplo, exchangedelegation.contoso.com y el texto hash personalizado generado para la prueba del dominio, como Y3259071352452626169.                                                                                                                                                                                    |
| **CNAME (Exchange federation)** | Ayuda a los clientes de Outlook a conectarse fácilmente al servicio Exchange Online mediante Autodiscover cuando una organización utiliza la federación de Exchange. Autodiscover encuentra automáticamente el host correcto de Exchange Server y configura Outlook para los usuarios. | **Alias:** por ejemplo, Autodiscover.service.contoso.com. **Target:** autodiscover.outlook.com                                                                                                                                                                                                                                                                                                                                                                                            |

## External DNS records required for Microsoft Teams

Una organización debe realizar pasos específicos cuando utiliza **Microsoft 365 URLs and IP address ranges** para garantizar que su red esté configurada correctamente.

Estos registros DNS se aplican únicamente a tenants en modo **Teams-only**. Para tenants híbridos, se deben considerar las implicaciones DNS para organizaciones locales que se convierten en híbridas.

| Registro DNS             | Propósito                                                                                                                                                                             | Valor a utilizar                                                                                                                                                                                                                                                                                                         |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **SRV (Federation)**     | Permite que el dominio Microsoft 365 de una organización comparta características de mensajería instantánea (IM) con clientes externos mediante la habilitación de la federación SIP. | **Domain:** [domain]. **Service:** sipfederationtls. **Protocol:** TCP. **Priority:** 100. **Weight:** 1. **Port:** 5061. **Target:** sipfed.online.lync.com. Si el firewall o servidor proxy de la organización bloquea las búsquedas SRV en un DNS externo, se debe agregar este registro SRV al registro DNS interno. |
| **SRV (SIP)**            | Puede ser necesario si la organización tiene un tenant Teams-only que utiliza teléfonos de Skype for Business Online para Teams.                                                      | **Domain:** [domain]. **Service:** sip. **Protocol:** TLS. **Priority:** 100. **Weight:** 1. **Port:** 443. **Target:** sipdir.online.lync.com                                                                                                                                                                           |
| **CNAME (Lyncdiscover)** | Los tenants Teams-only requieren este registro para admitir cmdlets de PowerShell que todavía utilizan la infraestructura de Skype for Business Online para la administración.        | **Alias:** lyncdiscover.[domain]. **Target:** webdir.online.lync.com                                                                                                                                                                                                                                                     |

## External DNS records required for Microsoft 365 Single Sign-on

| Registro DNS | Propósito                                                                                                                                                                                                                                                                                                      | Valor a utilizar                                                                                                                                            |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **CNAME**    | Se utiliza para verificar la propiedad del dominio y configurar dominios personalizados. Normalmente apunta a un valor o token específico proporcionado por Microsoft. El registro CNAME se utiliza para la verificación del dominio y para dirigir el tráfico hacia los servicios adecuados de Microsoft 365. | **Name/Host:** el nombre o alias específico, como "autodiscover" o "msoid". **Target:** el dominio o nombre de host de destino proporcionado por Microsoft. |

## External DNS records required for Sender policy framework (SPF)

Los registros SPF son registros TXT que ayudan a evitar que otras personas utilicen el dominio de una organización para enviar spam u otros correos electrónicos maliciosos.

Los registros SPF identifican los servidores que una organización autoriza para enviar correo electrónico desde su dominio.

Sender Policy Framework (SPF) ayuda a prevenir la suplantación, pero existen técnicas de suplantación contra las que SPF no puede proteger.

Para protegerse contra estas técnicas, una vez configurado SPF, la organización debe configurar **DKIM** y **DMARC** para Microsoft 365.

Una organización solo puede tener un registro SPF. En otras palabras, solo puede tener un registro TXT que defina SPF para su dominio.

Ese único registro puede tener varias inclusiones diferentes, pero el total de búsquedas DNS resultantes no puede ser superior a **10**. Este diseño ayuda a prevenir ataques de denegación de servicio.

### Structure of an SPF record

Un registro SPF contiene las siguientes partes:

* La declaración de que es un registro SPF.
* Los dominios.
* Las direcciones IP que deberían enviar correo electrónico.
* Una regla de aplicación.

Un ejemplo de un registro SPF común para Microsoft 365 cuando solo se utiliza Exchange Online para el correo electrónico es:

```text
TXT Name @ Values: v=spf1 include:spf.protection.outlook.com -all
```

Un sistema de correo que recibe un correo electrónico del dominio de una organización consulta el registro SPF.

Si el servidor de correo que envió el mensaje era un servidor de Microsoft 365, el sistema de correo acepta el mensaje.

Sin embargo, si el servidor que envió el mensaje era el sistema de correo antiguo de la organización o un sistema malicioso en Internet, la comprobación SPF puede fallar y el sistema no entrega el mensaje.

Estas comprobaciones ayudan a prevenir mensajes de suplantación de identidad y phishing.

### Choose the correct SPF record structure

En ocasiones, una organización no utiliza únicamente Exchange Online para el correo electrónico de Microsoft 365, por ejemplo, cuando también utiliza correo electrónico originado desde SharePoint Online.

En este escenario, la organización debe utilizar la siguiente información para determinar qué incluir en el valor del registro.

> **Caution**
>
> Si se dispone de un escenario complejo que incluye, por ejemplo, servidores de correo perimetrales para gestionar el tráfico de correo a través del firewall, será necesario configurar un registro SPF más detallado.

| Número | Si utilizas...                                          | Propósito                                                                                            | Agregar estas inclusiones                                                                                                                                                                |
| ------ | ------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1**  | Todos los sistemas de correo electrónico (obligatorio)  | Todos los registros SPF comienzan con este valor.                                                    | **v=spf1**                                                                                                                                                                               |
| **2**  | Exchange Online (común)                                 | Utilizar únicamente con Exchange Online.                                                             | **include:** spf.protection.outlook.com                                                                                                                                                  |
| **3**  | Sistema de correo electrónico de terceros (menos común) |                                                                                                      | **include:** [sistema de correo electrónico como mail.contoso.com]                                                                                                                       |
| **4**  | Sistema de correo local (menos común)                   | Utilizar si se emplea Exchange Online Protection o Exchange Online junto con otro sistema de correo. | **ip4:** [0.0.0.0] **ip6:** [: : ] **include:** [mail.contoso.com]. El valor entre corchetes debe corresponder a otros sistemas de correo que envían correo electrónico para el dominio. |
| **5**  | Todos los sistemas de correo electrónico (obligatorio)  |                                                                                                      | **-all**                                                                                                                                                                                 |

# Create a custom domain in Microsoft 365

Cuando una organización tiene un nombre de dominio que desea agregar a Microsoft 365, el administrador o partner de Microsoft debe verificar primero que la organización es propietaria del dominio.

La propiedad del dominio puede ser problemática, especialmente si un exempleado registró el dominio con su información personal y posteriormente dejó la organización.

## Métodos para verificar información histórica del dominio

Uno de los métodos más comunes que las empresas utilizaban anteriormente para averiguar quién registró originalmente el dominio era consultar el registro **WHOIS** del dominio mediante un registro WHOIS de Internet, como who.is.

Sin embargo, la **Internet Corporation for Assigned Names and Numbers (ICANN)**, organización sin fines de lucro que supervisa y coordina diversos aspectos del sistema de nombres de dominio (DNS) de Internet, ya no exige que la información WHOIS esté disponible públicamente.

Por ello, consultar WHOIS puede no proporcionar una respuesta útil, aparte de verificar quién es el registrador.

Como alternativa, las organizaciones suelen utilizar alguno de los siguientes métodos:

### Historical WHOIS databases

Existen servicios que mantienen registros WHOIS históricos, permitiendo buscar información de registros anteriores aunque ya no esté disponible públicamente.

Algunos ejemplos incluyen servicios como **DomainTools' Domain History** o **Whois History**.

### Domain registrar

Contactar directamente al registrador actual del dominio puede proporcionar información.

El registrador puede proporcionar información histórica o indicar los pasos siguientes para obtener los datos del registro original.

### Domain transfer documentation

Las transferencias de dominio permiten mover un nombre de dominio de un registrador a otro.

El propietario del dominio normalmente inicia este proceso por diferentes razones, como mejores precios, mejores servicios o consolidación de la administración del dominio.

Cuando se produce una transferencia de dominio, la documentación de transferencia puede contener información sobre el registrante original.

Esta información normalmente está disponible para el propietario actual del dominio o para el registrador.

Se debe verificar que la organización tenga acceso administrativo para administrar el DNS del dominio.

Los diferentes proveedores de alojamiento DNS proporcionan distintos niveles de acceso a los registros DNS de un dominio alojado.

### Legal assistance

Cuando es fundamental determinar la información original de registro del dominio, puede ser necesario buscar asesoramiento legal.

Un abogado con experiencia en disputas de nombres de dominio o en derecho de propiedad intelectual puede orientar sobre el proceso legal y ayudar a obtener la información requerida.

## Verificación y configuración inicial

Después de verificar que una organización es propietaria del dominio, debe comprobar que puede realizar cambios en los registros DNS del dominio.

En ese momento, la organización debe agregar el dominio a Microsoft 365.

Para ello, normalmente debe seguir estos pasos:

### Access DNS Management

La organización debe disponer de acceso administrativo al sistema de administración DNS del dominio.

Este acceso puede realizarse mediante un registrador de dominios, un proveedor de alojamiento DNS o un servidor DNS interno dentro de la red de la organización.

### Identify DNS Management Method

La organización debe determinar el método o plataforma específica utilizada para administrar los registros DNS del dominio.

El método puede ser un panel de control basado en web proporcionado por el registrador o proveedor DNS, o puede implicar acceso directo al servidor DNS mediante una herramienta de administración o una interfaz de línea de comandos.

### Locate DNS Zone

La organización debe identificar la zona DNS correspondiente al dominio dentro del sistema de administración DNS.

Esta zona contiene los registros DNS que controlan cómo se resuelve el dominio en Internet.

### Make DNS Record Changes

La organización debe poder modificar los registros DNS dentro de la zona DNS.

Dependiendo del método de administración DNS, normalmente esto implica localizar el registro DNS relevante, como **MX**, **TXT**, **CNAME** u otros, y realizar los cambios necesarios en su configuración.

### Save and Publish Changes

Después de modificar un registro DNS, la organización debe guardar y publicar los cambios dentro del sistema de administración DNS.

Esta acción garantiza que los registros DNS actualizados se propaguen por toda la infraestructura DNS y sean efectivos.

### Verify DNS Record Propagation

Una vez que la organización cambia los registros DNS y los guarda, debe verificar que los registros DNS actualizados se hayan propagado.

La propagación DNS se refiere al tiempo que tarda un proceso denominado replicación DNS en distribuir los registros DNS actualizados entre los servidores DNS de todo el mundo.

Este período puede variar y normalmente tarda desde unos minutos hasta varias horas.

### Perform Microsoft 365 Domain Verification

Después de confirmar que los registros DNS se propagaron, la organización puede continuar con el proceso de verificación del dominio dentro del portal de administración de Microsoft 365.

Este proceso normalmente implica agregar un registro **TXT** o **CNAME** específico a la zona DNS del dominio para demostrar la propiedad y el control.

### Verify Domain Ownership

Una vez que la organización agrega el registro TXT o CNAME a la zona DNS, puede iniciar el proceso de verificación del dominio dentro del portal de administración de Microsoft 365.

Microsoft 365 intenta validar la presencia del registro DNS para confirmar la propiedad del dominio.

El proceso de verificación puede tardar algún tiempo, ya que el registro DNS puede necesitar propagarse a todos los servidores DNS.

Este proceso de verificación ayuda a garantizar una configuración correcta de los servicios de Microsoft 365 con el dominio personalizado.

## Tip

Si se necesita ayuda con estos pasos, se puede considerar trabajar con un especialista de Microsoft para pequeñas empresas.

Con **Business Assist**, la organización y sus empleados obtienen acceso permanente a especialistas en pequeñas empresas a medida que hacen crecer su negocio, desde la incorporación hasta el uso diario.

# Step 1: Add a TXT or MX record to verify you own the domain

## Recommended: Verify with a TXT record

Primero se debe demostrar que se es propietario del dominio personalizado que se desea agregar a Microsoft 365.

1. Iniciar sesión en el centro de administración de Microsoft 365.
2. En el panel de navegación izquierdo, seleccionar **Show all**, luego **Settings** y después **Domains**.
3. En una nueva pestaña o ventana del navegador, iniciar sesión en el proveedor de alojamiento DNS y localizar dónde se administran las configuraciones DNS, por ejemplo **Zone File Settings**, **Manage Domains**, **Domain Manager** o **DNS Manager**.
4. Ir a la página DNS Manager del proveedor y agregar al dominio el registro TXT indicado en el centro de administración.
5. Agregar este registro no afecta al correo electrónico existente ni a otros servicios. Se puede eliminar de forma segura una vez conectado el dominio a Microsoft 365.

### Ejemplo

```text
TXT Name: @
TXT Value: MS=ms######## (unique ID from the admin center)
TTL: 3600 (or your provider default)
```

Guardar el registro, volver al centro de administración y seleccionar **Verify**.

Normalmente los cambios de registros tardan alrededor de **15 minutos** en registrarse, aunque en ocasiones pueden tardar más.

Se debe dar tiempo y realizar varios intentos para que Microsoft 365 detecte el cambio.

Cuando Microsoft 365 encuentra el registro TXT correcto, se verifica que la organización es propietaria del dominio.

## Verify with an MX record

Si el registrador no admite agregar registros TXT, se puede verificar la propiedad del dominio agregando un registro MX.

1. Iniciar sesión en el centro de administración de Microsoft 365.
2. En el panel de navegación izquierdo, seleccionar **Show all**, luego **Settings** y después **Domains**.
3. En una nueva pestaña o ventana del navegador, iniciar sesión en el proveedor de alojamiento DNS y localizar dónde se administran las configuraciones DNS, por ejemplo **Zone File Settings**, **Manage Domains**, **Domain Manager** o **DNS Manager**.
4. Ir a la página DNS Manager del proveedor y agregar al dominio el registro MX indicado en el centro de administración.

> **Important**
>
> La prioridad de este registro MX debe ser la más alta de todos los registros MX existentes para el dominio. De lo contrario, puede interferir con el envío y recepción de correo electrónico.
>
> Se debe eliminar este registro tan pronto como finalice la verificación de la propiedad del dominio.

Al crear el registro MX, se deben configurar los siguientes campos:

```text
Record Type: MX
Priority: Set to any large value not used already.
Host Name: @
Points to address: Copy the value from the admin center and paste it here.
TTL: 3600 (or your provider default)
```

Cuando Microsoft 365 encuentra el registro MX correcto, se verifica que la organización es propietaria del dominio.

# Step 2: Add DNS records to connect Microsoft services

En una nueva pestaña o ventana del navegador, iniciar sesión en el proveedor de alojamiento DNS y localizar dónde se administran las configuraciones DNS, por ejemplo **Zone File Settings**, **Manage Domains**, **Domain Manager** o **DNS Manager**.

Se deben agregar varios tipos diferentes de registros DNS dependiendo de los servicios que se quieran habilitar.

## Add an MX record for email (Outlook, Exchange Online)

Antes de comenzar, si los usuarios ya tienen correo electrónico con el dominio, como **[user@yourdomain.com](mailto:user@yourdomain.com)**, se deben crear sus cuentas en el centro de administración de Microsoft 365 antes de configurar los registros MX.

De esta manera, continúan recibiendo correo electrónico.

Después de actualizar el registro MX del dominio, todo el correo electrónico nuevo para cualquier persona que utilice el dominio llegará a Microsoft 365.

El correo electrónico que ya existe permanece en el proveedor de correo actual, a menos que se decida migrar el correo electrónico y los contactos a Microsoft 365.

Cuando se agrega un dominio en el centro de administración de Microsoft 365, se inicia el **Domain setup wizard**. El asistente proporciona la información necesaria para crear el registro MX.

En el sitio web del proveedor de alojamiento, se debe agregar un nuevo registro MX.

Los campos deben configurarse de la siguiente manera:

```text
Record Type: MX
Priority: Set to the highest value available, typically 0.
Host Name: @
Points to address: Copy the value from the admin center and paste it here.
TTL: 3600
```

> **Note**
>
> Exchange Online solo admite valores TTL inferiores a **6 horas (21.600 segundos)**.

Guardar el registro y eliminar cualquier otro registro MX.

Los dominios públicos administrados en sus respectivos portales de proveedores deben apuntar a Microsoft 365 para recibir correos electrónicos y utilizarlos en Microsoft 365.

## Add CNAME records to connect other services (Teams, Exchange Online, MDM)

El asistente de configuración del dominio proporciona la información necesaria para crear el registro CNAME.

En el sitio web del proveedor de alojamiento, se deben agregar registros CNAME para cada servicio de Microsoft 365 que se quiera conectar.

Cada registro CNAME debe configurarse con los siguientes campos:

```text
Record Type: CNAME (Alias)
Host: Paste the values you copy from the admin center here.
Points to address: Copy the value from the admin center and paste it here.
TTL: 3600 (or your provider default)
```

## Add or edit an SPF TXT record to help prevent email spam (Outlook, Exchange Online)

Antes de comenzar, si ya existe un registro SPF para el dominio, no se debe crear uno nuevo para Microsoft 365.

En su lugar, se deben agregar los valores requeridos por Microsoft 365 al registro actual en el sitio web del proveedor de alojamiento, de modo que exista un único registro SPF que incluya ambos conjuntos de valores.

En el sitio web del proveedor de alojamiento, se debe editar el registro SPF existente o crear uno.

Los campos deben configurarse de la siguiente manera:

```text
Record Type: TXT (Text)
Host: @
TXT Value: v=spf1 include:spf.protection.outlook.com -all
TTL: 3600 (or your provider default)
```

Guardar el registro.

En este punto, se debe validar el registro SPF utilizando una de las herramientas de validación SPF.

> **Important**
>
> SPF está diseñado para ayudar a prevenir la suplantación, pero existen técnicas de suplantación contra las que SPF no puede proteger. Para protegerse contra estas técnicas, primero se debe configurar SPF y después DKIM y DMARC para Microsoft 365.

## Add SRV records for communications services (Teams, Skype for Business)

En el sitio web del proveedor de alojamiento, se deben agregar registros SRV para cada servicio de Microsoft 365 que se quiera conectar.

Cada registro SRV debe configurarse con los siguientes campos:

```text
Record Type: SRV (Service)
Name: @
Target: Copy the value from the admin center and paste it here.
Protocol: Copy the value from the admin center and paste it here.
Service: Copy the value from the admin center and paste it here.
Priority: 100
Weight: 1
Port: Copy the value from the admin center and paste it here.
TTL: 3600 (or your provider default)
```

Guardar el registro.

Los proveedores de alojamiento pueden imponer restricciones sobre los valores de los campos de los registros SRV.

### Name

Si el proveedor de alojamiento no permite establecer este campo en **@**, se debe dejar en blanco.

Este enfoque solo debe utilizarse cuando el proveedor tiene campos separados para los valores **Service** y **Protocol**.

### Service and Protocol

Si el proveedor de alojamiento no proporciona estos campos para los registros SRV, se deben especificar los valores **Service** y **Protocol** en el campo **Name** del registro.

Dependiendo del proveedor, el campo Name puede tener otro nombre, como **Host**, **Hostname** o **Subdomain**.

Para agregar estos valores, se debe crear una única cadena separando los valores con un punto.

Ejemplo:

```text
_sip._tls
```

### Priority, Weight, and Port

Si el proveedor de alojamiento no proporciona estos campos para los registros SRV, se deben especificar en el campo **Target**.

Dependiendo del proveedor, el campo Target puede tener otro nombre, como **Content**, **IP Address** o **Target Host**.

Para agregar estos valores, se debe crear una única cadena separando los valores con espacios y, en algunos casos, terminando con un punto.

Se debe consultar al proveedor si existe alguna duda.

Los valores deben incluirse en este orden:

**Priority, Weight, Port, Target**

Ejemplo 1:

```text
100 1 443 sipdir.online.lync.com.
```

Ejemplo 2:

```text
100 1 443 sipdir.online.lync.com
```

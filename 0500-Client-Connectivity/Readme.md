# Conectividad de clientes con Microsoft 365

## Introducción

Este módulo aborda cómo los clientes se conectan a Microsoft 365, incluyendo la resolución de nombres, la configuración de Outlook, el uso de Autodiscover, los protocolos de conectividad y las técnicas para solucionar problemas de conectividad.

## Configuración automática de Outlook con Autodiscover

Microsoft Outlook incluye **Autodiscover**, una funcionalidad que configura automáticamente Outlook para conectarse a Exchange Online sin configurar manualmente los parámetros de conexión. Al iniciar Outlook por primera vez, el usuario proporciona su dirección de correo de Microsoft 365 y contraseña.

Para que Autodiscover funcione correctamente, deben configurarse los registros DNS apropiados durante la configuración del tenant de Microsoft 365.

### Proceso de conexión inicial

1. El usuario de Outlook introduce su dirección de correo y contraseña.
2. Mediante la dirección de correo y el registro **Autodiscover** del DNS público, el cliente localiza el servicio Autodiscover de Microsoft 365.
3. El cliente proporciona su dirección SMTP y contraseña para autenticarse con el servicio Autodiscover.
4. El cliente solicita los parámetros de conexión correspondientes.
5. Microsoft 365 proporciona los parámetros en formato de información de configuración **XML**.
6. Outlook descarga la información y la aplica a sus parámetros de conexión.
7. Outlook se conecta a **Exchange Online** en Microsoft 365.

## Registros DNS necesarios para la configuración de clientes

Outlook y otros clientes relacionados con Office utilizan **Autodiscover** para localizar automáticamente servicios en Microsoft 365. Para ello, la organización debe configurar los registros DNS correspondientes en los servidores DNS públicos de Internet.

* Si el espacio de nombres DNS interno es diferente del espacio de nombres DNS de Internet, por ejemplo **adatum.local** y **adatum.com**, los servidores DNS internos reenvían las consultas de los clientes a los servidores DNS de Internet.
* En configuraciones **split-brain DNS**, donde los espacios de nombres internos y externos son iguales, por ejemplo **adatum.com**, tanto los servidores DNS internos como los de Internet deben resolver los registros Autodiscover de Microsoft 365.

### Registros Autodiscover

| Registro DNS                    | Propósito                                                                                                                                                         | Valor                                                                                            |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| **CNAME (Exchange Online)**     | Permite que Autodiscover configure Outlook para los usuarios.                                                                                                     | **Alias:** Autodiscover<br>**Destino:** autodiscover.outlook.com                                 |
| **CNAME (Exchange Federation)** | Permite que Autodiscover configure Outlook en escenarios de federación de Exchange. Es opcional, pero necesario para una configuración híbrida con Microsoft 365. | **Alias:** por ejemplo, Autodiscover.service.adatum.com<br>**Destino:** autodiscover.outlook.com |

El dominio de la dirección de correo del usuario se resuelve mediante DNS. Luego se produce la redirección a Exchange Online, que devuelve al cliente Outlook el archivo **Autodiscover.xml** con toda la información de configuración.

El portal de **Microsoft 365** proporciona al administrador los registros DNS necesarios para la configuración inicial. Algunos proveedores DNS, como GoDaddy, permiten que Microsoft 365 cree automáticamente todos los registros necesarios.

## Configuración de clientes Outlook

Al conectarse a Microsoft 365, los usuarios proporcionan su dirección de correo y contraseña la primera vez que inician Outlook. **Autodiscover** configura automáticamente Outlook para trabajar con Microsoft 365.

### Protocolos de conectividad

La conectividad de Outlook con Exchange evolucionó de **RPC/TCP** a **RPC/HTTP** y posteriormente a **MAPI/HTTP**.

**MAPI sobre HTTP (MAPI/HTTP)** es el protocolo de transporte más reciente para la conectividad de Outlook y el único compatible con:

* Outlook y **Exchange Online** en Microsoft 365.
* **Exchange Server 2019**.
* **Hybrid Modern Authentication**.

MAPI/HTTP coloca los comandos MAPI directamente en paquetes HTTPS, proporcionando:

* **Menor latencia:** utiliza HTTP, un protocolo más ligero que RPC.
* **Mejor gestión de conexiones:** maneja mejor las conexiones de red inestables o intermitentes.
* **Mayor seguridad:** admite autenticación moderna como **OAuth**, evitando exponer las credenciales del usuario.
* **Mayor escalabilidad:** administra mejor grandes cantidades de usuarios, conexiones y solicitudes simultáneas.
* **Adaptabilidad a redes modernas:** funciona mejor con firewalls y proxies al utilizar HTTP.
* **Mejores diagnósticos:** facilita el análisis del tráfico HTTP y la identificación de problemas.

MAPI/HTTP también mejora la confiabilidad y estabilidad de las conexiones Outlook-Exchange al utilizar el modelo HTTP estándar. Permite mayor visibilidad de errores de transporte, mejor recuperación y una función explícita de **pausa y reanudación**.

### Beneficios adicionales de MAPI/HTTP

* Permite futuras innovaciones en autenticación mediante un protocolo basado en HTTP.
* Permite reconexiones más rápidas después de interrupciones porque solo deben reconstruirse las conexiones TCP, no las conexiones RPC.
* Facilita la recuperación después de situaciones como:

  * Hibernación del dispositivo.
  * Cambio de una red cableada a una inalámbrica o celular.
* Mantiene el contexto de sesión independiente de la conexión durante un período configurable, incluso cuando el usuario cambia de red.

Debido a estos beneficios y a que es el único protocolo compatible con Exchange Online, **MAPI/HTTP está habilitado de forma predeterminada en Microsoft 365**.

## Conectividad de Outlook en implementaciones cloud-only e híbridas

La forma en que Outlook se conecta depende del tipo de implementación.

### Implementación cloud-only

* Los clientes Outlook de una red interna se conectan a Microsoft 365 mediante registros DNS de **Autodiscover** ubicados en servidores DNS internos o de Internet.
* Los clientes Outlook conectados desde Internet utilizan los registros Autodiscover de los servidores DNS de Internet.

### Implementación híbrida

En una implementación híbrida, los clientes Outlook siempre deben conectarse inicialmente al servicio **Autodiscover** que se ejecuta en el Exchange Server de la organización.

Cuando el cliente está en la red interna:

1. Outlook localiza el Exchange Server mediante el **Autodiscover Service Connection Point (SCP)** almacenado en **Active Directory Domain Services (AD DS)**.
2. Outlook se conecta al Exchange Server.
3. Exchange determina si el buzón está en las instalaciones o en Microsoft 365.
4. Si el buzón está en Microsoft 365, Exchange proporciona a Outlook información de un dominio SMTP alternativo.
5. Outlook utiliza ese dominio para buscar en Internet el registro Autodiscover de Microsoft 365.
6. Outlook se conecta a Exchange Online.

Cuando el cliente está en Internet:

1. Outlook localiza el Exchange Server mediante el registro Autodiscover que apunta a los servicios de acceso de cliente de Exchange en la red interna.
2. Outlook se conecta al Exchange Server.
3. Exchange determina si el buzón está en las instalaciones o en Microsoft 365.

## Configuración de red

Los servicios de Microsoft 365 contienen múltiples **endpoints** utilizados por los clientes para conectarse a servicios como Exchange Online, Skype for Business Online y SharePoint Online.

Los endpoints de Microsoft 365 incluyen:

* **FQDN** (Fully Qualified Domain Names).
* Puertos.
* **URL**.
* Rangos de direcciones **IPv4 e IPv6**.

Las organizaciones que restringen el acceso de sus equipos a determinados recursos de Internet deben conocer todos los endpoints utilizados por Microsoft 365. Esta información permite configurar correctamente dispositivos de red como **routers y firewalls**, garantizando que los clientes puedan conectarse correctamente a los servicios de Microsoft 365.

## Solución de problemas de conectividad

Microsoft proporciona herramientas para analizar y solucionar problemas de conectividad en implementaciones de Microsoft 365.

### Microsoft Remote Connectivity Analyzer

**Microsoft Remote Connectivity Analyzer (RCA)** es una herramienta web para administradores de TI que permite solucionar problemas de conectividad en implementaciones de **Microsoft 365, Teams y Exchange Server**.

Simula distintos escenarios de inicio de sesión de clientes y flujo de correo. Cuando una prueba falla, proporciona errores y sugerencias para solucionar el problema.

RCA permite:

* Identificar problemas de conectividad entre clientes de correo y Exchange Server.
* Identificar problemas de conectividad entre clientes de correo y Microsoft 365.
* Solucionar problemas en implementaciones de Exchange Server y Microsoft 365.
* Identificar problemas comunes.
* Ejecutar pruebas desde equipos cliente dentro de la red corporativa.
* Generar registros con los pasos que tuvieron éxito y los que fallaron.
* Proporcionar sugerencias para resolver los problemas detectados.

### Aplicación Get Help

**Get Help** está integrada en Windows 10 y versiones posteriores y es la herramienta principal para solucionar problemas de Microsoft 365, Office y Outlook en un dispositivo.

Realiza diagnósticos automatizados, identifica problemas y aplica correcciones directamente. Si no puede resolver un problema, proporciona los siguientes pasos y permite conectarse con Microsoft Support.

Se puede abrir desde:

* **Inicio** → buscar **Get Help** → seleccionar **Get Help**.
* **Configuración** → **Sistema** → **Solucionar problemas** → **Otros solucionadores**.
* Enlace **Get Help** de la página principal de Configuración.

Puede solucionar problemas relacionados con:

* **Aplicaciones de Microsoft 365**

  * Errores durante la instalación de Office.
  * Problemas de activación de Microsoft 365.
  * Desinstalación de Office.
  * Problemas para iniciar sesión en Microsoft 365.
* **Outlook clásico**

  * Outlook no se inicia.
  * Problemas para configurar el correo de Microsoft 365.
  * Outlook solicita continuamente la contraseña.
  * Outlook muestra continuamente "Intentando conectar..." o "Desconectado".
  * Problemas con el calendario.
  * El complemento Teams Meeting no se carga en Outlook.
* **Otros**

  * Ejecución de diagnósticos avanzados de Outlook.
  * Comprobación de la conectividad de red con la red de Microsoft.

> **Nota:** Los solucionadores de Get Help admiten únicamente **Outlook clásico para Windows**. No admiten el nuevo Outlook para Windows ni el nuevo Teams.

Get Help ofrece correcciones automatizadas para muchos problemas. Los solucionadores realizan comprobaciones y acciones de recuperación, muestran los resultados y sugieren posibles soluciones. Los archivos de registro generados durante la sesión permiten analizar posteriormente los pasos realizados.

### Get Help Command-Line Tool

Para administradores de TI empresariales que necesitan ejecutar diagnósticos de forma remota o en varios dispositivos, Microsoft proporciona la herramienta de línea de comandos **GetHelpCmd.exe**.

Esta herramienta:

* Admite los mismos escenarios de solución de problemas que la aplicación gráfica Get Help.
* Puede ejecutarse mediante scripts de **PowerShell**.
* Puede implementarse mediante herramientas de administración como **Microsoft Intune**.

## Conectividad y resolución de problemas

* Configuración de resolución de nombres para garantizar que los clientes puedan conectarse sin intervención del usuario.
* Identificación de los registros **DNS** necesarios para Outlook y otros clientes relacionados con Office.
* Descripción de los protocolos de conectividad que permiten a Outlook conectarse a Microsoft 365.
* Comprensión de las diferencias de conectividad entre implementaciones **cloud-only** e **híbridas**.
* Identificación y configuración de los endpoints necesarios para permitir el acceso a los servicios de Microsoft 365.
* Uso de **Microsoft Remote Connectivity Analyzer** para diagnosticar problemas de conectividad.
* Uso de **Get Help** para realizar diagnósticos y aplicar correcciones automatizadas.
* Uso de **GetHelpCmd.exe** para diagnósticos remotos o en múltiples dispositivos.

# Deploy Microsoft 365 Apps for enterprise

## Introduction

Microsoft 365 Apps for enterprise puede instalarse:

* Mediante **self-service installation**, realizada por el usuario.
* Mediante **centralized deployment**, administrado por Microsoft 365 Administrator.

El módulo se enfoca principalmente en las opciones de despliegue centralizado y en su administración. Las herramientas de despliegue incluyen:

* Group Policy
* System Center Configuration Manager
* Windows Intune

También se aborda cómo habilitar o prohibir instalaciones self-service y cómo agregar Microsoft 365 Apps for enterprise a Microsoft Intune.

Con la instalación predeterminada, Office se actualiza automáticamente cuando Microsoft publica mejoras. Si se elimina la licencia de un usuario, las aplicaciones pasan a un **restricted functionality mode**.

Microsoft Intune permite distribuir Microsoft 365 Apps a dispositivos Windows 10 y posteriores y aplicar el **security baseline** de Microsoft 365 Apps for enterprise a usuarios, grupos o dispositivos.

## Microsoft 365 Apps for enterprise: funcionalidad

Microsoft 365 Apps for enterprise es una versión descargable de Office. Incluye:

* Microsoft Word
* Microsoft Excel
* Microsoft PowerPoint
* Microsoft Outlook
* Microsoft Access
* Microsoft Publisher
* Microsoft OneNote
* Microsoft Teams

**Access y Publisher no están incluidos en instalaciones para Mac.**

Utiliza **Click-to-Run** mediante streaming: la aplicación puede comenzar a utilizarse mientras continúa instalándose en segundo plano.

Aunque requiere Internet para la implementación, se instala y ejecuta localmente. No requiere conexión permanente, pero debe conectarse a Internet al menos cada **30 días** para validar automáticamente la licencia.

### Microsoft Visio y Microsoft Project

Algunos planes de Microsoft 365 permiten agregar Microsoft Visio y Microsoft Project. No forman parte de Microsoft 365 Apps for enterprise, aunque pueden descargarse desde el Microsoft 365 admin center.

Microsoft InfoPath 2013 y SharePoint Designer 2013 ya no forman parte de las ediciones actuales de Office. Están disponibles desde el Microsoft Download Center y no se actualizan más allá de 2013. Pueden requerir desinstalación y reinstalación al instalar Microsoft 365 Apps for enterprise.

## Self-service installation

Los usuarios pueden iniciar una instalación desde el Microsoft 365 portal seleccionando la opción de instalación de software.

Características:

* Requiere poca configuración administrativa.
* Ofrece menor control sobre el despliegue.
* Los administradores pueden deshabilitar todas las instalaciones self-service.
* Office se descarga desde Internet mediante Click-to-Run.
* No admite ubicaciones de origen locales.
* El usuario necesita una cuenta de Microsoft 365 con licencia para Microsoft 365 Apps for enterprise.
* El usuario necesita derechos administrativos sobre el equipo local.
* Las actualizaciones se instalan automáticamente en segundo plano desde Internet y este comportamiento no puede modificarse.

### Obstáculos para una instalación self-service

* **Falta de conocimientos de IT:** la configuración de despliegues mediante Configuration Manager u Office Deployment Tool puede resultar compleja. Microsoft recomienda el self-deployment desde el Microsoft 365 portal cuando se busca minimizar la configuración administrativa.
* **Limitaciones de ancho de banda:** Microsoft 365 Apps puede ocupar varios GB y múltiples descargas simultáneas pueden generar congestión y degradar el rendimiento de la red.
* **Ausencia de permisos de administrador local:** Click-to-Run requiere privilegios administrativos para instalar software y realizar cambios a nivel del sistema.

## Prohibir instalaciones para todos los usuarios

Microsoft 365 dispone de una configuración global que controla la descarga de aplicaciones móviles y de escritorio.

Ruta:

1. Microsoft 365 admin center → **...Show all**.
2. **Settings** → **Org Settings**.
3. En **Services**, seleccionar **Microsoft 365 installation options**.
4. Ir a la pestaña **Installation**.
5. En **Apps for Windows and mobile devices**, desactivar **Office (includes Skype for Business)**.
6. Seleccionar **Save**.
7. Cerrar el panel.

Al desactivar esta opción, los usuarios no pueden descargar Microsoft 365 Apps for enterprise.

# Deploy Microsoft 365 Apps with Configuration Manager

En un despliegue administrado, el administrador descarga primero Microsoft 365 Apps a la red local y posteriormente utiliza un mecanismo de push para desplegarlo.

Configuration Manager permite controlar la instalación, actualizaciones y configuraciones, y escala para entornos grandes.

Características:

* **Office Client Management dashboard** para desplegar Office y supervisar actualizaciones.
* Integración con **Office Customization Tool** para Click-to-Run.
* Eliminación de versiones existentes de Office durante el despliegue.
* Configuración de opciones como notificaciones de macros VBA, ubicaciones predeterminadas y formatos de archivo.
* **Peer cache** para reducir el impacto sobre redes con capacidad limitada.

Se recomienda utilizar la **Current branch** de Configuration Manager.

## Mejores prácticas

Crear dos aplicaciones Office de 64 bits:

* **Semi-Annual Enterprise Channel (Preview)** para el grupo piloto.
* **Semi-Annual Enterprise Channel** para el grupo amplio.

Crear dos colecciones:

* Grupo piloto → Semi-Annual Enterprise Channel (Preview).
* Grupo amplio → Semi-Annual Enterprise Channel.

Estas opciones pueden adaptarse a las necesidades de la organización.

## Paso 1: revisar la infraestructura

Recomendaciones:

* Utilizar la Current branch de Configuration Manager.
* Habilitar peer cache.
* Desplegar Office como aplicación mediante **Office Client Management dashboard** y **Office 365 Installer wizard**.

Requisitos:

* Los dispositivos cliente necesitan acceso a Internet para activar Microsoft 365 Apps.
* El equipo que ejecuta la consola de Configuration Manager requiere IE 11 o superior y acceso HTTPS por el puerto 443.
* El asistente utiliza `https://config.office.com`.
* Si existe un proxy, los usuarios deben poder acceder a esa URL.
* Con Enhanced Security Configuration habilitado, agregar a Trusted Sites:

  * `https://.office.com`
  * `https://.officeconfig.msocdn.com`

## Paso 2: revisar las colecciones

Configuration Manager representa los grupos de despliegue mediante **collections**.

Como práctica estándar:

* Collection piloto → Semi-Annual Enterprise Channel (Preview).
* Collection amplia → Semi-Annual Enterprise Channel.

En despliegues más complejos pueden utilizarse múltiples grupos.

## Paso 3: crear y desplegar Office al grupo piloto

1. Configuration Manager → **Software Library** → **Overview** → **Office 365 Client Management**.
2. Seleccionar **Office 365 Installer**.
3. En **Application Settings**, proporcionar nombre, descripción y ubicación de descarga, por ejemplo `\server\share`.
4. En **Office Settings**, seleccionar **Go to the Office Customization Tool**.
5. Configurar:

   * **Software:** Microsoft 365 Apps for enterprise.
   * **Update channel:** Semi-Annual Enterprise Channel (Preview).
   * **Languages:** paquetes de idiomas requeridos.
   * **Upgrades:** eliminar automáticamente versiones MSI anteriores.
   * **Display level:** Off.
   * **Automatically accept the EULA:** On.
   * **Application settings:** configuraciones como macros VBA, ubicaciones predeterminadas y formatos de archivo.
6. Seleccionar **Submit**.
7. Seleccionar **Yes** para desplegar.
8. Elegir la collection correspondiente.
9. Completar el asistente.

Por defecto, Configuration Manager no administra las actualizaciones de Office después del despliegue; Office se actualiza automáticamente.

## Paso 4: desplegar al grupo amplio

Después de probar Office en el grupo piloto, repetir el proceso utilizando **Semi-Annual Enterprise Channel** en lugar de **Semi-Annual Enterprise Channel (Preview)**.

## Paso 5: revisar los resultados

El **Microsoft 365 Client Management dashboard** permite revisar:

* Número de clientes Office 365.
* Versiones.
* Idiomas.
* Canales.

Ruta:

**Software Library → Overview → Office 365 Client Management**

El filtro **Collection** permite visualizar los datos de una colección específica.

Si los datos no aparecen, puede ser necesario habilitar hardware inventory y seleccionar la clase **Office 365 ProPlus Configurations**.

# Deploy Microsoft 365 Apps from the cloud

Microsoft 365 Apps for enterprise puede desplegarse desde el **Office Content Delivery Network (CDN)** utilizando el **Office Deployment Tool (ODT)**.

## Office Content Delivery Network

El CDN busca optimizar el rendimiento mediante:

* Distribución de objetos frecuentes mediante una red global de alta velocidad.
* Reducción del tiempo de carga.
* Acceso a los objetos desde ubicaciones cercanas al usuario.

El CDN utiliza un **origin**, que puede ser un sitio de SharePoint, una biblioteca de documentos o una carpeta accesible mediante URL.

### Public CDN

Está diseñado para:

* JavaScript.
* CSS.
* Web fonts.
* Imágenes no propietarias.

Los **public origins** son accesibles anónimamente. Cualquier persona con la URL puede acceder al contenido, por lo que deben utilizarse solamente para contenido genérico no sensible.

### Private CDN

Está diseñado para contenido privado, como:

* Bibliotecas de documentos de SharePoint Online.
* Sitios.
* Imágenes propietarias.

Utiliza tokens generados dinámicamente y solo permite acceso a usuarios con permisos sobre el contenido original. Los private origins solo pueden utilizarse para contenido de SharePoint Online y el acceso se realiza mediante redirección desde el tenant de SharePoint Online.

## Office Deployment Tool

El **Office Deployment Tool (ODT)** es una herramienta de línea de comandos para descargar y desplegar Microsoft 365 Apps.

Permite definir:

* Productos e idiomas.
* Comportamiento de las actualizaciones.
* Experiencia de instalación.

Está destinada principalmente a administradores de entornos empresariales con cientos o miles de equipos.

El ODT permite:

* Descargar archivos de Office.
* Instalar o eliminar Click-to-Run.
* Personalizar instalaciones.
* Aplicar políticas de actualización.

Antes de ejecutarlo, los usuarios deben tener privilegios de administrador local. Si no los tienen, deben utilizar las herramientas y procesos estándar de despliegue.

## Mejores prácticas con ODT

* Administrar las actualizaciones automáticamente.
* Crear dos paquetes de instalación de 64 bits:

  * Semi-Annual Enterprise Channel.
  * Semi-Annual Enterprise Channel (Preview).
* Cada paquete incluye las aplicaciones principales de Office.
* Crear otro paquete si se necesita la versión de 32 bits.
* Utilizar dos grupos:

  * Piloto → Semi-Annual Enterprise Channel (Preview).
  * Amplio → Semi-Annual Enterprise Channel.

Estas opciones pueden modificarse según las necesidades, incluyendo más grupos, otros canales, Visio y Project.

## Paso 1: descargar ODT

1. Crear `\Server\Share\M365` y asignar permisos de lectura.
2. Descargar la última versión del ODT en esa carpeta.
3. Ejecutar el archivo autoextraíble.

Incluye:

* `setup.exe`
* `configuration.xml`

## Paso 2: archivo de configuración para el grupo piloto

Se recomienda utilizar **Office Customization Tool**.

Configuración:

* **Products:** Microsoft 365 Apps for enterprise.
* **Update channel:** Semi-Annual Enterprise Channel (Preview).
* **Language:** paquetes necesarios.

  * **Match operating system:** instala los mismos idiomas del sistema operativo y usuarios.
  * **Fallback to the CDN:** utiliza el CDN como fuente alternativa para paquetes de idioma.
* **Installation:** Office Content Delivery Network (CDN).
* **Updates:** CDN + Automatically check for updates.
* **Upgrades:** eliminar automáticamente versiones MSI anteriores.
* **Display level:** Off.
* **Automatically accept the EULA:** On.
* **Application preferences:** configuraciones de Office.

Exportar como:

`config-pilot-SECP.xml`

en:

`\Server\Share\M365`

Los archivos de instalación y actualizaciones provienen de Semi-Annual Enterprise Channel (Preview).

## Paso 3: archivo de configuración para el grupo amplio

Utilizar las mismas configuraciones que el grupo piloto, excepto:

* **Update channel:** Semi-Annual Enterprise Channel.

Exportar como:

`config-broad-SEC.xml`

en:

`\Server\Share\M365`

## Paso 4: desplegar al grupo piloto

Ejecutar en los equipos cliente con privilegios administrativos:

```text
Server\Share\M365\setup.exe /configure Server\Share\M365\config-pilot-SECP.xml
```

Los usuarios necesitan permisos de lectura sobre el share y, si ejecutan directamente el comando, privilegios administrativos locales.

Normalmente este comando se incorpora a un script, batch u otro proceso automatizado, pudiendo ejecutarse con permisos elevados.

Si existen problemas:

* Verificar que se utiliza la última versión del ODT.
* Verificar la ubicación del archivo de configuración.
* Revisar el log en `%temp%`.

Después del despliegue se debe probar Office, especialmente con el hardware y los drivers de los dispositivos.

## Paso 5: desplegar al grupo amplio

Ejecutar:

```text
Server\Share\M365\setup.exe /configure Server\Share\M365\config-broad-SEC.xml
```

La diferencia respecto al grupo piloto es el archivo de configuración utilizado.

# Deploy Microsoft 365 Apps from a local source

Para desplegar Microsoft 365 Apps desde un origen local:

1. Descargar primero el software a una carpeta compartida de la red local.
2. Utilizar ODT para desplegar las aplicaciones desde esa carpeta.

## Comparación cloud vs. local

### Cloud

1. Descargar ODT.
2. Crear configuración para piloto.
3. Crear configuración para grupo amplio.
4. Desplegar al piloto.
5. Desplegar al grupo amplio.

### Local

1. Crear carpetas compartidas.
2. Descargar ODT.
3. Crear configuración para piloto.
4. Crear configuración para grupo amplio.
5. Descargar paquete de instalación del piloto.
6. Descargar paquete de instalación del grupo amplio.
7. Desplegar al piloto.
8. Desplegar al grupo amplio.

## Paso 1: crear carpetas compartidas

Crear:

* `\Server\Share\M365` → ODT y archivos de configuración.
* `\Server\Share\M365\SECP` → archivos de instalación de Semi-Annual Enterprise Channel (Preview).
* `\Server\Share\M365\SEC` → archivos de instalación de Semi-Annual Enterprise Channel.

Asignar permisos **Read** a los usuarios.

Pueden utilizarse múltiples ubicaciones para mejorar la disponibilidad y reducir el impacto sobre el ancho de banda. DFS puede utilizarse para replicar un share a múltiples ubicaciones.

## Paso 2: descargar ODT

Descargar la última versión del ODT en:

`\Server\Share\M365`

Ejecutar el archivo autoextraíble, que contiene `setup.exe` y un archivo de configuración de ejemplo.

## Paso 3: configuración para el piloto

Utilizar Office Customization Tool con:

* **Products:** Microsoft 365 Apps for enterprise.
* **Update channel:** Semi-Annual Enterprise Channel (Preview).
* **Language:** paquetes necesarios.

  * Match operating system.
  * Fallback to the CDN.
* **Installation:** Local source.
* **Source path:** `\Server\Share\M365\SECP`.
* **Updates:** CDN + Automatically check for updates.
* **Upgrades:** eliminar versiones MSI anteriores.
* **Display level:** Off.
* **Automatically accept the EULA:** On.
* **Application preferences:** configuraciones de Office.

Exportar como:

`config-pilot-SECP.xml`

Los archivos de instalación y actualizaciones provienen de Semi-Annual Enterprise Channel (Preview).

## Paso 4: configuración para el grupo amplio

Utilizar las mismas opciones, excepto:

* **Update channel:** Semi-Annual Enterprise Channel.
* **Installation:** Local source.
* **Source path:** `\Server\Share\M365\SEC`.

Exportar como:

`config-broad-SEC.xml`

La diferencia principal entre las configuraciones piloto y amplia es el canal de actualización y el origen local correspondiente.

## Paso 5: descargar paquete del piloto

Ejecutar ODT en modo download:

```text
Server\Share\M365\setup.exe /download Server\Share\M365\config-pilot-SECP.xml
```

Los archivos se descargan en:

`\Server\Share\M365\SECP`

Si la carpeta ya contiene parte de la versión de Office, ODT descarga solamente los archivos faltantes, reduciendo el consumo de ancho de banda.

Ante problemas:

* Verificar la última versión de ODT.
* Verificar la ubicación de la configuración.
* Revisar `%temp%`.

## Paso 6: descargar paquete del grupo amplio

Ejecutar:

```text
Server\Share\M365\setup.exe /download Server\Share\M365\config-broad-SEC.xml
```

Los archivos se descargan en:

`\Server\Share\M365\SEC`

## Paso 7: desplegar al piloto

Ejecutar:

```text
Server\Share\M365\setup.exe /configure Server\Share\M365\config-pilot-SECP.xml
```

El usuario necesita permisos de lectura sobre el share y, si ejecuta directamente el comando, privilegios administrativos locales.

El comando puede automatizarse mediante scripts, batch u otros procesos con permisos elevados.

## Paso 8: desplegar al grupo amplio

Ejecutar:

```text
Server\Share\M365\setup.exe /configure Server\Share\M365\config-broad-SEC.xml
```

El comando utiliza la configuración correspondiente al grupo amplio.

# Manage updates to Microsoft 365 Apps for enterprise

Click-to-Run utiliza un modelo optimizado de actualización con actualizaciones en segundo plano y de menor tamaño.

Cada **segundo martes del mes (Patch Tuesday / Update Tuesday)** Microsoft publica un nuevo build completo de Office.

A diferencia de instalaciones basadas en MSI, no se publican por separado security fixes, hotfixes, cumulative updates y service packs. El nuevo build contiene el conjunto completo de archivos.

Para instalaciones existentes, el cliente compara el build actual con el nuevo y descarga solamente las diferencias (**deltas**).

Las actualizaciones no interrumpen el trabajo del usuario. La aplicación utiliza el nuevo build cuando el usuario la cierra y vuelve a abrir.

## Opciones de actualización

### Automatic from cloud

Es la opción predeterminada.

* Las actualizaciones se descargan desde la nube.
* Una tarea diaria comprueba si existe un nuevo build.
* El cliente descarga automáticamente los deltas.

### Automatic from network

En despliegues administrados, los administradores pueden especificar una fuente interna mediante:

* Group Policy.
* `configuration.xml`.

Es una opción utilizada normalmente por organizaciones pequeñas o medianas.

### Rerun setup.exe mediante ESD

En organizaciones grandes, herramientas como Configuration Manager permiten mayor control sobre la programación.

Se puede volver a ejecutar:

```text
setup.exe /configure
```

El sistema compara la versión actual con el origen definido en `SourcePath` y descarga solamente los deltas.

El ESD permite controlar cuántos usuarios reciben un nuevo build durante un período determinado.

Para las actualizaciones administradas desde red o mediante ESD, se recomienda:

1. Descargar inicialmente el build actualizado a un share de prueba.
2. Aplicarlo a equipos de prueba o piloto.
3. Después de las pruebas, mover el build al share de producción.
4. Permitir que los equipos de producción se actualicen automáticamente.

Los clientes no pueden permanecer en un build desactualizado indefinidamente: después de **12 meses** deben descargar un build más reciente que tenga soporte de Microsoft.

Microsoft 365 Apps puede actualizarse mediante:

* Group Policy.
* File share.
* Microsoft 365.

## Administrar actualizaciones mediante configuration.xml

El archivo `configuration.xml` del ODT permite controlar el comportamiento de las actualizaciones.

Ejemplo:

```xml
<Updates Enabled="TRUE" UpdatePath="\\Server\Share\Office\" />
```

### Parámetros

* **Enabled:** si es `TRUE` (valor predeterminado), Click-to-Run detecta, descarga e instala automáticamente las actualizaciones.
* **UpdatePath:** especifica una ruta de red, local o HTTP que Click-to-Run utiliza como origen de actualizaciones. Si no se establece o se configura como `default`, utiliza el origen de Click-to-Run en Internet.
* **TargetVersion:** establece un número de build específico, por ejemplo `16.0.6366.2036`, para la siguiente actualización. Si no se establece o se configura como `default`, Click-to-Run actualiza a la versión más reciente disponible en el origen de Click-to-Run.

# Explore the update channels for Microsoft 365 Apps for enterprise

Los **update channels** permiten controlar con qué frecuencia los usuarios reciben nuevas características, actualizaciones de seguridad y actualizaciones no relacionadas con seguridad.

Las actualizaciones no relacionadas con seguridad incluyen correcciones de problemas conocidos y mejoras de estabilidad o rendimiento.

Existen tres canales principales:

* **Current Channel**
* **Monthly Enterprise Channel**
* **Semi-Annual Enterprise Channel**

## Current Channel

Proporciona las nuevas características de Office tan pronto como están disponibles.

* Normalmente recibe nuevas características al menos una vez al mes.
* No tiene un calendario fijo para las nuevas características.
* También recibe actualizaciones de seguridad y no relacionadas con seguridad durante el mes.
* Generalmente recibe dos o tres releases por mes, incluyendo una el segundo martes.

### Current Channel (Preview)

Es la versión de preview de Current Channel.

* Permite familiarizarse con las nuevas características antes de su lanzamiento en Current Channel.
* No tiene un calendario fijo.
* Generalmente recibe una nueva versión al menos una semana antes que Current Channel.
* Puede recibir varias actualizaciones no relacionadas con seguridad antes del lanzamiento a Current Channel.
* Microsoft recomienda desplegarlo a un grupo pequeño y representativo de usuarios.
* Permite identificar problemas antes del despliegue general y solicitar correcciones a Microsoft.
* Puede reducir la cantidad de actualizaciones no relacionadas con seguridad necesarias posteriormente en Current Channel.

## Monthly Enterprise Channel

Proporciona nuevas características de Office cada mes.

Microsoft recomienda este canal cuando una organización necesita **un único update mensual con un calendario predecible**.

* Las actualizaciones se publican el **segundo martes de cada mes**.
* Pueden incluir características, actualizaciones de seguridad y actualizaciones no relacionadas con seguridad.
* No existe un canal de preview dedicado.

Una organización puede hacer que un grupo representativo utilice la nueva versión cuando esté disponible en Office CDN y posteriormente desplegarla al resto de la organización durante varios días.

## Semi-Annual Enterprise Channel

Microsoft recomienda este canal para dispositivos que necesitan **pruebas extensivas** antes de recibir nuevas características.

Puede utilizarse cuando:

* Existen requisitos regulatorios, gubernamentales u otros requisitos empresariales.
* Los usuarios no pueden recibir nuevas características con una frecuencia mayor a dos veces al año.

Las actualizaciones se publican el **segundo martes del mes**.

* En **enero y julio**, pueden incluir características, actualizaciones de seguridad y actualizaciones no relacionadas con seguridad.
* En los demás meses, pueden incluir actualizaciones de seguridad y no relacionadas con seguridad.

### Semi-Annual Enterprise Channel (Preview)

Es el canal de preview de Semi-Annual Enterprise Channel.

* Permite familiarizarse con las nuevas características antes de su lanzamiento al canal Semi-Annual Enterprise.
* Microsoft publica nuevas características dos veces al año:

  * Segundo martes de marzo.
  * Segundo martes de septiembre.
* Esto proporciona **cuatro meses** antes de que esas características lleguen a Semi-Annual Enterprise Channel.
* Puede recibir actualizaciones de seguridad y no relacionadas con seguridad mensualmente, el segundo martes.
* Microsoft recomienda desplegarlo a un grupo pequeño y representativo.
* Permite detectar problemas antes del despliegue general.
* También proporciona cuatro meses para identificar problemas que Microsoft pueda corregir antes del lanzamiento al Semi-Annual Enterprise Channel.

Una vez que una versión llega a Semi-Annual Enterprise Channel, el proceso de aprobación de actualizaciones no relacionadas con seguridad es más riguroso.

## Recomendaciones de canales

* **Current Channel:** recomendado cuando se necesitan las características más nuevas tan pronto como estén disponibles.
* **Monthly Enterprise Channel:** recomendado cuando se necesita un calendario mensual predecible.
* **Semi-Annual Enterprise Channel:** recomendado para dispositivos que requieren pruebas extensivas antes de recibir nuevas características.

La elección del canal también depende de:

* Uso de ancho de banda.
* Capacitación y soporte de usuarios finales.
* Aplicaciones de línea de negocio.
* Otros requisitos organizacionales.

El uso de usuarios específicos para probar nuevas versiones es una parte importante de la administración continua de versiones en entornos empresariales.

## Configurar usuarios para los update channels

Los administradores de Microsoft 365 pueden aplicar los canales mediante:

### Microsoft 365 admin center

Ruta:

**Organization settings → Services → Office installation options**

Opciones:

* **As soon as updates are ready** → Current Channel.
* **Once a month** → Monthly Enterprise Channel.
* **Every six months** → Semi-Annual Enterprise Channel.

Microsoft recomienda **Current Channel**, es decir, recibir las actualizaciones tan pronto como estén disponibles.

Si una organización cambia de actualizaciones mensuales a actualizaciones cada seis meses, los usuarios perderán las actualizaciones correspondientes a futuras releases.

El Microsoft 365 admin center no ofrece una opción **Deferred Channel**.

### Office Deployment Tool

Mediante la versión de Office 2016 del ODT, se puede modificar `configuration.xml` para establecer:

* Current Channel.
* Monthly Enterprise Channel.
* Semi-Annual Enterprise Channel.

Diferentes usuarios pueden utilizar diferentes archivos `configuration.xml` para establecer distintos calendarios de actualización.

### Group Policy

Los archivos **Office Administrative Template** permiten configurar la rapidez con la que se proporcionan las actualizaciones.

Después de descargar los templates, se puede crear un **Group Policy Object** para definir el canal disponible para los usuarios.

Ruta:

**Configuration → Administrative Templates → Microsoft Office 2016 (Machine) → Updates**

Opciones:

* Current.
* Monthly Enterprise.
* Semi-Annual Enterprise.

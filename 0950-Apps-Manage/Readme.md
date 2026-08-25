# Resumen — Deploy Microsoft 365 Apps for enterprise

## Manage cloud apps using the Microsoft 365 Apps admin center

El **Microsoft 365 Apps admin center** permite administrar en la nube Microsoft 365 Apps for enterprise.

### Acceso

Desde **Microsoft 365 admin center**:

1. Seleccionar **...Show all**.
2. En **Admin centers**, seleccionar **All admin centers**.
3. Seleccionar **Office configuration**.

### Office cloud policy service

Permite aplicar configuraciones de políticas de Microsoft 365 Apps for enterprise en los dispositivos de los usuarios, incluso si el dispositivo no está unido a un dominio ni administrado.

Cuando el usuario inicia sesión en Microsoft 365 Apps for enterprise, las políticas se aplican al dispositivo. Algunas políticas también pueden aplicarse a **Office para la web**, tanto a usuarios autenticados como a quienes acceden anónimamente a documentos.

### Office Customization Tool

Permite crear archivos de configuración para implementar Office en organizaciones grandes. Estos archivos permiten definir:

* Aplicaciones e idiomas a instalar.
* Forma de actualizar las aplicaciones.
* Preferencias de las aplicaciones.

Los archivos pueden utilizarse con **Office Deployment Tool** para implementar una instalación personalizada.

### Microsoft 365 Apps health

Supervisa métricas de **confiabilidad y rendimiento** y proporciona orientación para optimizar y solucionar problemas de Microsoft 365 Apps en los dispositivos cliente.

Permite consultar información como:

* Tasa de bloqueos de aplicaciones.
* Tiempo de inicio.
* Rendimiento según la versión de Microsoft 365 Apps.

### Office Inventory

La página **Inventory** muestra información sobre el estado de las instalaciones de Office en los dispositivos de la organización.

Permite identificar problemas, como dispositivos que ejecutan compilaciones antiguas o no compatibles, y proporciona información sobre los complementos instalados.

Para un dispositivo específico se puede consultar:

* Información de hardware.
* Sistema operativo.
* Software de Office instalado.
* Complementos y macros.
* Último usuario que inició sesión.

### Security Update Status

La página **Security Update Status** permite comprobar qué dispositivos tienen instaladas las últimas actualizaciones de seguridad de Office.

También permite establecer un **objetivo de implementación**, indicando el porcentaje de dispositivos que se desea actualizar dentro de un período determinado.

El objetivo es únicamente para informes y seguimiento; **no crea políticas ni modifica los dispositivos**.

### Servicing profile

Los **servicing profiles** permiten entregar automáticamente actualizaciones mensuales de Office a usuarios o grupos específicos.

Al aplicar un perfil:

* Los dispositivos pasan automáticamente al **Monthly Enterprise Channel**.
* Las actualizaciones provienen del **Office Content Delivery Network (CDN)**.
* El servicing profile administra los dispositivos.

Las actualizaciones comienzan el **segundo martes de cada mes** y Microsoft las distribuye en oleadas para limitar el impacto en la red.

También permite:

* Pausar actualizaciones para investigar problemas.
* Establecer fechas límite de instalación.
* Definir fechas en las que no se pueden instalar actualizaciones.

---

## Add Microsoft 365 Apps for enterprise to Microsoft Intune

Antes de configurar, asignar, proteger o supervisar aplicaciones, es necesario agregarlas a **Microsoft Intune**.

Las aplicaciones administradas por Intune pueden:

* Implementarse.
* Configurarse.
* Protegerse.
* Actualizarse.

Intune admite diferentes tipos de aplicaciones y plataformas, incluyendo **iOS/iPadOS y Android**.

### Beneficios de administrar aplicaciones con Intune

* **Administración centralizada:** implementación y actualización desde una única consola.
* **Seguridad y cumplimiento:** aplicación de actualizaciones y configuraciones de cumplimiento.
* **Escalabilidad:** permite implementaciones a gran escala.
* **Experiencia de usuario:** aplicaciones consistentes y actualizadas.
* **Protección de datos:** políticas para proteger información sensible.
* **Amplio soporte de aplicaciones.**
* **Control de acceso:** permite determinar quién puede acceder a las aplicaciones.
* **Configuración de aplicaciones:** permite establecer configuraciones según las políticas de la organización.
* **Actualizaciones:** facilita las actualizaciones automáticas.

Casos en los que puede ser necesario administrar aplicaciones con Intune:

* Configurar aplicaciones con parámetros específicos.
* Proteger datos sensibles utilizados por una aplicación.
* Proteger el acceso a una aplicación.
* Supervisar aplicaciones para garantizar la protección de datos y mantenerlas actualizadas.

Antes de agregar aplicaciones a Intune se deben determinar:

* Requisitos de los usuarios, plataformas y capacidades necesarias.
* Si Intune administrará los dispositivos y sus aplicaciones o solamente las aplicaciones.
* Qué aplicaciones y capacidades necesita cada grupo de usuarios.

### Tipos de aplicaciones en Microsoft Intune

| Tipo                               | Instalación                                                     | Actualizaciones |
| ---------------------------------- | --------------------------------------------------------------- | --------------- |
| Apps from the store                | Intune instala la aplicación en el dispositivo                  | Automáticas     |
| Line-of-business (LOB)             | Intune instala la aplicación a partir del archivo proporcionado | Manuales        |
| Built-in apps                      | Intune instala la aplicación                                    | Automáticas     |
| Web apps                           | Intune crea un acceso directo en la pantalla principal          | Automáticas     |
| Apps from other Microsoft services | Intune crea un acceso directo en Company Portal                 | Automáticas     |

### Tipos específicos de aplicaciones

* **Android store apps:** seleccionar el tipo correspondiente e ingresar la URL de Google Play.
* **iOS/iPadOS store apps:** buscar y seleccionar la aplicación en Intune.
* **Microsoft store apps:** ingresar la URL de Microsoft Store.
* **Managed Google Play / Android Enterprise apps:** buscar y seleccionar la aplicación.
* **Microsoft 365 apps para Windows 10 y posteriores:** seleccionar Windows 10 y posteriores dentro de Microsoft 365 Apps.
* **Microsoft 365 apps para macOS:** seleccionar macOS dentro de Microsoft 365 Apps.
* **Microsoft Edge para Windows/macOS:** seleccionar el tipo correspondiente.
* **Android LOB:** archivo `.apk`.
* **iOS/iPadOS LOB:** archivo `.ipa`.
* **Windows LOB:** archivos `.msi`, `.appx`, `.appxbundle`, `.msix` o `.msixbundle`.
* **Built-in iOS/iPadOS y Android:** seleccionar la aplicación integrada.
* **Web apps:** ingresar una URL válida.
* **iOS/iPadOS web clip:** URL de la aplicación web.
* **macOS web clip:** URL de la aplicación web.
* **Windows web link:** URL de la aplicación web.
* **Cross-platform web apps:** URL de la aplicación web.
* **Android Enterprise system apps:** nombre, editor y paquete.
* **Windows app (Win32):** archivo `.intunewin`.
* **Enterprise App Catalog app (Win32):** seleccionar desde el catálogo y configurar información, comandos, requisitos y reglas de detección.
* **macOS LOB:** archivo `.pkg`.
* **macOS DMG:** archivo `.dmg`.
* **macOS PKG:** archivo `.pkg`.
* **Microsoft Defender for Endpoint para macOS:** seleccionar macOS y configurar la aplicación en Intune.

Para agregar una aplicación:

**Apps > All apps > Add**

Luego aparece **Select app type**, donde se selecciona el tipo de aplicación.

Una aplicación **LOB** se agrega mediante un archivo de instalación, por ejemplo `.ipa` para una aplicación iOS/iPadOS personalizada.

---

## Agregar Microsoft 365 Apps a dispositivos Windows 10/11 con Intune

Intune permite asignar e instalar Microsoft 365 Apps en dispositivos administrados con **Windows 10/11**. También permite instalar **Microsoft Project Online desktop client** y **Microsoft Visio Online Plan 2** si se poseen las licencias correspondientes.

Las aplicaciones Microsoft 365 disponibles aparecen como una única entrada en Intune.

### Consideraciones importantes

* Si existen aplicaciones Office `.msi`, se debe utilizar **Remove MSI** para desinstalarlas correctamente; de lo contrario, la instalación puede fallar.
* Las asignaciones múltiples de aplicaciones requeridas o disponibles **no son acumulativas**: una asignación posterior puede sobrescribir una anterior.
* Si una asignación posterior no incluye Word, por ejemplo, Word puede desinstalarse.
* Esta condición no se aplica a Visio ni Project.
* Los dispositivos deben ejecutar **Windows 10/11 Creators Update o posterior**.
* Intune admite agregar aplicaciones Office únicamente desde la suite **Microsoft 365 Apps**.
* Si hay aplicaciones Office abiertas durante la instalación, esta puede fallar y los usuarios pueden perder datos no guardados.
* El método no es compatible con **Windows Home, Windows Team, Windows Holographic ni Windows Holographic for Business**.
* No se admite instalar aplicaciones Microsoft 365 de escritorio desde Microsoft Store si Microsoft 365 Apps ya fue implementado mediante Intune; hacerlo puede provocar pérdida o corrupción de datos.
* No se admiten múltiples implementaciones de Microsoft 365; solo una se entrega al dispositivo.
* Se debe seleccionar la arquitectura **32 bits o 64 bits**. La versión de 32 bits puede instalarse en dispositivos de 32 o 64 bits; la de 64 bits requiere un dispositivo de 64 bits.
* Si se selecciona **Remove MSI**, se eliminan todas las aplicaciones Office MSI existentes, no solo las seleccionadas para la instalación.
* Al reinstalar Office, los usuarios reciben automáticamente los mismos paquetes de idioma que tenían en la instalación MSI anterior.
* En dispositivos aprovisionados mediante **Autopilot**, si Microsoft 365 Apps se implementará como aplicación supervisada durante el proceso **Enrollment Status Page (ESP)**, Microsoft recomienda implementarlo como aplicación **Win32**.
* La instalación del tipo **Microsoft 365 Apps (Windows 10 and later)** no es administrada por **Intune Management Extension (IME)**.
* Durante ESP puede producirse una concurrencia de instalaciones entre Microsoft 365 Apps y una aplicación Win32, provocando el fallo de ESP.

### Proceso de implementación

1. Iniciar sesión en **Microsoft 365 admin center**.
2. Seleccionar **Show all**.
3. En **Admin centers**, seleccionar **Endpoint Manager** para abrir Microsoft Intune admin center.
4. Seleccionar **Apps**.
5. En **Apps | Overview**, utilizar **All apps** o una plataforma específica y seleccionar **+Add**.
6. En **Select app type**, seleccionar **Windows 10 and later** y luego **Select**.
7. En **Add Microsoft 365 Apps > App Suite Information**, configurar:

   * **Suite Name**
   * **Suite Description**
   * **Publisher:** Microsoft
   * **Category:** opcional.
   * **Featured App:** opcional.
8. Seleccionar **Next**.
9. En **Configure app suite**, configurar:

   * **Architecture:** 32 o 64 bits.
   * **Default file format:** Office Open Document Format u Office Open XML Format.
   * **Update Channel:** Current Channel, Monthly Enterprise Channel, Semi-Annual Enterprise Channel o Semi-Annual Enterprise Channel (Preview).
   * **Languages:** idiomas requeridos.
   * **Remove MSI:** eliminar versiones MSI existentes.
10. Seleccionar **Next**.
11. En **Assignments**, asignar la suite a los usuarios, grupos o dispositivos correspondientes.
12. Seleccionar **Next**.
13. En **Review + create**, revisar la configuración y seleccionar **Create**.

---

## Deploy Microsoft 365 Apps for enterprise security baseline

Una **security baseline** es una configuración recomendada por Microsoft para clientes empresariales. Sirve como punto de partida para que los administradores evalúen y equilibren seguridad y productividad y ajusten la configuración según sus necesidades.

Las security baselines están disponibles para:

* Windows 10 o posterior.
* Microsoft Defender for Endpoint.
* Microsoft Edge.
* Windows 365.
* Microsoft 365 Apps for enterprise.

La **Microsoft 365 Apps for enterprise security baseline** puede implementarse mediante Microsoft Intune para aplicar configuraciones de seguridad recomendadas a las aplicaciones.

Una security baseline en Intune funciona como una plantilla con múltiples configuraciones de dispositivos que pueden asignarse a:

* **Grupos específicos de dispositivos.**
* **Grupos o usuarios específicos.**
* También permite excluir grupos determinados.

### Beneficios

* **Seguridad mejorada:** aplicación de buenas prácticas de seguridad, MFA para acceder a Microsoft 365 Apps y políticas DLP para proteger información sensible.
* **Cumplimiento:** aplicación consistente de configuraciones de seguridad para cumplir estándares y políticas organizacionales.
* **Administración simplificada:** administración centralizada de configuraciones desde Intune.
* **Experiencia de usuario:** experiencia consistente y segura, con actualizaciones automáticas que mantienen las aplicaciones protegidas sin intervención manual.

### Crear una security baseline

1. Iniciar sesión en **Microsoft 365 admin center**.
2. Seleccionar **Show all**.
3. En **Admin centers**, seleccionar **Endpoint Manager** para abrir Microsoft Intune admin center.
4. Seleccionar **Endpoint security**.
5. En **Endpoint security | Overview**, seleccionar **Security baselines**.
6. Seleccionar **Microsoft 365 Apps for Enterprise Security Baseline**.
7. En **Profiles**, seleccionar **+Create profile**.
8. Seleccionar **Create** para iniciar el asistente.
9. En **Basics**, introducir **Name** y **Description** y seleccionar **Next**.
10. En **Configuration settings**, revisar y configurar las opciones de seguridad recomendadas y seleccionar **Next**.
11. En **Scope tags**, seleccionar las etiquetas necesarias y seleccionar **Next**.
12. En **Assignments**, incluir los grupos, usuarios o dispositivos. Opcionalmente, utilizar **Exclude groups** para excluir grupos.
13. En **Review + create**, revisar la configuración y seleccionar **Create**.

# Grupos en Microsoft 365

Después de que una organización crea las cuentas de usuario para su tenant de Microsoft 365, puede crear grupos para la colaboración entre usuarios, tanto dentro como fuera de la empresa.

* En **Exchange Online**, los grupos permiten distribuir correo electrónico a varios usuarios.
* En **SharePoint Online**, los grupos permiten la colaboración entre distintos equipos.
* Una organización puede agregar personas externas a la empresa a un grupo, siempre que el administrador de Microsoft 365 habilite este permiso.

Los grupos pueden utilizarse para distribuir correo, administrar permisos, controlar el acceso a recursos y facilitar la colaboración.

## Tipos de grupos en Microsoft 365

La pertenencia a grupos se basa en cuentas de **Microsoft Entra ID**. Algunos grupos son creados por administradores para administrar Conditional Access, dispositivos y otros recursos. Otros son creados por miembros de la organización para colaborar mediante Teams, SharePoint y otras herramientas.

| Tipo de grupo                   | Descripción                                                                                                                                                                                                                                                                                                                                                      | Cuándo utilizarlo                                                                                                                      | Dónde crearlo                                                                                                                  |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Microsoft 365 group**         | Es el tipo de grupo recomendado. Incluye correo grupal y espacios de trabajo compartidos para correo, conversaciones, archivos y eventos de calendario. Es similar a un grupo de distribución porque tiene su propio buzón y sus miembros reciben los mensajes enviados al grupo, pero además proporciona un espacio de trabajo compartido para la colaboración. | Cuando se necesitan capacidades de lista de distribución y características de colaboración. Es la mejor opción para trabajo en equipo. | Microsoft 365 admin center, Microsoft 365 admin app, Microsoft Entra admin center, Exchange admin center, Outlook (Groups app) |
| **Distribution group**          | También denominado distribution list. Se utiliza principalmente para enviar notificaciones a un grupo de personas mediante una única dirección de correo. El sistema de correo distribuye los mensajes enviados a esa dirección entre todos los miembros.                                                                                                        | Cuando solo se necesita distribuir mensajes.                                                                                           | Microsoft 365 admin center, Microsoft 365 admin app, Exchange admin center                                                     |
| **Mail-enabled security group** | Grupo de seguridad asociado a una dirección de correo. Sus miembros pueden enviar y recibir correos mediante esa dirección. Funciona como lista de distribución y también puede utilizarse para asignar permisos a recursos como SharePoint. No puede administrarse dinámicamente ni contener dispositivos.                                                      | Cuando se necesita utilizar el grupo tanto para permisos como para distribución de correo.                                             | Microsoft 365 admin center, Microsoft 365 admin app, Exchange admin center                                                     |
| **Security group**              | Permite administrar y asignar permisos a múltiples usuarios simultáneamente. Puede conceder acceso a recursos como OneDrive y SharePoint.                                                                                                                                                                                                                        | Cuando solo se necesita un grupo para conceder permisos.                                                                               | Microsoft 365 admin center, Microsoft 365 admin app, Microsoft Entra admin center                                              |
| **Dynamic distribution group**  | Administra automáticamente su pertenencia según criterios o filtros predefinidos. Microsoft 365 actualiza dinámicamente la lista de miembros según atributos como departamento, ubicación, cargo o atributos personalizados. Se administra en Exchange Online mediante PowerShell o Exchange admin center.                                                       | Cuando se necesita una lista de distribución cuya pertenencia cambie automáticamente.                                                  | Exchange admin center                                                                                                          |
| **Shared mailbox**              | Permite que varias personas accedan al mismo buzón, por ejemplo una dirección de información, soporte, recepción u otra función compartida. Los usuarios con permisos pueden enviar como el buzón o en nombre del buzón.                                                                                                                                         | Cuando varias personas necesitan acceder al mismo buzón, como una dirección de soporte.                                                | Microsoft 365 admin center, Microsoft 365 admin app, Exchange admin center                                                     |

## Espacios de colaboración de los grupos de Microsoft 365

Un grupo de Microsoft 365 puede estar compuesto por los siguientes objetos:

* Bandeja de entrada compartida de Outlook.
* Calendario compartido.
* Sitio de equipo de SharePoint.
* Biblioteca de documentos de SharePoint.
* Planner.
* Power BI.
* Yammer, si el grupo se creó desde Yammer.
* Un Team, si el grupo se creó desde Teams.
* Un roadmap, si se dispone de Project for the web.

Los espacios de colaboración dependen de dónde se cree el grupo de Microsoft 365. Los usuarios pueden crear grupos desde Outlook, mientras que otras aplicaciones los crean automáticamente cuando los usuarios crean Teams, sitios de equipo de SharePoint, planes de Planner y grupos de Viva Engage.

**Nota:** Teams y Viva Engage no pueden conectarse al mismo grupo.

## Cómo funcionan los grupos de Microsoft 365 con Teams

Microsoft 365 Groups es el servicio de pertenencia entre aplicaciones de Microsoft 365. Un grupo de Microsoft 365 es un objeto de Microsoft Entra ID con una lista de miembros y una vinculación con cargas de trabajo relacionadas, como:

* Sitio de equipo de SharePoint.
* Buzón compartido de Exchange.
* Planner.
* OneNote.

Los usuarios pueden agregarse o eliminarse del grupo como con cualquier otro objeto de seguridad basado en grupos de Active Directory.

De forma predeterminada, los usuarios de Microsoft 365 pueden crear y administrar grupos.

Cuando se crea un Team, se crea un grupo de Microsoft 365 para administrar la pertenencia al equipo. Los servicios relacionados, como el sitio de SharePoint y el buzón, también se crean al mismo tiempo.

Las personas que crean Teams pueden elegir utilizar un grupo de Microsoft 365 existente si son propietarios de ese grupo.

Cada canal del Team tiene una carpeta independiente en la biblioteca de documentos. Crear carpetas directamente en la biblioteca de documentos no crea canales en el Team.

Cuando se crea un grupo de Microsoft 365 desde Teams admin center, Outlook o SharePoint, el buzón del grupo es visible en Outlook.

Cuando se crea un Team en Teams, el buzón del grupo está oculto de forma predeterminada. Se puede utilizar el cmdlet `Set-UnifiedGroup` con el parámetro `HiddenFromExchangeClientsEnabled` para hacer visible el buzón.

### Pertenencia a grupos

Si se elimina un miembro de un Team, también se lo elimina del grupo de Microsoft 365. La eliminación del grupo elimina inmediatamente el Team y sus canales del cliente de Teams.

Si se elimina una persona de un grupo mediante el Microsoft 365 admin center, deja de tener acceso a otros aspectos colaborativos, como:

* Biblioteca de documentos de SharePoint Online.
* Grupo de Viva Engage.
* OneNote compartido.

Sin embargo, todavía puede acceder a la funcionalidad de chat del Team durante aproximadamente dos horas.

Como buena práctica para administrar miembros de Teams, se recomienda agregarlos y eliminarlos desde Teams para que las actualizaciones de permisos en las demás cargas de trabajo conectadas al grupo se produzcan rápidamente.

Si los miembros se agregan o eliminan fuera de Teams, mediante Microsoft 365 admin center, Microsoft Entra ID o Exchange Online PowerShell, los cambios pueden tardar hasta 24 horas en reflejarse en Teams.

### Eliminación de grupos y Teams

Cuando se elimina un grupo de Microsoft 365:

* El sistema elimina el alias del buzón para conversaciones persistentes de Outlook/OWA y las invitaciones a reuniones de Teams.
* El sitio de SharePoint queda marcado para eliminación.

Transcurren aproximadamente 20 minutos entre la eliminación de un Team y su efecto en Outlook.

Al eliminar un Team desde Teams, desaparece inmediatamente de la vista de todos los usuarios que son miembros del equipo.

Si se eliminan miembros de un grupo de Microsoft 365 conectado a Teams, puede existir un retraso de aproximadamente dos horas antes de que el Team desaparezca de la vista de las personas afectadas.

## Crear y administrar grupos en Microsoft 365

Las organizaciones pueden utilizar distintos portales de Microsoft 365 para organizar usuarios en grupos. Los grupos pueden utilizarse para asignar permisos y administrar el acceso a recursos.

Por ejemplo, una organización puede crear en el Microsoft 365 admin center un grupo de seguridad que incluya a todos los usuarios del departamento de Marketing y conceder a ese grupo acceso **Full Control** a una colección de sitios de SharePoint dedicada a Marketing.

### Buenas prácticas

* Mantener las convenciones de nombres simples pero claras.
* Crear políticas y procedimientos para el mantenimiento continuo de los grupos.
* Agregar usuarios a grupos de seguridad y después agregar esos grupos de seguridad a los grupos o roles predeterminados de SharePoint, en lugar de agregar usuarios individuales.
* Mantener un proceso de aprovisionamiento de cuentas consistente y bien definido.
* Asignar al menos dos propietarios a un grupo para que uno pueda ayudar en ausencia del otro.

### Crear un grupo desde Microsoft 365 admin center

1. En **Microsoft 365 admin center**, seleccionar **Groups** y después **Active groups**.
2. En **Active groups**, seleccionar **Add a group**.
3. En **Group type**, seleccionar el tipo de grupo apropiado.
4. En **Set up the basics**, proporcionar el nombre y la descripción.
5. Es necesario seleccionar el campo **Description** para habilitar el botón **Next**, incluso si no se agrega una descripción.
6. En **Assign owners**, seleccionar un propietario. El campo **Owners** permite buscar entre los usuarios activos.
7. En **Edit settings**:

   * Asignar una dirección de correo para grupos habilitados para correo.
   * Determinar si el grupo es **Public** o **Private**.
   * Seleccionar si se debe crear un Microsoft Team para el grupo.
8. La opción **Public** está seleccionada de forma predeterminada. Aunque se quiera un grupo público, se debe seleccionar esta opción para habilitar **Next**.
9. En **Review and finish adding group**, revisar y corregir la información.
10. Seleccionar **Create group**.

Una organización no puede utilizar el Microsoft 365 admin center para editar grupos de seguridad que estén sincronizados con Active Directory local. Para modificarlos debe utilizar las herramientas de administración del Active Directory local.

También se pueden crear grupos de seguridad mediante Windows PowerShell. En Microsoft Graph PowerShell se utiliza `New-MgGroup`.

Ejemplo:

```powershell
New-MgGroup -DisplayName 'Test Group' -MailEnabled:$False -MailNickName 'testgroup' -SecurityEnabled
```

### Determinar los tipos de grupos

En Microsoft 365 admin center, la columna **Type** muestra el tipo de grupo.

La misma información puede obtenerse mediante Microsoft Graph PowerShell utilizando `Get-MgGroup`.

## Anidamiento de grupos

Microsoft 365 permite el anidamiento de grupos, es decir, agregar un grupo como miembro de otro grupo.

Para anidar grupos:

* Al agregar miembros desde Microsoft 365 admin center, seleccionar el grupo correspondiente en lugar de un usuario.
* También se pueden anidar grupos de seguridad mediante Windows PowerShell.

Microsoft 365 limita el anidamiento y no permite agregar todos los tipos de grupos como miembros de todos los demás tipos.

| Tipo de grupo                | Puede ser miembro de grupos Microsoft 365 | Puede ser miembro de grupos de distribución | Puede ser miembro de grupos de seguridad | Puede ser miembro de grupos de seguridad habilitados para correo |
| ---------------------------- | ----------------------------------------: | ------------------------------------------: | ---------------------------------------: | ---------------------------------------------------------------: |
| Microsoft 365 groups         |                                        No |                                          No |                                       No |                                                               No |
| Distribution groups          |                                        No |                                          Sí |                                       Sí |                                                               Sí |
| Security groups              |                                        No |                                          No |                                       Sí |                                                               No |
| Mail-enabled Security groups |                                        No |                                          Sí |                                       Sí |                                                               Sí |

Los grupos anidados pueden provocar problemas de permisos, por lo que es importante planificar cuidadosamente la jerarquía de grupos para garantizar que los permisos se concedan correctamente.

## Eliminar y restaurar grupos

Para eliminar un grupo desde Microsoft 365 admin center:

1. Seleccionar **Groups** y después **Active groups**.
2. Seleccionar el grupo que se desea eliminar.
3. Seleccionar el icono de tres puntos (**More actions**).
4. Seleccionar **Delete group**.
5. En el panel de detalles, seleccionar **Delete group**.
6. Confirmar la eliminación.

También se pueden eliminar grupos mediante Microsoft Graph PowerShell utilizando `Remove-MgGroup`.

Cuando se elimina un grupo de Microsoft 365, el sistema lo conserva durante **30 días** de forma predeterminada. Este período se considera un **soft-delete**, porque el grupo todavía puede restaurarse durante ese tiempo.

Después de 30 días, el grupo de Microsoft 365 y su contenido asociado se eliminan permanentemente.

Solo los grupos de Microsoft 365 pueden restaurarse después de ser eliminados. Los demás tipos de grupos no pueden restaurarse.

Al restaurar un grupo de Microsoft 365, se restauran automáticamente:

* Objeto, propiedades y miembros del grupo en Microsoft Entra ID.
* Direcciones de correo del grupo.
* Bandeja de entrada y calendario compartidos de Exchange Online.
* Sitio de equipo y archivos de SharePoint Online.
* OneNote.
* Planner.
* Teams.
* Grupo y contenido de Yammer, si el grupo se creó desde Yammer.
* Espacio de trabajo de Power BI Classic.

**Nota:** Azure Active Directory (Azure AD) ahora se denomina Microsoft Entra ID.

## Licencias basadas en grupos en Microsoft Entra ID

Los servicios cloud pagos de Microsoft, como Microsoft 365, Enterprise Mobility + Security y Dynamics 365, requieren licencias.

Las organizaciones pueden administrar licencias desde Microsoft 365, Microsoft Entra ID o mediante cmdlets de PowerShell.

Microsoft Entra ID permite utilizar **group-based licensing**, que permite asignar una o más licencias de producto a un grupo.

Microsoft Entra ID asigna automáticamente esas licencias a todos los miembros agregados al grupo. Cuando un miembro abandona el grupo, el sistema elimina automáticamente sus licencias.

Esto elimina la necesidad de automatizar mediante PowerShell la administración de licencias para reflejar cambios organizativos y departamentales por usuario.

### Requisitos para group-based licensing

Cada usuario que se beneficie de group-based licensing debe estar cubierto por una de las siguientes licencias:

* Suscripción paga o de prueba de **Microsoft Entra Premium P1 o superior**.
* Edición paga o de prueba de:

  * Microsoft 365 Business Premium.
  * Microsoft 365 Enterprise E3.
  * Microsoft 365 A3.
  * Microsoft 365 GCC G3.
  * Microsoft 365 E3 for GCCH.
  * Microsoft 365 E3 for DOD.
  * O superior.

Para cualquier grupo al que se asigne una licencia, se requiere una licencia para cada miembro único.

No es necesario asignar directamente una licencia a cada miembro del grupo, pero deben existir suficientes licencias para cubrir a todos los miembros.

Por ejemplo, si existen 1.000 miembros únicos que forman parte de grupos con licencias en el tenant, se necesitan al menos 1.000 licencias para cumplir con el acuerdo de licenciamiento.

### Características de group-based licensing

* Se pueden asignar licencias a cualquier grupo de seguridad de Microsoft Entra ID.
* Las organizaciones pueden sincronizar grupos de seguridad locales mediante Microsoft Entra Connect Sync.
* También pueden crear grupos de seguridad directamente en Microsoft Entra ID (cloud-only groups).
* Los grupos de seguridad pueden crearse automáticamente mediante la funcionalidad de grupos dinámicos de Microsoft Entra ID.
* Al asignar una licencia de producto a un grupo, el administrador puede deshabilitar uno o más service plans del producto.
* Un service plan puede deshabilitarse cuando la organización todavía no está preparada para utilizar un servicio incluido en el producto.
* El sistema admite los servicios cloud de Microsoft que requieren licenciamiento por usuario, incluidos Microsoft 365, Enterprise Mobility + Security y Dynamics 365.
* Group-based licensing está disponible actualmente únicamente mediante Microsoft Entra admin center.
* La administración de usuarios y grupos puede continuar realizándose desde otros portales, pero la administración de licencias a nivel de grupo debe realizarse desde Microsoft Entra admin center.
* Microsoft Entra ID administra automáticamente las modificaciones de licencias provocadas por cambios en la pertenencia a grupos.
* Normalmente, los cambios de licencias son efectivos en cuestión de minutos después de modificar la pertenencia.
* Un usuario puede pertenecer a varios grupos con políticas de licencia y también puede tener licencias asignadas directamente.
* El estado final del usuario combina todas las licencias de productos y servicios asignadas.
* Si la misma licencia se asigna al usuario desde varias fuentes, el sistema consume la licencia una sola vez.
* En algunos casos, Microsoft Entra ID no puede asignar completamente las licencias a un usuario, por ejemplo cuando no existen suficientes licencias disponibles o cuando se asignan servicios incompatibles.
* Los administradores pueden consultar la información de los usuarios para los que Microsoft Entra ID no pudo procesar completamente las licencias de grupo y tomar medidas correctivas.

## Grupos dinámicos mediante Microsoft Entra rule builder

Las organizaciones pueden utilizar reglas para determinar la pertenencia a grupos basándose en propiedades de usuarios o dispositivos de Microsoft Entra ID.

Microsoft 365 admite pertenencia dinámica para:

* **Security groups**
* **Microsoft 365 Groups**

Cuando se crea un grupo con pertenencia dinámica, el sistema evalúa los atributos de usuarios y dispositivos para determinar si coinciden con la regla.

Cuando cambia un atributo de un usuario o dispositivo, el sistema examina las reglas de los grupos dinámicos de la organización para determinar los cambios de pertenencia. Luego agrega o elimina usuarios y dispositivos según las condiciones de cada grupo.

### Requisitos de licencia para grupos dinámicos

Las organizaciones que implementan grupos dinámicos deben disponer de una licencia **Microsoft Entra Premium P1** o **Microsoft Intune for Education** para cada usuario único que sea miembro de un grupo dinámico.

No es necesario asignar directamente las licencias a los usuarios para que sean miembros de grupos dinámicos, pero la organización debe disponer del número mínimo de licencias necesario para cubrirlos.

Por ejemplo, si existen 1.000 usuarios únicos en todos los grupos dinámicos de la organización, se necesitan al menos 1.000 licencias Microsoft Entra Premium P1.

Los dispositivos que sean miembros de un grupo dinámico de dispositivos no necesitan una licencia.

## Rule builder en Microsoft Entra admin center

Microsoft Entra ID proporciona una herramienta **rule builder** para crear y actualizar reglas de forma rápida.

* El rule builder admite hasta **cinco expresiones**.
* Facilita la creación de reglas con unas pocas expresiones simples.
* No permite reproducir todas las reglas.
* Cuando la regla requiere más de cinco expresiones o una sintaxis que el rule builder no admite, se debe utilizar el cuadro de texto de sintaxis.

Ejemplos de reglas que deben construirse mediante el cuadro de sintaxis:

* Reglas con más de cinco expresiones.
* Regla **Direct reports**.
* Configuración de precedencia de operadores.
* Reglas con expresiones complejas, como:

  ```text
  (user.proxyAddresses -any (_ -contains “contoso“))
  ```

El rule builder puede no mostrar algunas reglas creadas directamente en el cuadro de texto. Puede aparecer un mensaje indicando que no puede mostrar la regla.

El rule builder no modifica la sintaxis admitida, la validación ni el procesamiento de las reglas de grupos dinámicos.

### Crear una regla de pertenencia a un grupo

1. Ir a **Microsoft Entra admin center**.
2. También se puede acceder desde Microsoft 365 admin center seleccionando **Show all** y luego **Identity** en **Admin centers**.
3. Iniciar sesión con una cuenta que sea Global administrator, Intune administrator o User administrator.
4. En el panel izquierdo, seleccionar **Groups** y luego **All groups**.
5. Seleccionar **New group**.
6. En la página **New Group**, indicar:

   * **Group name**
   * **Group description**
   * Si se pueden asignar roles de Microsoft Entra al grupo.
   * **Membership type**, seleccionando **Dynamic user** o **Dynamic device**.
7. En **Owners**, seleccionar **No owners selected** y luego agregar los propietarios.
8. En **Dynamic user members**, seleccionar **Add dynamic query**.
9. En **Dynamic membership rules**, utilizar el rule builder o el cuadro de texto de sintaxis.
10. Para consultar las propiedades de extensión personalizadas:

    * Seleccionar **+Get custom extension properties**.
    * Introducir el **application ID**.
    * Seleccionar **Refresh properties**.
11. Seleccionar **Save**.
12. En la página **New group**, seleccionar **Create**.

Si la regla no es válida, el sistema muestra una explicación del problema y normalmente proporciona instrucciones para corregirla.

## Reglas de pertenencia dinámica

Las reglas basadas en atributos permiten crear pertenencia dinámica para grupos de seguridad o grupos de Microsoft 365.

Cuando cambian los atributos de un usuario o dispositivo, el sistema evalúa las reglas de los grupos dinámicos del directorio.

Si cumple la regla de un grupo, se agrega automáticamente. Si deja de cumplirla, se elimina automáticamente.

Reglas:

* No se puede agregar o eliminar manualmente un miembro de un grupo dinámico.
* Se puede crear un grupo dinámico de dispositivos o de usuarios, pero una regla no puede contener simultáneamente usuarios y dispositivos.
* Un grupo de dispositivos no puede basarse en atributos del usuario propietario del dispositivo. Las reglas de pertenencia de dispositivos solo pueden hacer referencia a atributos del dispositivo.

## Sintaxis de una regla con una expresión

Una expresión simple tiene la forma:

```text
Property Operator Value
```

La propiedad utiliza el nombre de `object.property`.

Ejemplo:

```text
user.department -eq “Sales“
```

Los paréntesis son opcionales para una expresión simple.

La longitud total del cuerpo de una regla no puede superar los **3072 caracteres**.

### Operadores admitidos

| Operador        | Sintaxis         |
| --------------- | ---------------- |
| Not Equals      | `-ne`            |
| Equals          | `-eq`            |
| Not Starts With | `-notStartsWith` |
| Starts With     | `-startsWith`    |
| Not Contains    | `-notContains`   |
| Contains        | `-contains`      |
| Not Match       | `-notMatch`      |
| Match           | `-match`         |
| In              | `-in`            |
| Not In          | `-notIn`         |

Los operadores pueden utilizarse con o sin el prefijo `-`.

El operador **Contains** realiza coincidencias parciales de cadenas, no coincidencias de elementos dentro de una colección.

Para comparar un atributo de usuario contra múltiples valores se pueden utilizar `-in` o `-notIn`, utilizando `[` y `]` para delimitar la lista.

Ejemplo:

```text
user.department -in ["50001","50002","50003","50005","50006","50007","50008","50016","50020","50024","50038","50039","51100"]
```

El operador `-match` permite realizar coincidencias mediante expresiones regulares.

Ejemplo:

```text
user.displayName -match "Da.*"
```

En este caso, `"Da"`, `"Dav"` y `"David"` son verdaderos, mientras que `"aDa"` es falso.

Otro ejemplo:

```text
user.displayName -match ".*vid"
```

En este caso, `"David"` es verdadero y `"Da"` es falso.

## Construcción del cuerpo de una regla

Una regla de pertenencia que completa automáticamente un grupo con usuarios o dispositivos es una expresión binaria que devuelve verdadero o falso.

Una regla simple tiene tres partes:

* **Property**
* **Operator**
* **Value**

El orden de las partes es importante para evitar errores de sintaxis.

### Propiedades admitidas

Se pueden utilizar tres tipos de propiedades:

* Boolean.
* String.
* String collection.

### Valores admitidos

Los valores pueden ser:

* Strings.
* Boolean: `true`, `false`.
* Numbers.
* Arrays: arrays de números o strings.

Consideraciones de sintaxis:

* Las comillas dobles son opcionales excepto cuando el valor es una cadena.
* Las operaciones de strings y expresiones regulares no distinguen mayúsculas y minúsculas.
* Cuando una cadena contiene comillas dobles, se deben escapar.
* Las comillas simples se deben escapar utilizando dos comillas simples.
* Se pueden realizar comprobaciones de `Null`, utilizando `null`.

Ejemplo:

```text
user.department -eq null
```

## Reglas con múltiples expresiones

Una regla puede contener varias expresiones simples conectadas mediante:

* `-and`
* `-or`
* `-not`

También se pueden combinar operadores lógicos.

Ejemplos:

```text
(user.department -eq “Sales“) -or (user.department -eq “Marketing“)
```

```text
(user.department -eq “Sales“) -and -not (user.jobTitle -contains “SDE“)
```

## Reglas con expresiones complejas

Una expresión se considera compleja cuando:

* La propiedad consiste en una colección de valores, específicamente propiedades con múltiples valores.
* Se utilizan los operadores `-any` o `-all`.
* El valor de la expresión puede ser una o más expresiones.

## Ejemplos de reglas comunes

### Direct Reports

Se puede crear un grupo que contenga todos los subordinados directos de un manager. Cuando cambien sus subordinados directos, el sistema ajusta automáticamente la pertenencia del grupo.

Sintaxis:

```text
Direct Reports for “{objectID_of_manager}“
```

Ejemplo:

```text
Direct Reports for “62e19b97-8b3d-4d4a-a106-4ce66896a863“
```

Consideraciones:

* El Manager ID es el object ID del manager y se puede encontrar en su Profile.
* La propiedad Manager de los usuarios debe estar correctamente configurada.
* Esta regla solo admite subordinados directos del manager.
* No se puede crear un grupo que incluya también los subordinados de esos subordinados.
* Esta regla no puede combinarse con otras reglas de pertenencia.

### All Users

Se puede crear un grupo que contenga todos los usuarios de una organización.

El sistema ajusta automáticamente la pertenencia cuando se agregan o eliminan usuarios.

Para incluir usuarios miembro y usuarios invitados B2B:

```text
user.objectId -ne null
```

Para excluir invitados y utilizar únicamente usuarios miembros:

```text
(user.objectId -ne null) -and (user.userType -eq “Member“)
```

### All Devices

Se puede crear un grupo que contenga todos los dispositivos de una organización.

El sistema ajusta automáticamente la pertenencia cuando se agregan o eliminan dispositivos.

Regla:

```text
device.objectId -ne null
```

## Extension attributes y custom extension properties

El sistema admite atributos de extensión y propiedades de extensión personalizadas como propiedades de tipo string en reglas de pertenencia dinámica.

Los **Extension attributes** pueden sincronizarse desde Windows Server Active Directory local o actualizarse mediante Microsoft Graph.

Tienen el formato:

```text
extensionAttributeX
```

donde `X` corresponde a un valor entre 1 y 15.

No se admiten propiedades de extensión con múltiples valores en reglas de pertenencia dinámica.

Ejemplo:

```text
(user.extensionAttribute15 -eq “Marketing“)
```

Las **custom extension properties** pueden sincronizarse desde:

* Windows Server Active Directory local.
* Una aplicación SaaS conectada.
* Microsoft Graph.

Deben utilizar el formato:

```text
user.extension_[GUID]_[Attribute]
```

donde:

* `[GUID]` es la versión sin separadores del identificador único de Microsoft Entra ID correspondiente a la aplicación que creó la propiedad. Contiene únicamente caracteres 0-9 y A-Z.
* `[Attribute]` es el nombre de la propiedad cuando se creó originalmente.

Ejemplo:

```text
user.extension_c272a57b722d4eb29bfe327874ae79cb_OfficeNumber -eq "123"
```

Las custom extension properties también se denominan directory extension properties o Microsoft Entra extension properties.

El nombre de una propiedad personalizada puede encontrarse consultando la propiedad de un usuario mediante Graph Explorer y buscando el nombre de la propiedad.

También se puede seleccionar **Get custom extension properties** en el rule builder de grupos dinámicos, introducir un application ID y mostrar la lista completa de propiedades de extensión personalizadas disponibles.

La lista puede actualizarse para obtener nuevas propiedades de extensión personalizadas de esa aplicación.

Las extension attributes y las custom extension properties deben provenir de aplicaciones del tenant.

# Microsoft 365 group naming policy

Las organizaciones pueden utilizar una **group naming policy** para aplicar una estrategia de nombres consistente a los grupos creados por los usuarios.

La política puede ayudar a identificar:

* Función del grupo.
* Pertenencia.
* Región geográfica.
* Usuario que creó el grupo.

También puede ayudar a categorizar grupos en la libreta de direcciones y bloquear palabras específicas en nombres y alias de grupos.

La política se aplica a los grupos que los usuarios crean en diferentes cargas de trabajo, como:

* Outlook.
* Microsoft Teams.
* SharePoint.
* Planner.
* Yammer.
* Otras cargas de trabajo de grupos.

Microsoft 365 aplica la política tanto al nombre del grupo como al alias.

También se aplica cuando un usuario:

* Crea un grupo.
* Edita el nombre de un grupo existente.
* Edita el alias.
* Edita la descripción.
* Edita el avatar.

La Microsoft 365 group naming policy se crea en Microsoft Entra ID mediante Microsoft Entra admin center.

**Importante:** la Microsoft 365 group naming policy solo se aplica a grupos de Microsoft 365. No se aplica a grupos de distribución creados en Exchange Online.

## Características de la naming policy

### Prefix-Suffix naming policy

Permite utilizar prefijos o sufijos para definir la convención de nombres.

Ejemplo:

```text
US_My Group_Engineering
```

Los prefijos y sufijos pueden ser:

* Strings fijos.
* Atributos de usuario, como `[Department]`, que se sustituyen según el usuario que crea el grupo.

### Custom Blocked Words

Permite cargar palabras bloqueadas específicas de la organización.

Por ejemplo:

```text
CEO, Payroll, HR
```

Microsoft 365 impide que los usuarios utilicen esas palabras en los grupos de Microsoft 365 que crean.

## Requisitos de licencia

Para utilizar una naming policy de Microsoft Entra para Microsoft 365 Groups, una organización debe disponer de:

* Microsoft Entra Premium P1.
* O Microsoft Entra Basic EDU.

Debe existir una licencia para cada usuario único y cada invitado que sea miembro de uno o más grupos de Microsoft 365. No es necesario asignar directamente la licencia a los usuarios.

Microsoft Entra Premium P1 proporciona funcionalidades adicionales para administrar Microsoft 365 Groups, como:

* Pertenencia dinámica.
* Administración de grupos mediante autoservicio.

Microsoft Entra Basic EDU es una alternativa de menor costo con funcionalidades básicas para administrar Microsoft 365 Groups y está destinada principalmente a instituciones educativas reconocidas.

El requisito de licencia también se aplica al administrador que crea la naming policy.

## Prefix-Suffix naming policy

Los prefijos y sufijos pueden ser strings fijos o atributos de usuario.

### Strings fijos

Se pueden utilizar strings cortos para diferenciar grupos en la GAL y en la navegación izquierda de las cargas de trabajo de grupos.

Ejemplos:

```text
Grp_Name
#Name
_Name
```

### Atributos de usuario

Se pueden utilizar atributos para identificar quién creó el grupo o su ubicación.

Ejemplo:

```text
Policy = "GRP [GroupName] [Department]"
User's department = Engineering
Created group name = "GRP My Group Engineering"
```

Los atributos de Microsoft Entra ID admitidos son:

* `[Department]`
* `[Company]`
* `[Office]`
* `[StateOrProvince]`
* `[CountryOrRegion]`
* `[Title]`

Los atributos no admitidos se consideran strings fijos, como `[postalCode]`.

No se admiten extension attributes ni custom attributes.

Microsoft recomienda utilizar atributos que tengan valores completos para todos los usuarios y evitar atributos cuyos valores sean demasiado largos.

## Consideraciones de Microsoft 365 group naming policy

* Durante la creación de la política, se debe limitar la longitud total de los strings de prefijo y sufijo a **53 caracteres**.
* Los prefijos y sufijos pueden contener caracteres especiales admitidos en nombres y alias de grupos.
* Si los caracteres especiales no están permitidos en el alias del grupo, el sistema aplica esos prefijos y sufijos únicamente al nombre del grupo.
* En ese caso, los prefijos y sufijos aplicados al nombre pueden no coincidir con los aplicados al alias.
* El sistema permite un punto (`.`) o un guion (`-`) en cualquier posición del nombre, excepto al principio o al final.
* El guion bajo (`_`) puede utilizarse en cualquier posición, incluso al principio o al final.
* Si se utilizan grupos conectados de Yammer Office 365, se deben evitar `@`, `#`, `[`, `]`, `<` y `>`, porque si aparecen en la naming policy, los usuarios normales de Yammer no podrán crear grupos.

### Buenas prácticas

* Utilizar strings cortos como sufijos.
* Utilizar atributos que tengan valores.
* No utilizar nombres demasiado creativos.
* El sistema permite un nombre máximo de **264 caracteres**.
* Cargar las palabras bloqueadas específicas de la organización para restringir su uso.

## Custom blocked words

Se puede introducir una lista separada por comas de palabras bloqueadas.

El sistema no realiza búsquedas de subcadenas. Para activar el bloqueo debe existir una coincidencia exacta entre el nombre introducido por el usuario y una palabra de la lista.

Condiciones:

* Las palabras bloqueadas no distinguen mayúsculas y minúsculas.
* Cuando un usuario introduce una palabra bloqueada, el cliente del grupo muestra un mensaje de error con la palabra bloqueada.
* No existen restricciones de caracteres para las palabras bloqueadas.
* Se pueden configurar hasta **5000 palabras bloqueadas**.

## Administrator override

Microsoft 365 exime a determinados administradores de las políticas de naming en todas las cargas de trabajo y endpoints de grupos.

Estos administradores pueden crear grupos utilizando palabras bloqueadas y las convenciones de nombres que deseen.

Roles exentos:

* Global Administrator.
* Partner Tier 1 Support.
* Partner Tier 2 Support.
* User Account Administrator.

## Configurar la naming policy

1. En **Microsoft 365 admin center**, seleccionar **Show all**.
2. En **Admin centers**, seleccionar **Identity**.
3. En **Microsoft Entra admin center**, seleccionar **Groups**.
4. Seleccionar **Group settings**.
5. En **Groups | General**, dentro de **Settings**, seleccionar **Naming policy**.
6. En **Groups | Naming policy**, aparece inicialmente la pestaña **Blocked words**.
7. Seleccionar la pestaña **Group naming policy**.
8. En **Current policy**, seleccionar las casillas para requerir un prefijo, un sufijo o ambos.
9. Para cada casilla seleccionada, utilizar el campo correspondiente y elegir entre **Attribute** y **String**.
10. Especificar el atributo o string.
11. Seleccionar **Save**.

# Crear grupos en Exchange Online y SharePoint Online

Una organización puede crear grupos desde:

* Microsoft 365 admin center.
* Exchange Online.
* SharePoint Online.

## Crear grupos en Exchange Online

Exchange Online admin center permite crear grupos de usuarios.

Uno de los principales beneficios de los grupos es enviar un correo electrónico a todos los usuarios de un grupo al mismo tiempo.

Al crear un grupo en Exchange Online se debe seleccionar el tipo adecuado según su finalidad.

### Microsoft 365

Permite a los equipos colaborar mediante:

* Correo grupal.
* Espacio de trabajo compartido.
* Conversaciones.
* Archivos.
* Calendarios.

En Outlook se denominan **Groups**.

### Distribution

También se denomina **distribution list**.

Crea una dirección de correo para un grupo de personas.

### Mail-enabled security

Envía mensajes a todos los miembros del grupo y permite acceder a recursos como:

* OneDrive.
* SharePoint.
* Roles administrativos.

Combina las características de un grupo de seguridad y un grupo de distribución de correo.

### Dynamic distribution

Es un tipo de grupo de distribución.

Microsoft 365 actualiza automáticamente la lista de destinatarios cada **24 horas**, según los filtros y condiciones definidos por la organización.

Después de crear grupos de distribución y grupos de seguridad habilitados para correo en Exchange admin center:

* Sus nombres y listas de usuarios aparecen en la página **Active teams and groups** del Microsoft 365 admin center.
* Se pueden eliminar desde ambas ubicaciones.
* Solo se pueden editar desde Exchange admin center.
* Los grupos de distribución dinámicos no aparecen en la página de grupos de seguridad de Microsoft 365.

## Crear grupos en SharePoint Online

Microsoft 365 crea automáticamente varios grupos integrados de SharePoint cuando se crea una colección de sitios en SharePoint Online.

Los administradores de SharePoint también pueden crear manualmente grupos de SharePoint Online.

Los grupos de SharePoint Online son colecciones de usuarios que tienen el mismo nivel de permisos.

Esto permite conceder acceso a varios usuarios a un sitio de SharePoint Online mediante la asignación de permisos al grupo.

Los grupos de SharePoint Online simplifican la administración de permisos.

Aunque pueden contener usuarios individuales, es más fácil administrarlos mediante grupos de seguridad de Microsoft 365.

Los grupos integrados creados automáticamente al crear una colección de sitios se denominan **default SharePoint Online groups**.

Los grupos predeterminados dependen de la plantilla utilizada para crear el sitio.

Por ejemplo, la plantilla **Team Site** contiene:

* **Team Site Visitors**
* **Team Site Members**
* **Team Site Owners**

Los grupos predeterminados utilizan los niveles de permisos predeterminados de SharePoint, también denominados roles de SharePoint, para conceder derechos y acceso.

## Preguntas frecuentes sobre security groups

### ¿Cuál es la diferencia entre un security group de Microsoft 365 y los security groups creados en SharePoint?

Un security group de Microsoft 365, también denominado **Microsoft Entra security group**, funciona a nivel de Microsoft Entra ID.

Puede administrar acceso y permisos en distintos servicios, aplicaciones y recursos de Microsoft 365, proporcionando un alcance amplio de seguridad y control de acceso en todo el entorno de Microsoft 365.

Un security group de SharePoint es específico de SharePoint y funciona a nivel de colección de sitios o sitio.

Se utiliza para administrar acceso y permisos dentro de SharePoint, controlando quién puede:

* Ver.
* Editar.
* Interactuar con sitios.
* Interactuar con bibliotecas.
* Interactuar con listas.
* Interactuar con elementos individuales.

### ¿Es obligatorio utilizar security groups para que una organización sea segura?

No.

Los security groups son una forma de administrar la seguridad de la organización. También se pueden conceder permisos y acceso individualmente a los usuarios.

Los security groups facilitan la administración de grupos grandes de usuarios.

### ¿Se puede enviar correo a un security group?

Sí, siempre que sea un **mail-enabled security group**.

No se puede enviar correo a un security group normal.

# Knowledge checks

## Grupos para colaboración

Una organización quiere crear un grupo para que los miembros de un equipo de Manufacturing puedan colaborar y disponer de un espacio de trabajo compartido para:

* Email.
* Conversations.
* Files.
* Calendar events.

La respuesta correcta es:

**Microsoft 365 group**

## Edición de grupos sincronizados

Una organización creó un security group en Microsoft 365 que está sincronizado con Active Directory local y necesita editarlo.

La herramienta correcta es:

**Local Active Directory management tools**

Los security groups sincronizados con Active Directory local solo pueden modificarse mediante las herramientas de administración del Active Directory local.

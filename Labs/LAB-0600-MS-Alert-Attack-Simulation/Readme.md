# Lab 6 - Alert Policies y Attack Simulation Training en Microsoft Defender

## Exercise 1 - Prepare for Alert Policies

> Se prepara el tenant para trabajar con Alert Policies en Microsoft Defender XDR. Hay dos requisitos previos: Audit Logging (ya activado y propagado desde el Lab 1) y los permisos RBAC correctos. En este ejercicio se asigna a Lynne Robbins -la usuaria elegida para testear alertas- el role group **Compliance Data Administrator** (incluye el role Compliance Administrator), que cubre las categorías **Data Loss Prevention** y **Permissions**, necesarias para ver las 3 alertas que se van a crear en este lab.

| Role group | Data governance | Data loss prevention | Mail flow | Permissions | Threat Management | Others |
|---|---|---|---|---|---|---|
| Compliance Data Administrator | | X | | X | | X |

## Task 1: Assign RBAC Permissions for Alert Notification Testing
> Se asigna a Lynne Robbins al role group Compliance Data Administrator en Microsoft Defender XDR, lo que le da permisos para ver alertas de las categorías Permissions y Data Loss Prevention.
* [WINDOWS] Switch a **LON-CL1** (al finalizar el lab anterior se quedó logueado en LON-CL2)
  * Edge -> Holly debería seguir logueada en Microsoft 365
  * [MENU] pestaña **Microsoft 365 admin center** -> Admin centers -> **Security**
* [BROWSER] Se abre el **Microsoft Defender portal** en nueva pestaña
  * [MENU] scroll hasta el final del navigation pane -> **System** -> **Permissions**
    * [LINK] Permissions page tiene 4 secciones (Microsoft Defender XDR, Microsoft Entra ID, Email & collaboration roles, Cloud Apps) -> en sección **Email & collaboration roles** -> **Roles**
      * Ordenar la lista de roles por la columna **Name** (ascendente)
      * Seleccionar el role group **Compliance Data Administrator** (click en el nombre, no en el checkbox)
        * [DIALOG] pane **Compliance Data Administrator** -> revisar la lista de roles asignados a este role group
          * Scroll hasta el final del pane -> verificar que no hay members
          * Scroll al inicio -> **Edit**
        * [DIALOG] Edit members of the role group -> **Choose users**
          * [DIALOG] Choose users -> campo Search: escribir `Lynne` -> Enter
            * Tildar el checkbox de **Lynne Robbins** -> **Select**
          * Verificar que Lynne aparece en la lista -> **Next**
        * [TAB] Review the role group and finish -> verificar que Lynne figura como member -> **Save**
        * pane **You successfully updated the role group** -> **Done**
* Dejar todas las pestañas abiertas para el siguiente lab exercise

Con esto, Lynne Robbins queda agregada al role group **Compliance Data Administrator**.

---

# Learning Path 6 - Lab 6 - Exercise 2 - Implement a Mailbox Permission Alert

> Se configura y prueba una alert policy que notifica a Lynne Robbins cuando se otorgan permisos FullAccess sobre cualquier mailbox de Adatum. Se crea la policy (Task 1) y luego se dispara la alerta otorgando a Joni Sherman los tres permisos de delegación (Send as, Send on behalf, Full Access) sobre el mailbox de Alex Wilber (Task 2).
> ⚠️ IMPORTANTE: Este lab tiene 3 ejercicios que crean alert notifications (Ejercicios 2 a 4) y 2 ejercicios de ataques simulados que también generan alertas (Ejercicios 5 y 6). En los 5 casos el sistema puede tardar hasta 15 minutos en generar la alerta o el email correspondiente. Para no esperar 15 minutos después de cada uno (75 minutos en total), las tasks de validación de estos 5 ejercicios se movieron todas al Ejercicio 7 (el último del lab).

## Task 1: Create a Mailbox Permission Alert
> Se crea la alert policy "Mailbox permission change" (categoría Permissions, severidad Medium) que se dispara ante la actividad "Granted mailbox permission" y notifica por email a Lynne Robbins.
* [WINDOWS] LON-CL1 -> Edge (Holly logueada en Microsoft 365)
  * [MENU] pestaña **Microsoft Defender** (debería seguir abierta del ejercicio anterior)
    * [MENU] sección **Email & collaboration** -> **Policies & rules**
      * [MENU] **Alert policy**
        * [DIALOG] si aparece un aviso de que el alert policy portal fue actualizado -> **Dismiss**
        * NOTA: el mensaje en la parte superior de la página indica que las mail flow alerts se movieron al Exchange admin center y ya no se pueden mantener desde Microsoft Defender. Como se va a crear una alerta de mailbox permission (no de mail flow), se puede seguir trabajando en Microsoft Defender.
        * Revisar la lista de alert policies preconfiguradas
        * [MENU] **+New Alert Policy** (inicia el wizard New Alert Policy)
          * [TAB] Name your alert, categorize it, and choose a severity
            * Name: `Mailbox permission change`
            * Description: `This alert notifies Lynne Robbins when FullAccess permissions are granted to any mailbox in Adatum Corporation`
            * Severity: **Medium**
            * Category: **Permissions**
            * **Next**
          * [TAB] Choose an activity, conditions and when to trigger the alert
            * Activity is: seleccionar el campo -> escribir `mail` para filtrar -> seleccionar **Granted mailbox permission** de la lista
              * ⚠️ Esta actividad implica otorgar permiso FullAccess a un mailbox
            * How do you want the alert to be triggered?: **Every time an activity matches the rule**
            * **Next**
          * [TAB] Decide if you want to notify people when this alert is triggered
            * Email recipients: seleccionar la **X** junto a Holly Dickson para quitarla -> escribir `Lynne` -> seleccionar **Lynne Robbins** de la lista
            * Daily notification limit: **No limit**
            * **Next**
          * [TAB] Review your settings -> revisar la configuración (usar **Edit** en la sección correspondiente si hace falta corregir algo)
            * Do you want to turn the policy on right away?: seleccionar **Yes, turn it on right away**
            * **Submit**
          * New Alert Policy -> **Done**
        * Verificar que la nueva policy aparece en la lista del Alert policy page, con Type = **Custom** y Status = **On** (puede requerir scroll horizontal según el tamaño de pantalla)
* Dejar la pestaña Alert policy abierta para el siguiente task

Con esto queda creada una activity alert en Microsoft Defender XDR que se dispara cuando se otorgan permisos FullAccess a cualquier mailbox.

## Task 2: Test the Mailbox Permission Alert
> Se dispara la alerta creada en Task 1 otorgando a Joni Sherman los tres permisos de delegación (Send as, Send on behalf, Read and manage / Full Access) sobre el mailbox de Alex Wilber. La validación del email de notificación a Lynne Robbins se hace en el Ejercicio 7.
* [WINDOWS] LON-CL1 -> Edge (Holly logueada en Microsoft 365)
  * [MENU] pestaña **Microsoft 365 admin center** -> Admin centers -> **Exchange** (abre el Exchange admin center en nueva pestaña)
* [BROWSER] Exchange admin center
  * Ventana **Manage mailboxes** por default (si no aparece -> [MENU] sección Recipients -> **Mailboxes**)
    * Seleccionar **Alex Wilber** de la lista de mailboxes (click en el nombre, no en el checkbox)
      * [DIALOG] pane **Alex Wilber** -> tab General por default -> seleccionar tab **Delegation**
        * [TAB] Delegation -> tres permisos disponibles: **Send as**, **Send on behalf**, **Read and manage (Full Access)**
        * Para CADA uno de los tres permisos, agregar a Joni Sherman:
          * **Edit** en el permiso correspondiente
          * [DIALOG] Manage mailbox delegation -> **+Add members**
            * Tildar el checkbox de **Joni Sherman** -> **Save**
          * [DIALOG] Add delegate permissions? -> **Confirm**
          * Una vez agregado el permiso -> flecha atrás (arriba del pane) para volver al tab Delegation
          * Repetir para los otros dos permisos restantes
        * Una vez asignados los tres permisos a Joni -> cerrar el pane Alex Wilber con la **X**
    * ⚠️ Esta actividad debería disparar la alert policy creada en Task 1 y enviar un email de notificación al mailbox de Lynne Robbins. La validación se hace en el Ejercicio 7, Task 1 de este lab (en vez de esperar hasta 15 minutos ahora).
* Cerrar la pestaña del Exchange admin center. Dejar el resto de las pestañas abiertas y continuar con el siguiente ejercicio.

---

# Learning Path 6 - Lab 6 - Exercise 3 - Implement a SharePoint Permission Alert

> Se configura y prueba una alert policy que notifica a Lynne Robbins cuando se agrega un usuario como Site Collection Administrator en una SharePoint site collection. Se crea la policy (Task 1) y luego se dispara la alerta agregando a Alex Wilber como site collection admin del sitio global SharePoint Communication (Task 2).

## Task 1: Create a SharePoint Permission Alert
> Se crea la alert policy "Add user as a Site Collection administrator" (categoría Permissions, severidad Medium) que se dispara ante la actividad "Added site collection admin" y notifica por email a Lynne Robbins.
* [WINDOWS] LON-CL1 -> Edge (Holly logueada en Microsoft 365)
  * [MENU] pestaña **Alert policy - Microsoft Defender** (Microsoft Defender portal)
    * Debería seguir en la ventana Alert policy del ejercicio anterior (si no -> [MENU] **Policies & rules** -> **Alert policy**)
    * [MENU] **+New Alert Policy** (inicia el wizard New Alert Policy)
      * [TAB] Name your alert, categorize it, and choose a severity
        * Name: `Add user as a Site Collection administrator`
        * Description: `This alert notifies Lynne Robbins when a user is added to the Site Collection administrators on a SharePoint site collection.`
        * Severity: **Medium**
        * Category: **Permissions**
        * **Next**
      * [TAB] Choose an activity, conditions and when to trigger the alert
        * Activity is: seleccionar el campo Select an activity -> scroll hasta la sección **Site administration activities** -> seleccionar **Added site collection admin**
        * How do you want the alert to be triggered?: **Every time an activity matches the rule**
        * **Next**
      * [TAB] Decide if you want to notify people when this alert is triggered
        * Email recipients: quitar **Holly Dickson** y agregar **Lynne Robbins**
        * Daily notification limit: **No limit**
        * **Next**
      * [TAB] Review your settings
        * Do you want to turn the policy on right away?: seleccionar **Yes, turn it on right away**
        * **Submit**
      * New Alert Policy -> **Done**
    * Verificar que la nueva policy aparece en la lista del Alert policy page, con Type = **Custom** y Status = **On**
* Dejar todas las pestañas abiertas para el siguiente task

Con esto queda configurada una alert policy adicional que monitorea cuando se agrega un usuario como site collection administrator en SharePoint Online.

## Task 2: Test the SharePoint Permissions Alert
> Se dispara la alerta creada en Task 1 agregando a Alex Wilber como Site Collection Administrator del sitio global SharePoint Communication. La validación del email de notificación a Lynne Robbins se hace en el Ejercicio 7, Task 2.
* [WINDOWS] LON-CL1 -> Edge (Holly logueada en Microsoft 365)
  * [MENU] abrir nueva pestaña
* [BROWSER] `https://xxxxxZZZZZZ.sharepoint.com/_layouts/15/settings.aspx` (reemplazar xxxxxZZZZZZ por el tenant prefix del lab hosting provider) -> abre Site Settings del sitio global SharePoint Communication
  * [MENU] sección Users and Permissions -> **Site permissions**
    * [TAB] Permissions (por default) -> grupo Manage -> **Site Collection Administrators**
      * [DIALOG] Site Collection Administrators -> ya aparece la cuenta Global administrator asignada por default -> a la derecha, escribir `Alex` -> seleccionar **Alex Wilber** de la lista -> **OK**
      * ⚠️ Esta actividad debería disparar la alert policy creada en Task 1 y enviar un email de notificación al mailbox de Lynne Robbins. La validación se hace en el Ejercicio 7, Task 2 de este lab (en vez de esperar hasta 15 minutos ahora).
* Cerrar la pestaña **Permissions: Communication site**. Dejar el resto de las pestañas abiertas y continuar con el siguiente ejercicio.

---

# Learning Path 6 - Lab 6 - Exercise 4 - Test the Default eDiscovery Alert

> Se prueba una alert policy default de Microsoft 365 que notifica a todos los tenant admins (como Holly) cuando se crea o exporta un eDiscovery search. Primero se asignan los permisos RBAC de eDiscovery a Holly (Task 1), luego se revisa la configuración de la policy default (Task 2) y por último se dispara la alerta creando un eDiscovery search (Task 3).
> ⚠️ Una eDiscovery search sin regular puede extraer contenido sensible y exportarlo a una fuente no autorizada; por eso es importante tener este tipo de alerta configurada.

## Task 1: Assign RBAC Permissions for Search Notification Testing
> Se asigna a Holly Dickson los role groups eDiscovery Manager y eDiscovery Administrator, necesarios para poder testear la alert policy default.
* [WINDOWS] LON-CL1 -> Edge (Holly logueada en Microsoft 365)
  * [MENU] Microsoft 365 admin center -> Admin centers -> **Microsoft Purview**
* [BROWSER] Microsoft Purview portal
  * [DIALOG] Welcome to the new Microsoft Purview portal -> tildar **I agree to the terms** -> **Get started**
  * [MENU] **Settings**
    * [MENU] **Roles and scopes** -> **Role groups**
      * Seleccionar el role group **eDiscovery Manager** (click en el nombre, no en el checkbox)
        * [DIALOG] pane **eDiscovery Manager** -> **Edit**
        * [DIALOG] Manage eDiscovery Manager -> **Choose users**
          * [DIALOG] Choose users -> buscar y seleccionar **Holly Dickson** -> **Select**
          * Verificar que Holly aparece en la lista -> **Next**
        * [DIALOG] Manage eDiscovery Administrator -> **Choose users**
          * Buscar y seleccionar **Holly Dickson** -> **Select**
          * Verificar que Holly aparece en la lista -> **Next**
        * [TAB] Review the role group and finish -> verificar que Holly figura como member de ambos role groups -> **Save**
        * pane de confirmación -> **Done**
  * Sign out de Microsoft Purview -> volver a loguearse como **Holly Dickson**
    * ⚠️ Este paso ayuda a que los permisos actualizados se reconozcan en el siguiente task

Con esto queda Holly Dickson agregada a los role groups **eDiscovery Manager** y **eDiscovery Administrator**.

## Task 2: Review the Default eDiscovery Alert
> Se revisa la configuración de la alert policy default "eDiscovery search started or exported", que notifica a los Tenant Admins. Al tener el rol Global Administrator, Holly es automáticamente miembro de Tenant Admins.
* [WINDOWS] LON-CL1 -> Edge (Holly logueada en Microsoft 365)
  * [MENU] pestaña **Alert policy - Microsoft Defender**
    * Debería seguir en la ventana Alert policy del ejercicio anterior (si no -> [MENU] **Policies & rules** -> **Alert policy**)
    * Campo Search (arriba) -> escribir `eDiscovery` -> Enter
      * Seleccionar la policy **eDiscovery search started or exported** de la lista
        * [DIALOG] pane **eDiscovery search started or exported** -> scroll y verificar la configuración default:
          * Status: **On**
          * Sección **Create alert settings** (flecha hacia abajo) -> verificar:
            * Conditions: **Activity is eDiscoverySearchStartedOrExported**
            * Aggregation: **Single event**
            * Scope: **All users**
          * Sección **Set your recipients** (flecha hacia abajo) -> verificar:
            * Recipients: **TenantAdmins**
            * Daily notification limit: **No limit**
          * Arriba del pane -> **Edit policy**
            * ⚠️ Lo único editable en esta policy default es la lista de Email recipients. No se va a cambiar en este lab -> dejar como **TenantAdmins**. Sirve solo para ver cómo se editaría en un caso real.
            * **Cancel**
          * Cerrar el pane con la **X** (esquina superior derecha)
    * NOTA: también se puede editar la configuración de una policy desde el ícono de tres puntos verticales (Actions) al final de la fila correspondiente en la ventana Alert policy.

Con esto queda revisada la alerta default de Microsoft 365 que notifica a los tenant admins cuando se crea o exporta un eDiscovery search.

## Task 3: Test the Default eDiscovery Alert
> Se dispara la alerta default creando un eDiscovery search llamado "Confidential search". La validación del email de notificación a los Tenant Admins se hace en el Ejercicio 7, Task 3.
* [WINDOWS] LON-CL1 -> Edge (Holly logueada en Microsoft 365)
  * [MENU] pestaña **Microsoft Purview admin center**
* [BROWSER] Microsoft Purview portal
  * [MENU] **Solutions** -> **eDiscovery**
    * [MENU] **Content Search**
      * [TAB] Searches -> **Create a search** (inicia el wizard New search)
        * [TAB] Name and description -> Name: `Confidential search` -> **Create**
        * [DIALOG] **Confidential search** -> **Add sources**
          * Buscar y seleccionar el mailbox **Sales and Marketing** (si no está disponible, seleccionar **All mailboxes**)
          * **Save and close**
        * [TAB] Query -> condition builder -> keyword field: `Confidential` -> Enter
          * **Run query**
        * [TAB] Choose search results -> dejar los valores por default -> **Run query** nuevamente
        * De vuelta en **Confidential search** -> tab **Statistics** -> verificar que muestra resultados
    * ⚠️ Al correr esta search debería dispararse la eDiscovery alert, generando un email de notificación a todos los usuarios con permisos Tenant Admin. Puede tardar varios minutos en llegar. En vez de esperar, continuar con el siguiente ejercicio. La validación se hace en el Ejercicio 7, Task 3 de este lab.
* Dejar el browser abierto en LON-CL1 sin cerrar ninguna pestaña

---

# Learning Path 6 - Lab 6 - Exercise 5 - Conduct a Spear Phishing attack using Attack Simulation training

> Holly quiere evaluar qué tan susceptibles son los usuarios de Adatum a un ataque de phishing, usando la feature de Attack simulation training de Microsoft 365. Como esta feature requiere que el admin que corre la simulación tenga MFA habilitado, y Holly está excluida de MFA por la Conditional Access policy del pilot project, primero se habilita MFA a nivel de cuenta individual para Holly (Task 1) y luego se configura y lanza un ataque de Credentials Harvest tipo spear phishing contra todos los usuarios (Task 2).
> ⚠️ Para habilitar MFA en la cuenta de Holly hace falta un celular para recibir el código de verificación. Si no se cuenta con uno, hay que avisarle al instructor para hacer el lab en pareja con otro alumno.

## Task 1: Enable Multifactor Authentication for the attack simulation admin
> Se habilita MFA a nivel de cuenta individual solo para Holly Dickson (no vía Conditional Access), se cierra sesión y se vuelve a loguear completando el proceso de MFA con teléfono como segundo factor.
* [WINDOWS] LON-CL1 -> Edge (Holly logueada en Microsoft 365)
  * [MENU] pestaña **Microsoft 365 admin center** -> **Users** -> **Active users**
    * [MENU] barra de menú arriba de la lista -> **Multi-factor authentication** (si no aparece -> ícono de tres puntos **More actions** -> **Multi-factor authentication**)
* [BROWSER] Se abre la ventana **multi-factor authentication** en nueva pestaña
  * [TAB] users (por default) -> notar que el MFA Status de todos los usuarios está en **Disabled**
    * ⚠️ La Conditional Access policy creada anteriormente NO habilita el MFA status individual de cada usuario. Esa policy se aplica dinámicamente en cada sign-in para decidir si corresponde pedir MFA; si la policy no aplica MFA a un usuario, entonces se chequea el MFA status individual de su cuenta.
  * Tildar el checkbox de **Holly Dickson** (la cuenta .onmicrosoft) -> en el pane de properties que aparece a la derecha -> sección quick steps -> **Enable**
    * [DIALOG] About enabling multi-factor auth -> **enable multi-factor auth**
    * [DIALOG] Updates successful -> **close**
  * Verificar que el MFA Status de Holly cambió a **Enabled**
  * Cerrar la pestaña Multi-factor authentication -> vuelve a la pestaña Microsoft 365 admin center

### Cerrar sesión y volver a loguearse con MFA
* [MENU] ícono de usuario **HD** (esquina superior derecha) -> **Sign out**
* Cerrar Edge por completo
* [WINDOWS] LON-CL1 -> abrir Edge nuevamente (ícono en la taskbar)
* [BROWSER] `https://www.microsoft365.com/`
  * [LOGIN] Pick an account -> `Holly@xxxxxZZZZZZ.onmicrosoft.com` -> Next -> password: la New Administrative Password de Holly -> **Sign in**
  * [DIALOG] More information required (por MFA habilitado) -> **Next**
  * [MENU] Microsoft Authenticator page -> **I want to set up a different method**
    * ⚠️ No confundir con el link **I want to use a different authenticator app** que aparece arriba
  * [DIALOG] Choose a different method -> Which method would you like to use?: **Phone** -> **Confirm**
  * [DIALOG] Phone -> seleccionar país/región -> ingresar número de teléfono -> verificar **Receive a code** seleccionado -> **Next**
    * Retirar el código de verificación del SMS recibido
    * Ingresar el código de 6 dígitos -> **Next**
    * Mensaje de teléfono registrado exitosamente -> **Next**
  * pantalla Success! -> **Done**
  * [DIALOG] Stay signed in? -> tildar **Don't show this again** -> **Yes**
  * [TAB] Home | Microsoft 365 -> columna de íconos de apps -> ícono **Admin** (abre el Microsoft 365 admin center en nueva pestaña)
* [BROWSER] Microsoft 365 admin center
  * [MENU] **Show all** en el nav pane -> Admin centers -> **Security** (abre el Microsoft Defender portal; se retoma desde acá en el siguiente task)
* Dejar todo tal cual en la VM y continuar con el siguiente task

Con esto queda configurado MFA para Holly Dickson, con sesión iniciada en el Microsoft 365 admin center usando MFA, lista para correr el Attack simulator training en Microsoft Defender.

## Task 2: Configure and launch a Spear Phishing attack
> Se configura y lanza una simulación de Credentials Harvest ("PhishingTest1") usando un payload template predefinido, dirigida a todos los usuarios de Adatum, con landing page y notificaciones de entrenamiento configuradas.
* [WINDOWS] LON-CL1 -> Edge (Holly logueada con MFA)
  * [MENU] pestaña **Microsoft Defender** (si no está abierta -> https://security.microsoft.com y completar verificación/MFA si se solicita)
    * [MENU] sección **Email & collaboration** -> **Attack simulation training**
      * [DIALOG] Welcome to Attack simulation training -> **Close** (si aparece)
      * [TAB] Overview (por default)
        * NOTA: la simulación se puede lanzar desde el tab **Simulations** o desde el link **Launch a simulation** en Overview. Se recomienda usar Overview porque tiene información adicional sobre el tipo de ataque.
        * Scroll hasta la sección **Recommendations** -> buscar la recomendación **Launch a phishing simulation using other social engineering techniques**
        * Bajo esa recomendación -> **Create another simulation with new technique** (inicia el wizard Create Simulation)
          * [TAB] Select Technique
            * Revisar la info de **Credential Harvest** -> **View details of Credential harvest**
              * [DIALOG] pane Credential Harvest -> revisar Description y Simulation steps -> cerrar el pane
            * Seleccionar el technique **Credentials Harvest** (si no está seleccionado por default) -> **Next**
          * [TAB] Name Simulation
            * Simulation Name: `PhishingTest1`
            * Description: `This simulation provides insight on targeted email threats against users inside the company`
            * **Next**
          * [TAB] Select payload and login page -> tildar el checkbox del payload **Payment for Package** (si no está disponible, elegir otro payload) -> **Next**
          * [TAB] Target Users -> seleccionar **Include all users in my organization** -> **Next**
          * [TAB] Exclude users -> **Next**
          * [TAB] Assign Training -> sección Preferences -> verificar seleccionado **Assign training for me (Recommended)**
            * Due Date -> **7 days after Simulation ends** -> **Next**
          * [TAB] Select Phish landing page -> tab **Global landing pages** (por default)
            * Seleccionar el nombre **Microsoft Landing Page Template 1** para previsualizar
              * [DIALOG] preview del landing page -> revisar -> **Close**
            * Repetir con otros templates (seleccionar el nombre, no el checkbox) para comparar, tantas veces como se quiera
            * Una vez elegido el template a usar -> tildar su checkbox -> **Next**
          * [TAB] Select end user notification -> seleccionar **Microsoft default notification (recommended)**
            * **Microsoft default positive reinforcement notification** -> Delivery preferences: **Deliver after simulation ends**
            * **Microsoft default training reminder notification** -> Delivery preferences: **Weekly**
            * **Next**
          * [TAB] Launch Details -> seleccionar **Launch this simulation as soon as I'm done** -> **Next**
          * [TAB] Review Simulation -> revisar la configuración (usar **Edit** en la sección correspondiente si hace falta corregir algo) -> **Submit**
          * Esperar la confirmación **Simulation has been scheduled for launch** -> **Done**
    * ⚠️ Una vez lanzado el ataque simulado, puede tardar hasta 15 minutos en generarse el email y enviarse a todos los usuarios de Adatum. En vez de esperar, la validación del email y de los resultados de diagnóstico del ataque se hace en el Ejercicio 7, Task 4.
* Dejar Edge y todas las pestañas abiertas y continuar con el siguiente ejercicio

---

# Learning Path 6 - Lab 6 - Exercise 6 - Conduct a Drive-by URL attack using Attack Simulation training

> Se configura y lanza una simulación de Drive-by URL ("Custom payload") dirigida únicamente a Lynne Robbins, usando un payload custom ("Free gift offer") creado desde cero con la marca falsa Tailspin Toys, incluyendo un phishing link, un indicator de tipo "too good to be true" y su propia landing page.
> ℹ️ En un ataque Drive-by URL, el target recibe un email con un link a un sitio comprometido o clonado; al hacer click, corre código en background que recolecta información o despliega código malicioso en el dispositivo. A diferencia del ejercicio anterior (payload template + todos los usuarios), acá se usa un payload propio y se apunta solo a Lynne Robbins.

## Task 1: Configure and launch a Drive-by URL attack
* [WINDOWS] LON-CL1 -> Edge (Holly logueada en Microsoft 365)
  * [MENU] pestaña **Microsoft Defender** (si no está abierta -> Microsoft 365 admin center -> Admin centers -> **Security**)
    * [MENU] sección **Email & collaboration** -> **Attack simulation training**
      * [TAB] Overview (por default) -> seleccionar tab **Simulations**
        * [MENU] **+Launch a simulation** (inicia el Simulation wizard)
          * [TAB] Select technique -> scroll y seleccionar **Drive-by URL**
            * [LINK] **View details of Drive-by URL**
              * [DIALOG] pane Drive-by URL -> revisar Description y Simulation steps -> cerrar el pane
            * **Next**
          * [TAB] Name Simulation -> Simulation name: `Custom payload` -> **Next**
          * [TAB] Select payload and login page -> tab Global payloads (por default) -> seleccionar tab **Tenant payloads**
            * [MENU] **+Create a payload** (inicia el Payload wizard)
              * [TAB] Select type -> **Email** (seleccionado por default, puede estar deshabilitado) -> **Next**
              * [TAB] Select technique -> **Drive-by URL** (ya seleccionado, resto de opciones deshabilitadas) -> **Next**
              * [TAB] Payload Name
                * Payload name: `Free gift offer`
                * Description: `This payload is for Drive-by URL threats offering free prizes and gifts that are too good to be true`
                * **Next**
              * [TAB] Configure Payload
                * From name: `Klemen Sic`
                * From email: `klemens@tailspintoys.com`
                * Email subject: `Free toy giveaway promotion from Tailspin Toys`
                * Select a URL you want to be your phishing link -> **Select URL**
                  * [DIALOG] pane de URLs predefinidas -> Search: `prizegives` -> seleccionar **https://www.prizegives.com** -> **Confirm**
                * Theme: **Personalized Offer**
                * Industry: **Retail**
                * Current Event: **Yes**
                * Select the language for payload: **English**
                * Email message -> tab **Text** -> ingresar en el cuerpo del mensaje:
                  `Tailspin Toys is offering you a FREE, one-time only giveaway of a toy of your choice as part of our 25th anniversary celebration! Please click on the following link to select the toy of your choice:`
                  * Arriba del cuadro de mensaje, a la derecha de Dynamic tag -> botón **Phishing link**
                    * [DIALOG] Name Phishing Url -> Name: `Free25thAnniversaryGift@tailspintoys.com` -> **Confirm**
                  * ⚠️ Verificar que quede un espacio entre los dos puntos finales y el inicio del link para que se vea prolijo. El mensaje final debe quedar como: "...Please click on the following link to select the toy of your choice: Free25thAnniversaryGift@tailspintoys.com"
                * **Next**
              * [TAB] Add Indicators -> **Add Indicator**
                * [DIALOG] pane Add Indicator
                  * Select an indicator you would like to use: **Too good to be true offers**
                  * Where do you want to place this indicator on payload: **From the Body of the Email**
                  * Botón **Select Text**
                    * [DIALOG] pane Select the required text -> arrastrar el cursor desde el inicio hasta el final del bloque de código para resaltarlo por completo (habilita el botón Select) -> **Select**
                  * Indicator Description -> reemplazar el texto default por: `Free gifts or other one-time only promotional giveaways`
                  * Click dentro del área Indicator Preview para ver la preview -> click afuera para salir de la preview
                  * **Add** (abajo del pane)
                * Verificar que el indicator recién creado aparece en la página Add Indicators -> **Next**
              * [TAB] Review Payload -> revisar la configuración (usar **Edit** en la sección correspondiente, o **Back** para volver a la sección Configure si hace falta) -> **Submit**
              * Confirmación **New payload created** -> **Done**
          * [TAB] Select payload and login page -> el payload **Free gift offer** ya debería aparecer en la lista -> tildar su checkbox -> **Next**
          * [TAB] Target Users -> verificar seleccionado **Include only specific users and groups** -> **+Add Users**
            * [DIALOG] pane Add Users -> campo Search for Users or Groups: `Lynne` -> Enter -> seleccionar **Lynne Robbins** -> **Add 1 User(s)**
            * Verificar que Lynne Robbins aparece como targeted user -> **Next**
          * [TAB] Exclude users -> **Next**
          * [TAB] Assign Training -> sección Preferences -> verificar seleccionado **Assign training for me (Recommended)**
            * Due Date -> **7 days after Simulation ends** -> **Next**
          * [TAB] Select Phish landing page -> tab **Global landing pages** (por default)
            * Seleccionar el nombre **Microsoft Landing Page Template 1** para previsualizar
              * [DIALOG] preview del landing page -> revisar -> **Close**
            * Repetir con otros templates (seleccionar el nombre, no el checkbox) para comparar, tantas veces como se quiera
            * Una vez elegido el template a usar -> tildar su checkbox -> **Next**
          * [TAB] Select end user notification -> seleccionar **Microsoft default notification (recommended)**
            * **Microsoft default positive reinforcement notification** -> Delivery preferences: **Deliver after simulation ends**
            * **Microsoft default training reminder notification** -> Delivery preferences: **Weekly**
            * **Next**
          * [TAB] Launch Details -> seleccionar **Launch this simulation as soon as I'm done** -> **Next**
          * [TAB] Review Simulation -> revisar la configuración (usar **Edit** en la sección correspondiente si hace falta corregir algo) -> **Submit**
          * Esperar la confirmación **Simulation has been scheduled for launch** -> **Done**
    * ⚠️ Una vez lanzado el ataque simulado de Drive-by URL, debería enviarse un email a Lynne Robbins, lo que puede tardar hasta 15 minutos. En vez de esperar, la validación del email y de los resultados de diagnóstico del ataque se hace en el Ejercicio 7, Task 5.
* Dejar Edge y todas las pestañas abiertas y continuar con el siguiente ejercicio

---

# Learning Path 6 - Lab 6 - Exercise 7 - Validate alert notifications and simulated attacks

> Se validan los 5 emails generados por los ejercicios anteriores: las 3 alert policies (Exercises 2 a 4) y los 2 ataques simulados (Exercises 5 y 6). Cada uno pudo haber tardado hasta 15 minutos en generarse; al llegar a este punto ya debería estar todo disponible, sin necesidad de esperar.
> ℹ️ Si algún email todavía no llegó al revisar el Inbox correspondiente, usar el ícono de Refresh junto a la barra de direcciones y esperar un poco más.

## Task 1: Validate the Mailbox Permission Alert
> Se valida que Lynne Robbins recibió el email de alerta por el cambio de permisos FullAccess en el mailbox de Alex Wilber (Exercise 2), y se revisa el detalle del alert en Microsoft Defender.
* [WINDOWS] Switch a **LON-CL2** (logueado como local Admin, lon-cl2\admin)
  * [MENU] ícono **Microsoft Edge** en la taskbar -> maximizar
* [BROWSER] `https://outlook.office365.com`
  * [LOGIN] Pick an account -> si aparece **Lynne Robbins** (LynneR@xxxxxZZZZZZ.onmicrosoft.com) seleccionarla; si no -> **Use another account** -> `LynneR@xxxxxZZZZZZ.onmicrosoft.com` -> password: la New User Password asignada a Lynne -> **Sign in**
  * [TAB] Inbox -> deberían haber llegado hoy 2 emails enviados por **Office365Alerts@microsoft.com**
    * El primero corresponde a la alerta de Exercise 2: informa que Holly Dickson hizo un Mailbox permission change
    * ⚠️ El botón **View alert details** dentro del email dejó de funcionar desde agosto 2025 por un cambio de configuración en el portal de Defender XDR
  * [MENU] abrir nueva pestaña
* [BROWSER] `https://security.microsoft.com`
  * [MENU] nav pane izquierdo -> expandir **Incidents & alerts** -> **Email and collaboration alerts**
    * [TAB] View alerts -> seleccionar el alert **Mailbox permission change** (nombre, no checkbox)
      * [DIALOG] pane Mailbox permission change -> scroll y revisar toda la información de la actividad -> **Close**
  * Cerrar la pestaña **View Alerts - Microsoft Defender**
* Dejar abierta la pestaña de Outlook de Lynne (se usa en el siguiente task) y el browser abierto en LON-CL2

Con esto queda validada la mailbox permission alert que avisa cuando se otorga FullAccess sobre un mailbox de usuario.

## Task 2: Validate the SharePoint Permissions Alert
> Se valida que Lynne recibió el email de alerta por haber agregado a Alex Wilber como site collection administrator (Exercise 3), usando esta vez el preview pane de Outlook para que el botón View alert details funcione.
* [WINDOWS] LON-CL2 -> Edge -> Outlook de Lynne (sigue logueada del task anterior)
  * [TAB] Inbox -> el segundo de los dos emails de **Office365Alerts@microsoft.com** corresponde a la SharePoint Permissions alert de Exercise 3
    * Seleccionar el email en la lista (sin abrirlo) para verlo en el **preview pane**
      * ⚠️ El botón View alert details no funciona si se abre el email completo, pero sí funciona desde el preview pane
      * En el preview pane -> **View alert details** (abre el Microsoft Defender portal en nueva pestaña)
* [BROWSER] Microsoft Defender -> ventana Alerts -> se abre automáticamente el pane **Add user as a site collection administrator**
  * Scroll y revisar toda la información de la actividad -> **Close**
* Dejar LON-CL2 abierto (se usa el mailbox de Lynne más adelante en este ejercicio)

Con esto queda validada la alerta de SharePoint que monitorea permisos de site collection admin.

## Task 3: Validate the default eDiscovery Alert
> Se valida que Holly recibió el email default de eDiscovery search started or exported (Exercise 4), y opcionalmente se revisan las estadísticas del search "Confidential search" en Microsoft Purview.
* [WINDOWS] Switch a **LON-CL1** -> Edge (Holly logueada en Microsoft 365)
  * [MENU] pestaña con el mailbox de Holly (si no hay ninguna abierta -> [MENU] pestaña Home | Microsoft 365 -> columna de apps -> **Outlook**)
* [BROWSER] Outlook de Holly
  * [TAB] Inbox -> buscar el email de severidad Informational: **eDiscovery search started or exported**, enviado por la alerta default habilitada en Exercise 4
    * Seleccionar el email en la lista (sin abrirlo) para verlo en el **preview pane**
      * ⚠️ El botón View alert details solo funciona desde el preview pane, no abriendo el email
      * En el preview pane -> **View alert details** (abre el Microsoft Defender portal en nueva pestaña)
* [BROWSER] Microsoft Defender -> ventana Alerts -> se abre automáticamente el pane **eDiscovery search started or exported**
  * Scroll y revisar toda la información de la actividad -> **Close**

### Opcional: revisar las estadísticas del eDiscovery search
* [WINDOWS] LON-CL1 -> pestaña **Home - Microsoft 365 admin center**
  * [MENU] **Compliance** (abre Microsoft Purview portal)
* [BROWSER] Microsoft Purview
  * [MENU] **Solutions** -> **eDiscovery**
    * [MENU] sección Classic eDiscovery -> **Content Search**
      * [TAB] Search (por default) -> seleccionar **Confidential search** de la lista
        * [DIALOG] pane Confidential search -> tab **Summary** (por default) -> revisar información
        * tab **Search statistics** -> expandir cada una de las 3 secciones (**Search content**, **Condition report**, **Top locations**) y revisar el contenido
        * **Close**
* Dejar la pestaña Outlook de Holly (Mail - Holly Dickson - Outlook) abierta en LON-CL1 (se usa más adelante), junto con el resto de las pestañas

Con esto queda validada la alerta default de eDiscovery que monitorea la creación de searches o la exportación de datos.

## Task 4: Validate the simulated Spear Phishing attack
> Se verifica que el email de spear phishing llegó al Inbox de Holly, se simula caer en el ataque (ingresando credenciales en la fake landing page), se revisa el training reminder y los resultados diagnósticos de la simulación PhishingTest1.
* [WINDOWS] LON-CL1 -> Edge -> Outlook de Holly
  * [TAB] Inbox -> localizar el email enviado por el Attack Simulator (subject y texto varían según el payload elegido, ej: "2 Failed messages to you")
    * ⚠️ No abrir el email (el botón no funciona al abrirlo) -> seleccionarlo para verlo en el **preview pane**
    * En el preview pane -> revisar el mensaje (busca simular una notificación legítima del sistema)
    * **View Returned Messages** (el botón/link del ataque simulado)
* [BROWSER] Se abre una fake sign-in box
  * Ingresar `Holly@xxxxZZZZZZ.onmicrosoft.com` -> **Next** -> password: la New Administrative Password de Holly -> **Sign in**
  * Se muestra la página que indica que Holly "fue phisheada" por el equipo de seguridad, con tips para identificar mensajes de phishing -> revisar el contenido
  * Al pie de la página -> **Go to training** (abre nueva pestaña con training sobre Web Phishing)
* [WINDOWS] volver a la pestaña con el mailbox de Holly
  * Verificar que llegó un email adicional del **Security and Compliance Team** (el training reminder semanal configurado en Exercise 5)
* [WINDOWS] pestaña **Attack simulation training** (o Microsoft Defender -> nav pane -> **Attack simulation training**)
  * Seleccionar la simulación **PhishingTest1** para ver los resultados diagnósticos
    * [DIALOG] pane PhishingTest1 -> revisar toda la información recopilada del ataque simulado -> cerrar con la **X**
* Dejar el browser abierto en LON-CL1 sin cerrar ninguna pestaña

## Task 5: Validate the simulated Drive-by URL attack
> Se verifica que el email del Drive-by URL attack llegó al Inbox de Lynne, se simula caer en el ataque haciendo click en el phishing link, se revisa el training reminder y los resultados diagnósticos de la simulación Custom payload. Por último se cierra sesión de Lynne en LON-CL2 y se deshabilita MFA para Holly.
* [WINDOWS] Switch a **LON-CL2** -> Edge -> pestaña con el mailbox de Lynne (abierta desde tasks anteriores)
  * [TAB] Inbox -> localizar el email de **Klemen Sic** (klemens@tailspintoys.com), Subject: **Free toy giveaway promotion from Tailspin Toys**
    * ⚠️ No abrir el email -> seleccionarlo para verlo en el **preview pane**
    * En el preview pane -> click en el link **Free25thAnniversaryGift@tailspintoys.com**
* [BROWSER] Se abre la página del ataque simulado: indica que fue "phisheada" por el equipo de IT, explica que sitios de apariencia legítima como https://www.prizegives.com pueden estar comprometidos, y muestra qué información se hubiera podido capturar en un ataque real
* [WINDOWS] volver a la pestaña con el mailbox de Lynne
  * Verificar que llegó un email adicional del **Security and Compliance Team** (training reminder semanal legítimo configurado en Exercise 6)
  * [MENU] foto de **Lynne Robbins** (esquina superior derecha) -> **Sign out**
* Cerrar el Edge de LON-CL2
* [WINDOWS] Switch a **LON-CL1** -> pestaña **Attack simulation training** (Holly)
  * Seleccionar la simulación **Custom payload** para ver los resultados diagnósticos
    * [DIALOG] pane Custom payload -> revisar toda la información recopilada del ataque simulado -> cerrar con la **X**
* Cerrar todas las pestañas EXCEPTO **Home | Microsoft 365** y **Home | Microsoft 365 admin center**

## Task 6: Disable Multifactor Authentication for the attack simulation admin
> Ahora que terminaron los tests de Attack simulation training, se deshabilita MFA en la cuenta de Holly para que no tenga que lidiar con MFA durante el resto del pilot project.
* [WINDOWS] LON-CL1 -> Edge -> pestaña **Home | Microsoft 365 admin center**
  * [MENU] **Users** -> **Active users**
    * [MENU] barra de menú arriba de la lista -> **Multi-factor authentication**
* [BROWSER] multi-factor authentication
  * [TAB] users (por default) -> verificar que todos los usuarios están en **Disabled**, excepto **Holly Dickson**, cuyo status es **Enforced**
    * ⚠️ Al habilitar MFA a Holly en Exercise 5 su status pasó de Disabled a Enabled; la primera vez que se loguea con MFA activo, el sistema cambia automáticamente el status de Enabled a Enforced
  * Tildar el checkbox de **Holly Dickson** -> en el pane de properties -> **Disable**
    * [DIALOG] Disable multi-factor authentication? -> **yes**
    * [DIALOG] Updates successful -> **close**
  * Verificar que el MFA Status de Holly cambió a **Disabled**

### Cerrar sesión y volver a loguearse sin MFA
* [MENU] ícono de usuario **HD** (esquina superior derecha) -> **Sign out**
* Cerrar Edge por completo (limpia la cache)
* [WINDOWS] LON-CL1 -> abrir Edge nuevamente
* [BROWSER] `https://www.microsoft365.com`
  * [LOGIN] Pick an account -> seleccionar la cuenta de **Holly** -> password: la New Administrative Password de Holly -> **Sign in**
  * [TAB] Home | Microsoft 365 -> ícono **Admin** -> navega al Microsoft 365 admin center

Con esto queda todo listo para continuar con el siguiente lab exercise.

**End of Lab 6**

# Privileged Identity Management - Aprobación del rol Global Administrator

> Se implementa Privileged Identity Management (PIM) para el rol Global Administrator: se configura el rol para requerir aprobación con Holly Dickson como approver, se crea un grupo asignable a roles (PIM-Global-Administrators) con Patti Fernandez como miembro eligible, se envía una solicitud de activación desde Patti y se aprueba desde Holly.
> ⚠️ Best practice: la cuenta MOD Administrator (primer Global Admin, no personalizada) NO debe tener MFA activado. Los Global Admins personalizados (Holly, Patti, etc.) sí deben tener MFA.

## Task 1: Configurar el rol Global Administrator para requerir aprobación
> Se habilita "Require approval to activate" en el rol Global Administrator, se asigna a Holly como approver y se configuran las notificaciones adicionales hacia la cuenta MOD Administrator.
* [WINDOWS] LON-CL1 -> Browser (Holly logueada en Microsoft 365, admin center abierto)
* [MENU] Microsoft 365 admin center -> Admin centers -> **Identity** (si abre pestaña Sign in to Microsoft Entra -> Pick an account -> Holly -> password -> Stay signed in? -> Don't show this again -> Yes)
* [MENU] Entra admin center -> **ID governance** -> **Privileged Identity Management**
* [MENU] Quick start -> Manage -> **Microsoft Entra roles** -> Manage -> **Roles**
* Seleccionar rol **Global Administrator** (ordenar por columna Role si no están alfabéticos)
* [MENU] Role settings -> **Edit**
  * [TAB] Activation
    * Verificar **Azure MFA** tildado en "On activation, require"
    * Tildar **Require approval to activate** (habilita Select approver(s))
    * **Select approver(s)** -> buscar `Holly` -> seleccionar **Holly@xxxxxZZZZZZ.onmicrosoft.com** (⚠️ NO la cuenta del dominio custom) -> Select
  * [TAB] Notification
    * 3 eventos: assigned as eligible / assigned as active / eligible members activate
    * En **Additional recipients** de cada alerta (Role assignment alert x2, Role activation alert x1) -> agregar `admin@xxxxxZZZZZZ.onmicrosoft.com`
  * **Update**
* Dejar todas las pestañas abiertas para el siguiente task

## Task 2: Crear grupo eligible y asignarlo al rol Global Admin
> Se crea un grupo de seguridad asignable a roles (PIM-Global-Administrators) con Patti como miembro, y se asigna ese grupo como eligible al rol Global Administrator.
* [WINDOWS] LON-CL1 -> Entra admin center (Holly)
* [MENU] Groups -> **All groups** -> **New group**
  * ⚠️ Group type: **Security** (NO Microsoft 365/Teams; solo los grupos de Security pueden asignarse a roles)
  * Group name: `PIM-Global-Administrators`
  * Group description: `Group of eligible users that can be assigned to the Global Administrator role in PIM`
  * Microsoft Entra roles can be assigned to the group: **Yes**
  * Membership type: **Assigned**
  * Owners -> buscar `Holly` -> **Holly@xxxxxZZZZZZ.onmicrosoft.com**
  * Members -> buscar `Patti` -> Patti Fernandez
  * **Create**
  * [DIALOG] "Creating a group to which roles can be assigned cannot be changed later" -> **Yes**
  * [TAB] All groups -> si **PIM-Global-Administrators** no aparece -> **Refresh**
* [MENU] ID Governance -> **Privileged Identity Management** -> Manage -> **Microsoft Entra roles**
* Sección **Assign** -> **Assign Eligibility**
* Seleccionar rol **Global Administrator** -> **+Add assignments**
  * [TAB] Membership -> **No member selected** -> buscar `PIM` -> tildar **PIM-Global-Administrators** -> Select
  * [TAB] Setting (**Next**) -> Assignment type: **Eligible** -> verificar **Permanently eligible** tildado -> **Assign**
* [MENU] Manage -> **Assignments**
  * [TAB] Eligible assignments -> verificar que aparece PIM-Global-Administrators
    * ⚠️ Puede demorar hasta 30 min en aparecer -> **Refresh** periódicamente
* Dejar todo abierto para el siguiente task

## Task 3: Solicitar activación del rol Global Admin (como Patti)
> Se inicia sesión como Patti Fernandez en una ventana InPrivate y se activa el rol Global Administrator eligible, configurando MFA por teléfono en el proceso.
* [WINDOWS] LON-CL1 -> Edge -> click derecho ícono taskbar -> **New InPrivate window**
* [LOGIN] `https://portal.azure.com` -> `PattiF@xxxxxZZZZZZ.onmicrosoft.com` -> Next -> User Password -> Sign in
  * [DIALOG] Update your password -> Current password (User Password) -> New/Confirm (New User Password) -> Sign in
  * Stay signed in? -> Don't show this again -> Yes
  * Welcome to Microsoft Azure -> **Cancel**
* [MENU] Azure services -> **More services** -> buscar `priv` -> **Microsoft Entra Privileged Identity Management**
* [MENU] Tasks -> **My Roles**
  * [TAB] Eligible assignments -> fila Global Administrator -> **Activate**
    * [DIALOG] Activate - Global Administrator -> warning de verificación adicional -> click para continuar
    * **More information required** -> Next
    * [MENU] Microsoft Authenticator page -> **I want to set up a different method** (⚠️ no confundir con "I want to use a different authenticator app")
    * [DIALOG] Choose a different method -> **Phone** -> Confirm
    * Elegir país -> ingresar número -> **Receive a code** -> Next
    * Ingresar código de 6 dígitos -> Next -> Next -> **Done**
    * ⚠️ Si se demora demasiado, timeout -> volver a loguear con password de Patti y repetir MFA
    * [DIALOG] Activate - Global Administrator -> Reason: `Testing PIM` -> **Activate**
  * [TAB] Active assignments -> ⚠️ el rol todavía no aparece (falta aprobación de Holly)
* Dejar la ventana InPrivate abierta para el siguiente task

## Task 4: Aprobar la solicitud (como Holly)
> Desde la sesión original de Holly se revisa y aprueba la solicitud de Patti.
* [WINDOWS] LON-CL1 -> Edge (ventana original, Holly) -> pestaña Global Administrator | Assignments
* [MENU] Navegación superior -> **Privileged Identity Management | Microsoft Entra roles**
* [MENU] Quick start -> Tasks -> **Approve requests**
  * [TAB] Requests for role activations -> tildar solicitud de Patti (Global Administrator) -> **Approve**
    * [DIALOG] Approve Request -> Justification: `PIM testing` -> **Confirm**
* Dejar todo abierto para el siguiente task

## Task 5: Verificar que el rol quedó activo
> Se confirma la activación del rol Global Administrator para Patti, tanto desde su propia sesión como desde la vista de Holly en Entra admin center.
* [WINDOWS] Volver a ventana InPrivate (Patti)
  * [TAB] Active assignments -> **Refresh** -> verificar que **Global Administrator** ya aparece activo
* [WINDOWS] LON-CL1 -> Edge (ventana original, Holly) -> Entra admin center
* [MENU] Privileged Identity Management -> Microsoft Entra roles -> Assignments -> rol **Global Administrator**
  * [TAB] Active assignments -> verificar que **Patti Fernandez** figura con la fecha de expiración de la activación

---

# Privileged Identity Management - Self-Approval del rol Helpdesk Administrator

> Se configura el rol Helpdesk Administrator en PIM para self-activation: se crea un grupo eligible (PIM-Helpdesk-Administrators) con Alex Wilber y Joni Sherman, se configura el rol para que no requiera aprobación (solo justification) con asignaciones que expiran a los 15 días, se prueba la self-activation como Alex y se verifica que Holly recibió la notificación correspondiente.

## Task 1: Crear grupo eligible para el rol Helpdesk Administrator
> Se crea un grupo de seguridad asignable a roles (PIM-Helpdesk-Administrators) con Alex y Joni como miembros, y se asigna ese grupo como eligible al rol Helpdesk Administrator.
* [WINDOWS] LON-CL1 -> Entra admin center (Holly)
* [MENU] Groups -> **All groups** -> **New group**
  * ⚠️ Group type: **Security** (NO Microsoft 365/Teams; solo los grupos de Security pueden asignarse a roles)
  * Group name: `PIM-Helpdesk-Administrators`
  * Group description: `Group of eligible users who can be assigned to the Helpdesk Administrator role in PIM`
  * Microsoft Entra roles can be assigned to the group: **Yes**
  * Membership type: **Assigned**
  * Owners -> buscar `Holly` -> **Holly@xxxxxZZZZZZ.onmicrosoft.com**
  * Members -> seleccionar **Alex Wilber** -> buscar `Joni` -> seleccionar **Joni Sherman**
  * **Create**
  * [DIALOG] "Creating a group to which roles can be assigned cannot be changed later" -> **Yes**
  * [TAB] All groups -> si **PIM-Helpdesk-Administrators** no aparece debajo de PIM-Global-Administrators -> **Refresh**
* [MENU] ID Governance -> **Privileged Identity Management** -> Manage -> **Microsoft Entra roles**
* Sección **Assign** -> **Assign Eligibility**
* Seleccionar rol **Helpdesk Administrator** -> **+Add assignments**
  * [TAB] Membership -> **No member selected** -> buscar `PIM` -> tildar **PIM-Helpdesk-Administrators** -> Select
  * [TAB] Setting (**Next**) -> Assignment type: **Eligible** -> verificar **Permanently eligible** tildado -> **Assign**
* [MENU] Manage -> **Assignments**
  * [TAB] Eligible assignments -> verificar que aparece PIM-Helpdesk-Administrators
    * ⚠️ Puede demorar hasta 30 min en aparecer -> **Refresh** periódicamente
* Dejar todo abierto para el siguiente task

## Task 2: Configurar el rol Helpdesk Administrator para self-activation
> Se ajustan Activation, Assignment y Notification del rol para permitir self-approval (sin approval requerido, solo justification), con activaciones de hasta 24 hs y asignaciones que expiran a los 15 días, notificando a Holly cuando alguien active el rol.
* [WINDOWS] LON-CL1 -> Entra admin center (Holly)
* [MENU] ID Governance -> **Privileged Identity Management** -> Manage -> **Microsoft Entra roles** -> Manage -> **Roles**
* Seleccionar rol **Helpdesk Administrator** (ordenar por columna Role si no están alfabéticos)
* [MENU] Role settings -> **Edit**
  * [TAB] Activation
    * Activation maximum duration (hours): mover slider o escribir `24` (⚠️ 24 hs es el máximo permitido)
    * On activation, require: **None**
    * Verificar que los 3 checkboxes (Require justification on activation, Require approval to activate, Require ticket information) queden **destildados**
      * ⚠️ Al no tildar "Require approval to activate", los eligible users podrán self-approve sin aprobación de otro usuario
  * [TAB] Assignment
    * Destildar **Allow permanent active assignment**
    * **Expire active assignments after** -> `15 days`
    * Verificar tildado **Require justification on active assignment**
  * [TAB] Notification
    * Sección "Send notifications when eligible members activate this role"
      * Verificar tildado **Role activation alert** (destinatario default: Admin = Global Admins + Privileged Role Admins)
      * Destildar **Notification to activated user (requestor)** (Alex y Joni no necesitan notificación de su propia self-approval)
  * **Update**
* Dejar todo abierto para el siguiente task

## Task 3: Self-activar el rol Helpdesk Admin (como Alex)
> Se inicia sesión como Alex Wilber en una ventana InPrivate y se self-activa el rol Helpdesk Administrator eligible, sin requerir aprobación de otro usuario.
* [WINDOWS] LON-CL1 -> Edge -> click derecho ícono taskbar -> **New InPrivate window**
* [LOGIN] `https://portal.azure.com` -> `AlexW@xxxxxZZZZZZ.onmicrosoft.com` -> Next -> User Password -> Sign in
  * [DIALOG] Update your password -> Current password (User Password) -> New/Confirm (New User Password) -> Sign in
  * Stay signed in? -> Don't show this again -> Yes
  * Welcome to Microsoft Azure -> **Cancel**
* [MENU] Azure services -> **More services** -> buscar `priv` -> **Microsoft Entra Privileged Identity Management**
* [MENU] Tasks -> **My Roles**
  * [TAB] Eligible assignments -> verificar que aparece Helpdesk Administrator
  * [TAB] Active assignments -> verificar que todavía no hay roles asignados
  * [TAB] Eligible assignments -> fila Helpdesk Administrator -> **Activate**
    * [DIALOG] Activate - Helpdesk Administrator -> Reason: `Support requests from Sales team members that require resolution` -> **Activate**
    * Esperar a que se completen las 3 etapas de activación (⚠️ Stage 2 suele demorar más) -> el panel se cierra automáticamente
  * [TAB] Eligible assignments -> mensaje "Your active roles have changed. Click here to view your active roles." -> click en el mensaje
  * [TAB] Active assignments -> verificar que **Helpdesk Administrator** ya aparece asignado
* Cerrar la sesión InPrivate (vuelve al Entra admin center)
* Dejar todo abierto para el siguiente task

## Task 4: Verificar que se emitió la notificación de PIM
> Se confirma que Holly recibió el email de notificación por la self-activation de Alex, y se revisa el Resource audit en Entra admin center.
* [WINDOWS] LON-CL1 -> Edge -> pestaña **Home | Microsoft 365**
* [MENU] Ícono **Outlook** (columna de apps a la izquierda) -> abre el mailbox de Holly en nueva pestaña
  * [TAB] Inbox -> verificar email de PIM indicando que **Alex Wilber** activó el Helpdesk Administrator role assignment
  * Abrir el email -> revisar información -> cerrar
* [WINDOWS] Volver a pestaña **Microsoft Entra admin center** (Adatum Corporation - Settings)
* [MENU] Sección Activity -> **Resource audit**
  * Revisar las 2 actividades más recientes: solicitud de Alex para el rol Helpdesk Administrator y la finalización de esa solicitud

---

# Privileged Identity Management - Aprobación entre compañeros del rol Intune Administrator

> Se implementa un tercer modelo de aprobación en PIM: en vez de un admin (Holly) o self-approval, Alex Wilber y Joni Sherman se aprueban mutuamente las solicitudes de activación del rol Intune Administrator. Se crea el grupo eligible, se configura el rol para requerir aprobación de un miembro del propio grupo, se verifica que un usuario no puede auto-aprobar su propia solicitud, y se confirma la notificación a Holly y el registro en el audit log.

## Task 1: Crear grupo eligible para el rol Intune Administrator
> Se crea un grupo de seguridad asignable a roles (PIM-Intune-Administrators) con Alex y Joni como miembros, y se asigna ese grupo como eligible al rol Intune Administrator.
* [WINDOWS] LON-CL1 -> Entra admin center (Holly)
* [MENU] Groups -> **All groups** -> **New group**
  * ⚠️ Group type: **Security** (NO Microsoft 365/Teams; solo los grupos de Security pueden asignarse a roles)
  * Group name: `PIM-Intune-Administrators`
  * Group description: `Group of eligible users who can be assigned to the Intune Administrator role in PIM`
  * Microsoft Entra roles can be assigned to the group: **Yes**
  * Membership type: **Assigned**
  * Owners -> buscar `Holly` -> **Holly@xxxxxZZZZZZ.onmicrosoft.com**
  * Members -> seleccionar **Alex Wilber** -> buscar `Joni` -> seleccionar **Joni Sherman**
  * **Create**
  * [DIALOG] "Creating a group to which roles can be assigned cannot be changed later" -> **Yes**
  * [TAB] All groups -> si **PIM-Intune-Administrators** no aparece -> **Refresh** (puede demorar unos minutos)
* [MENU] ID Governance -> **Privileged Identity Management** -> Manage -> **Microsoft Entra roles**
* Sección **Assign** -> **Assign Eligibility**
* Seleccionar rol **Intune Administrator** -> **+Add assignments**
  * [TAB] Membership -> **No member selected** -> buscar `PIM` -> tildar **PIM-Intune-Administrators** -> Select
  * [TAB] Setting (**Next**) -> Assignment type: **Eligible** -> verificar **Permanently eligible** tildado -> **Assign**
* [MENU] Manage -> **Assignments**
  * [TAB] Eligible assignments -> verificar que aparece PIM-Intune-Administrators
    * ⚠️ Puede demorar hasta 30 min en aparecer -> **Refresh** periódicamente
* Dejar todo abierto para el siguiente task

## Task 2: Configurar el rol Intune Administrator para requerir aprobación entre pares
> Se configura el rol sin justification en la activación, con approval requerido, asignando al propio grupo PIM-Intune-Administrators como approver (para que Alex y Joni se aprueben mutuamente), y con notificaciones a Holly.
* [WINDOWS] LON-CL1 -> Entra admin center (Holly)
* [MENU] ID Governance -> **Privileged Identity Management** -> Manage -> **Microsoft Entra roles** -> Manage -> **Roles**
* Seleccionar rol **Intune Administrator** (ordenar por columna Role si no están alfabéticos)
* [MENU] Role settings -> **Edit**
  * [TAB] Activation
    * On activation, require: **None**
    * Destildar **Require justification on activation** (si está tildado)
    * Tildar **Require approval to activate** (habilita Select approver(s))
    * **Select approver(s)** -> buscar `PIM` -> seleccionar **PIM-Intune-Administrators** (grupo) -> Select
      * ⚠️ Al asignar el propio grupo como approver, cualquier miembro (Alex o Joni) recibe la notificación para aprobar la solicitud del otro
  * [TAB] Assignment -> verificar tildado **Require justification on active assignment**
  * [TAB] Notification -> sección "Send notifications when eligible members activate this role"
    * Verificar tildado **Role activation alert** (destinatario default: Admin = Global Admins + Privileged Role Admins)
    * Destildar **Notification to activated user (requestor)** (se aprueban entre ellos, no necesitan notificación propia)
    * Verificar tildado **Request to approve an activation**
  * **Update**
* Dejar todo abierto para el siguiente task

## Task 3: Solicitar el rol Intune Admin (como Joni)
> Se inicia sesión como Joni Sherman en una ventana InPrivate y se solicita la activación del rol Intune Administrator eligible, que queda pendiente de aprobación por otro miembro del grupo.
* [WINDOWS] LON-CL1 -> Edge -> click derecho ícono taskbar -> **New InPrivate window**
* [LOGIN] `https://portal.azure.com` -> `JoniS@xxxxxZZZZZZ.onmicrosoft.com` -> Next -> User Password -> Sign in
  * [DIALOG] Update your password -> Current password (User Password) -> New/Confirm (New User Password) -> Sign in
  * Stay signed in? -> Don't show this again -> Yes
  * Welcome to Microsoft Azure -> **Cancel** (si aparece)
* [MENU] Azure services -> **More services** -> buscar `priv` -> **Microsoft Entra Privileged Identity Management**
* [MENU] Tasks -> **My Roles**
  * [TAB] Eligible assignments -> fila Intune Administrator -> **Activate**
    * [DIALOG] Activate - Intune Administrator -> Reason: `Device management support requests from various users that require resolution` -> **Activate**
  * [TAB] Active assignments -> ⚠️ el rol todavía no aparece (falta aprobación de un miembro del grupo)
* Dejar la ventana InPrivate abierta para el siguiente task

## Task 4: Aprobar la solicitud del rol Intune Admin
> Se verifica primero que Joni no puede auto-aprobar su propia solicitud, y luego se aprueba desde la sesión de Alex, confirmando finalmente la asignación desde Joni.
* [WINDOWS] Seguir en la ventana InPrivate de Joni (o volver a loguearse si se cerró la sesión)
* [MENU] Navegación superior -> **Privileged Identity Management | My roles**
* [MENU] Tasks -> **Approve requests**
  * [TAB] Requests to renew or extend role assignments -> verificar que Joni **no tiene** solicitudes propias pendientes de aprobar
    * ⚠️ Confirma que un miembro del grupo approver no puede self-approve su propia solicitud, aunque sea parte del grupo
* Cerrar la sesión InPrivate de Joni
* [WINDOWS] Nueva ventana InPrivate -> `https://portal.azure.com`
* [LOGIN] `AlexW@xxxxxZZZZZZ.onmicrosoft.com` -> Next -> New User Password (definida en el lab anterior) -> Sign in
  * Stay signed in? -> Don't show this again -> Yes
  * Welcome to Microsoft Azure -> **Cancel** (si aparece)
* [MENU] Azure services -> **More services** -> buscar `priv` -> **Microsoft Entra Privileged Identity Management**
* [MENU] Tasks -> **Approve requests**
  * [TAB] Requests for role activations -> tildar solicitud de Joni (Intune Administrator) -> **Approve**
    * [DIALOG] Approve Request -> Justification: `PIM testing` -> **Confirm**
* Cerrar la sesión InPrivate de Alex
* [WINDOWS] Nueva ventana InPrivate -> `https://portal.azure.com`
* [LOGIN] `JoniS@xxxxxZZZZZZ.onmicrosoft.com` -> Next -> New User Password -> Sign in
  * Stay signed in? -> Don't show this again -> Yes
* [MENU] Azure services -> **More services** -> buscar `priv` -> **Microsoft Entra Privileged Identity Management**
* [MENU] Tasks -> **My roles**
  * [TAB] Active assignments -> verificar que **Intune Administrator** ya aparece activo para Joni
* Cerrar la sesión InPrivate
* Dejar el browser y todas las pestañas abiertas para el siguiente task

## Task 5: Verificar que se emitió la notificación de PIM

> Se confirma que Holly recibió el email de notificación por la aprobación de Alex a la solicitud de Joni, y se revisan los detalles de ambas actividades en el Resource audit.
* [WINDOWS] LON-CL1 -> Edge -> pestaña **Outlook** (abierta desde el lab anterior)
  * [TAB] Inbox -> verificar email de PIM indicando **"Joni Sherman activated the Intune Administrator role assignment"**
  * Abrir el email -> revisar información
* [WINDOWS] Volver a pestaña **Microsoft Entra admin center** (Adatum Corporation - Settings)
* [MENU] Sección Activity -> **Resource audit**
  * [TAB] Resource audit -> seleccionar la **2da actividad más reciente** (requestor = Alex Wilber)
    * [DIALOG] Audit details -> verificar Subject = Joni Sherman, Action = Alex aprobó la solicitud de Joni para Intune Administrator -> **Close**
  * [TAB] Resource audit -> seleccionar la **1ra actividad** (más reciente)
    * [DIALOG] Audit details -> verificar Subject = Joni Sherman, Action = Joni fue agregada al rol Intune Administrator, y el Reason ingresado en Task 3 -> **Close**

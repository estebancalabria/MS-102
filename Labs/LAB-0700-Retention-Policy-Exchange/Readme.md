Lab - Configure In-Place Archiving and Retention Policy (todo con la cuenta de Administrator)

En este ejercicio se habilita el archive mailbox de la propia cuenta de Administrator y se configura una retention policy aplicada únicamente a ese mailbox. Luego se envía un correo de prueba, se elimina y se purga, y se verifica que la retention policy lo conserva pese al borrado.

No se usa ningún usuario de prueba ni se delega acceso a otro mailbox: todos los pasos, incluida la parte de "usuario", se hacen sobre la misma cuenta de Administrator, de principio a fin.

Task 0: Assign eDiscovery Permissions to the Administrator Account

Ser Global Admin no otorga automáticamente permisos de eDiscovery: es un modelo de roles separado dentro de Purview. Sin este paso, el Content Search del Task 5 falla con el error "Missing required permissions to view case".

[WINDOWS] equipo del lab (sesión: Administrator)

- [BROWSER] Microsoft Purview portal
- Ícono Settings (arriba a la derecha)
  - Roles and groups
  - [MENU] Role groups (nav izquierdo)

- Buscar y seleccionar eDiscovery Manager
  - [DIALOG] pane eDiscovery Manager
- Edit
  - [TAB] Manage eDiscovery Manager
  - Choose users → seleccionar Administrator → Select → Next
- (Opcional) Para el subgrupo eDiscovery Administrator, repetir Choose users en el bloque correspondiente dentro del mismo flyout
- Next → Review the role group and finish → Save → Done

- Verificar que Administrator aparece listado bajo eDiscovery Manager

⚠️ El cambio puede tardar unos minutos en propagar. Si el error persiste, cerrar sesión y volver a entrar.

Task 1: Activate In-Place Archiving for the Administrator's Mailbox

Se habilita el archive mailbox de la cuenta de Administrator desde el Exchange admin center.

Habilitar el archive mailbox

[WINDOWS] equipo del lab (sesión: Administrator)

- [MENU] pestaña Microsoft 365 admin center
  - Admin centers → Exchange
- [BROWSER] Exchange admin center

- [MENU] Recipients → Mailboxes
  - [TAB] Manage mailboxes

- Revisar la columna Archive status
  - Administrator debería aparecer con estado Disabled
- Seleccionar Administrator (click en el nombre, no en el checkbox)
  - [DIALOG] pane Administrator

- Tab Others
  - Sección Mailbox archive
  - Verificar que el estado es Disabled
- Seleccionar Manage mailbox archive
  - [DIALOG] Manage mailbox archive

- Activar el toggle Mailbox archive status
  - Estado: Enabled
- Save
- Esperar el mensaje:
  - "Mailbox archiving successfully updated"

- Cerrar el pane con la X

[TAB] Manage mailboxes

- Seleccionar el icono Refresh
- Esperar hasta que el estado de Administrator cambie a:
  - Active
- Si todavía aparece Disabled, esperar unos momentos y volver a refrescar.

Con esto queda habilitado el archive mailbox de la cuenta de Administrator.

Task 2: Create an Email Retention Policy for the Administrator's Mailbox

Se crea la retention policy Administrator mailbox retention, aplicada únicamente al mailbox de Administrator. La policy retiene elementos durante un año desde su creación y posteriormente los elimina automáticamente.

Abrir Data Lifecycle Management

[WINDOWS] equipo del lab (sesión: Administrator)

- [MENU] pestaña Microsoft 365 admin center
  - Admin centers → Microsoft Purview
- [BROWSER] Microsoft Purview portal

- [MENU] Solutions
  - Data Lifecycle Management
- [MENU]
  - Policies
  - Retention policies

Crear la policy

[TAB] Retention policies

- +New retention policy
- [TAB] Name your retention policy
  - Name: Administrator mailbox retention
- Next

- [TAB] Policy Scope
  - Mantener la configuración por defecto
- Next

- [TAB] Choose the type of retention policy to create
  - Static
- Next

Seleccionar la ubicación

- [TAB] Choose where to apply this policy
- En Exchange mailboxes, seleccionar Edit
  - [DIALOG] Exchange mailboxes
  - Seleccionar: Administrator
  - Done
- Verificar que la ubicación Exchange indique:
  - 1 mailbox
- Desactivar todas las demás ubicaciones que estén activadas por defecto:
  - SharePoint classic and communication sites
  - OneDrive accounts
  - Microsoft 365 Group mailboxes & sites
- Verificar:
  - Exchange mailboxes → On, 1 mailbox incluido
  - Todas las demás ubicaciones → Off
- Next

Configurar la retención

[TAB] Decide if you want to retain content, delete it, or both

- Seleccionar: Retain items for a specific period
  - Tipo: Custom
  - Years: 1
  - Months: 0
  - Days: 0
- Start the retention period based on:
  - When items were created
- At the end of the retention period:
  - Delete items automatically

Configuración | Valor
--- | ---
Retain items for a specific period | 1 year
Start the retention period based on | When items were created
At the end of the retention period | Delete items automatically

- Next

Revisar y crear

[TAB] Review and finish

- Revisar configuración
- Submit
  - [DIALOG] You successfully created a retention policy
- Done

[TAB] Retention policies

- Verificar que aparece:
  - Administrator mailbox retention
  - Estado: Enabled

Con esto queda creada la policy para la cuenta de Administrator.

⚠️ Nota de timing importante: una retention policy de Purview puede tardar hasta 24 horas en distribuirse al mailbox antes de que el Managed Folder Assistant la empiece a proteger. Esto no es solo un detalle de cuándo se ven los resultados en el Task 5 — si el correo del Task 3 se envía y se purga (Task 4) antes de que la policy esté realmente activa sobre el mailbox, el correo se pierde de verdad y el Content Search del Task 5 no lo va a encontrar nunca, por más que se espere después.

Opciones para el instructor:
- Crear la policy (este Task 2) con varias horas o un día de anticipación, y recién ahí continuar con los Tasks 3-5 en la clase.
- Forzar el procesamiento con Start-ManagedFolderAssistant -Identity <cuenta de Administrator> desde Exchange Online PowerShell antes de pasar al Task 3, aunque esto no salta la distribución inicial de la policy si todavía no se propagó.

Task 3: Send a Test Email to Yourself

Se envía un correo de prueba desde la propia cuenta de Administrator hacia esa misma cuenta.

[BROWSER] Outlook on the web (sesión de Administrator)

- New email
  - To: Administrator (uno mismo)
  - Subject: Prueba retention policy
- Send

- Esperar unos segundos y hacer Refresh de la bandeja de entrada hasta que el correo llegue.

Task 4: Delete and Purge the Test Email

Se elimina y purga el correo directamente desde la propia bandeja de entrada, sin necesidad de delegación ni de cambiar de cuenta.

[BROWSER] Outlook on the web (sesión de Administrator)

- Ubicar el correo "Prueba retention policy" en Inbox
- Delete
  - Pasa a Deleted Items
- Seleccionar el correo en Deleted Items
- Delete nuevamente (o vaciar la carpeta) para purgarlo

⚠️ Con esto se simula que el usuario intenta eliminar el correo definitivamente.

Task 5: Verify the Email Is Preserved Despite the Deletion

Se verifica, desde Microsoft Purview, que el correo purgado sigue siendo recuperable gracias a la retention policy.

[BROWSER] Microsoft Purview portal

- [MENU] Solutions → eDiscovery
- [MENU] Content Search (nav izquierdo, dentro de eDiscovery)
  - [BROWSER] Content Search (breadcrumb: Cases > Content Search)

Crear la búsqueda

- Create a search
  - [DIALOG] Enter details to get started
  - Search name: Verificacion retention policy
  - Search description: (opcional)
  - Create

[TAB] Query

- Agregar el data source
  - Ícono + (Search and add)
  - Buscar y seleccionar el mailbox de Administrator
  - Save and close
  - Revisar la selección → Save

- Definir la condición (Condition builder)
  - Property: Subject
  - Operator: contains
  - Value: Prueba retention policy

- Run query

Elegir el tipo de resultado

[DIALOG] Choose search results

- Seleccionar Sample (no Statistics) — Statistics solo da un conteo agregado, Sample deja abrir el ítem puntual y ver su contenido
  - Select the number of sample items to generate per location: 1
  - Select the number of locations to get samples from: 10
- Tenant-wide source configuration: dejar todas las casillas sin marcar (no aplica, es un único mailbox propio)
- Run query

- Esperar a que termine de procesar
  - Redirige automáticamente a la pestaña Sample

[TAB] Sample

- Verificar que aparece un ítem con Subject: Prueba retention policy
- Seleccionar el ítem para ver su Source (contenido del correo)
  - Esto confirma que el correo purgado sigue siendo recuperable gracias a la retention policy, aunque ya no esté ni en Inbox ni en Deleted Items.

⚠️ Los resultados de Sample son válidos por 24 horas; si pasó más tiempo, usar Regenerate view.

Resultado final del ejercicio

Al finalizar este ejercicio:
- La cuenta de Administrator tiene habilitado su propio Archive Mailbox.
- La policy Administrator mailbox retention está creada y activa, aplicada solo a ese mailbox.
- Se envió un correo de prueba, se eliminó y se purgó, todo dentro de la misma cuenta de Administrator, sin delegación ni cambio de usuario.
- El content search confirma que el correo purgado sigue siendo recuperable gracias a la retention policy.

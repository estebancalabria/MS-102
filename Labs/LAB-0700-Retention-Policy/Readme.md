# Lab 7 - Configure In-place Archiving and Retention Policies

> En este ejercicio se habilita el archive mailbox de Holly Dickson desde Exchange Online y se configuran dos retention policies en Microsoft Purview.
>
> Primero se crea una policy de prueba para Joni Sherman y Lynne Robbins, con el objetivo de validar el funcionamiento de la retención de correos electrónicos. Luego se deshabilita esa policy de test y se crea la policy oficial de Adatum para todos los mailboxes de Exchange Online.

---

## Task 1: Activate In-Place Archiving for a New User's Mailbox

> Se habilita el archive mailbox de Holly Dickson desde el Exchange admin center. Una vez activado, el Default Retention Policy asignado al mailbox podrá mover automáticamente contenido antiguo desde el mailbox principal hacia el archivo.

### Comportamiento del Default Retention Policy

Una vez habilitado el archive mailbox:

* Los elementos con una antigüedad de **2 años o más** se moverán desde el primary mailbox al archive mailbox.
* Los elementos con una antigüedad de **14 días o más** en la carpeta **Recoverable Items** se moverán hacia la carpeta **Recoverable Items** del archive mailbox.

### Habilitar el archive mailbox

* [WINDOWS] LON-CL1
  * Edge debería continuar abierto con la sesión de **Holly Dickson**
  * [MENU] pestaña **Microsoft 365 admin center**
    * Admin centers → **Exchange**

* [BROWSER] Exchange admin center
  * [MENU] **Recipients** → **Mailboxes**

* [TAB] Manage mailboxes
  * Revisar la columna **Archive status**
    * Algunos usuarios deberían aparecer con estado **Active**
    * Holly Dickson debería aparecer con estado **Disabled**

  * Seleccionar **Holly Dickson** (click en el nombre, no en el checkbox)
    * [DIALOG] pane Holly Dickson
      * Tab **Others**
        * Sección **Mailbox archive**
          * Verificar que el estado es **Disabled**
          * Seleccionar **Manage mailbox archive**

    * [DIALOG] Manage mailbox archive
      * Activar el toggle **Mailbox archive status**
        * Estado: **Enabled**
      * **Save**

    * Esperar el mensaje:

      `Mailbox archiving successfully updated`

    * Cerrar el pane con la **X**

* [TAB] Manage mailboxes
  * Seleccionar el icono **Refresh**
  * Esperar hasta que el estado de Holly cambie a:

    **Active**

  * Si todavía aparece Disabled, esperar unos momentos y volver a refrescar.

* Dejar Edge y todas las pestañas abiertas para el siguiente task.

Con esto queda habilitado el archive mailbox de **Holly Dickson**.

---

## Task 2: Create an Email Retention Policy for Test Users

> Se crea la retention policy **Test user email retention**, aplicada únicamente a los mailboxes de Joni Sherman y Lynne Robbins.
>
> La policy retiene elementos durante un año desde su creación y posteriormente los elimina automáticamente.

### Abrir Data Lifecycle Management

* [WINDOWS] LON-CL1
  * [MENU] pestaña **Microsoft 365 admin center**
    * Admin centers → **Microsoft Purview**

* [BROWSER] Microsoft Purview portal
  * [MENU] **Solutions**
    * **Data Lifecycle Management**

  * [MENU]
    * **Policies**
      * **Retention policies**

### Crear la policy de prueba

* [TAB] Retention policies
  * **+New retention policy**

* [TAB] Name your retention policy
  * Name:

    `Test user email retention`

  * **Next**

* [TAB] Policy Scope
  * Mantener la configuración por defecto
  * **Next**

* [TAB] Choose the type of retention policy to create
  * **Static**
  * **Next**

### Seleccionar las ubicaciones

* [TAB] Choose where to apply this policy
  * En **Exchange mailboxes**, seleccionar **Edit**

* [DIALOG] Exchange mailboxes
  * Seleccionar:
    * **Joni Sherman**
    * **Lynne Robbins**
  * **Done**

* Verificar que la ubicación Exchange indique:

  **2 mailboxes**

* Desactivar todas las demás ubicaciones que estén activadas por defecto:

  * SharePoint classic and communication sites
  * OneDrive accounts
  * Microsoft 365 Group mailboxes & sites

* Verificar:

  * Exchange mailboxes → **On**
  * 2 mailboxes incluidos
  * Todas las demás ubicaciones → **Off**

* **Next**

### Configurar la retención

* [TAB] Decide if you want to retain content, delete it, or both

  * Seleccionar:

    **Retain items for a specific period**

  * Retain items for a specific period:
    * Tipo: **Custom**
    * Years: **1**
    * Months: **0**
    * Days: **0**

  * Start the retention period based on:
    * **When items were created**

  * At the end of the retention period:
    * **Delete items automatically**

| Configuración | Valor |
|---|---|
| Retain items for a specific period | 1 year |
| Start the retention period based on | When items were created |
| At the end of the retention period | Delete items automatically |

* **Next**

### Revisar y crear

* [TAB] Review and finish
  * Revisar configuración
  * **Submit**

* [DIALOG] You successfully created a retention policy
  * **Done**

* [TAB] Retention policies
  * Verificar que aparece:

    `Test user email retention`

* Dejar abierta la página Retention policies para el siguiente task.

Con esto queda creada la policy de prueba para **Joni Sherman** y **Lynne Robbins**.

---

## Task 3: Create an Email Retention Policy for All Users

> Se deshabilita la policy de prueba y se crea la policy organizacional **Adatum email retention**, que conserva todos los correos electrónicos de Exchange Online durante cinco años desde su última modificación y luego los elimina automáticamente.

### Deshabilitar la policy de prueba

* [WINDOWS] LON-CL1
  * Microsoft Purview debería continuar abierto en la página **Retention policies**

* [TAB] Retention policies
  * Seleccionar el checkbox:

    `Test user email retention`

  * **Disable policy**

⚠️ Es posible que la policy tarde algunos minutos en propagarse por el servicio. Si aparece un mensaje **Failed**, esperar unos minutos y volver a intentar.

* Una vez deshabilitada:
  * Seleccionar nuevamente la policy
  * Verificar que aparece la opción:

    **Enable policy**

  * Esto confirma que la policy quedó deshabilitada.

### Crear la policy organizacional

* [TAB] Retention policies
  * **+New retention policy**

* [TAB] Name your retention policy
  * Name:

    `Adatum email retention`

  * **Next**

* [TAB] Policy Scope
  * Mantener configuración por defecto
  * **Next**

* [TAB] Choose the type of retention policy to create
  * **Static**
  * **Next**

### Aplicar a todos los mailboxes

* [TAB] Choose where to apply this policy

  * Verificar:

    * Exchange mailboxes → **On**
    * Scope → **All mailboxes**

  * No modificar el valor **All mailboxes**

* Desactivar todas las demás ubicaciones activadas por defecto:

  * SharePoint classic and communication sites
  * OneDrive accounts
  * Microsoft 365 Group mailboxes & sites
  * Cualquier otra ubicación activada

* Verificar:

  * Exchange mailboxes → **On**
  * All mailboxes
  * Todas las demás ubicaciones → **Off**

* **Next**

### Configurar la retención organizacional

* [TAB] Decide if you want to retain content, delete it, or both

  * Seleccionar:

    **Retain items for a specific period**

  * Configurar:

| Configuración | Valor |
|---|---|
| Retain items for a specific period | 5 years |
| Start the retention period based on | When items were last modified |
| At the end of the retention period | Delete items automatically |

* **Next**

### Revisar y crear

* [TAB] Review and finish
  * Revisar configuración
  * **Submit**

* [DIALOG] You successfully created a retention policy
  * **Done**

* [TAB] Retention policies
  * Verificar que aparece:

    `Adatum email retention`

  * Verificar el estado de ambas policies:

| Policy | Estado |
|----------|----------|
| Test user email retention | Disabled |
| Adatum email retention | Enabled |

* Dejar todas las pestañas abiertas para el siguiente ejercicio.

---

## Resultado final del ejercicio

Al finalizar este ejercicio:

* Holly Dickson tiene habilitado su **Archive Mailbox**.
* La policy **Test user email retention** fue creada para validar la retención en los mailboxes de Joni Sherman y Lynne Robbins.
* La policy de prueba fue deshabilitada.
* Se creó la policy organizacional **Adatum email retention**.
* Todos los Exchange Online mailboxes de Adatum conservan contenido durante **5 años desde la última modificación**.
* Al finalizar el periodo de retención, los elementos se eliminan automáticamente.

**End of Lab 7**

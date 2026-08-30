# [TEÓRICO] Grupos en Microsoft 365 (**Slides:** 30-38)
---

# 1. Introducción a los grupos (Slides 30-31)

Los grupos permiten administrar usuarios de forma colectiva.

Microsoft 365 soporta distintos tipos de grupos según el escenario:

- Colaboración
- Distribución de correo
- Seguridad
- Automatización

---

# 2. Tipos de grupos (Slide 32)

## Mensaje principal

Microsoft soporta:

- Microsoft 365 Groups
- Distribution Groups
- Security Groups
- Mail Enabled Security Groups
- Dynamic Distribution Groups
- Shared Mailboxes


* [BROWSER] https://admin.cloud.microsoft/
     * [MENU] Teams & Groups → Active teams and groups
          * 👁️ -> Microsoft 365 Groups

---

# 3. Microsoft 365 Groups (Slide 32)


Un Microsoft 365 Group proporciona:

- Correo compartido
- Calendario compartido
- SharePoint Site
- Teams
- OneNote

Es el grupo recomendado para colaboración.


* [BROWSER] https://admin.cloud.microsoft/
     * [MENU] Teams & Groups → Active teams and groups
          * [BUTTON] Add a group
               * [OPTION] Microsoft 365
               * 👁️ -> Nombre
               * 👁️ -> Owners
               * 👁️ -> Members

---

# 4. Distribution Groups (Slide 32)

Se utilizan para distribuir correos electrónicos a múltiples usuarios.
No proporcionan herramientas de colaboración.


* [BROWSER] https://admin.exchange.microsoft.com
     * [MENU] Recipients → Groups
          * [BUTTON] Add distribution group
               * 👁️ -> Nombre
               * 👁️ -> Miembros

---

# 5. Security Groups (Slide 32)


Se utilizan para asignar permisos.
No están orientados al correo.


* [BROWSER] https://entra.microsoft.com
     * [MENU] Identity → Groups → All groups
          * [BUTTON] New group
               * [OPTION] Security
                   * 👁️ -> Nombre
                   * 👁️ -> Members

---

# 6. Mail Enabled Security Groups (Slide 32)

Combinan: Seguridad y Distribución de correo

* [BROWSER] https://admin.exchange.microsoft.com
     * [MENU] Recipients → Groups
          * [BUTTON] Add mail-enabled security group
               * 👁️ -> Nombre
               * 👁️ -> Correo
               * 👁️ -> Miembros

---

# 7. Dynamic Distribution Groups (Slides 32-34)

La pertenencia se calcula automáticamente mediante reglas.

* [BROWSER] https://entra.microsoft.com
     * [MENU] Identity → Groups → All groups
          * [BUTTON] New group
               * [OPTION] Security
                   * 👁️ -> Membership type = Dynamic User
                    * 👁️ -> Dynamic query

---

# 8. Shared Mailboxes (Slide 32)

Permiten que varias personas compartan el mismo buzón.


* [BROWSER] https://admin.exchange.microsoft.com
     * [MENU] Recipients → Shared
          * 👁️ -> Shared Mailboxes
          * [BUTTON] Add shared mailbox

---

# 9. Administrar grupos (Slide 33)

Buenas prácticas:

- Mantener convenciones de nombres.
- Tener al menos dos owners.
- Definir procesos de mantenimiento.
- Utilizar grupos para administrar permisos.

* [BROWSER] https://admin.cloud.microsoft/
     * [MENU] Teams & Groups → Active teams and groups
          * [ITEM] Seleccionar grupo
               * 👁️ -> Owners
               * 👁️ -> Members

---

# 10. Naming Policy (Slide 35)

Microsoft permite controlar:  Prefijos, Sufijos, Palabras bloqueadas

* [BROWSER] https://entra.microsoft.com
     * [SEARCH] Naming policy
          * 👁️ -> Prefixes
          * 👁️ -> Suffixes
          * 👁️ -> Blocked words

---

# 11. Grupos en Exchange y SharePoint (Slide 36)

Exchange y SharePoint utilizan grupos para administrar: Corre, Permisos y Colaboración

* [BROWSER] https://admin.exchange.microsoft.com
     * [MENU] Recipients → Groups
          * 👁️ -> Tipos de grupos disponibles
* [BROWSER] https://xxxx-admin.sharepoint.com
     * [MENU] Active sites
          * [ITEM] Seleccionar sitio
               * 👁️ -> Permissions
               * 👁️ -> Site members


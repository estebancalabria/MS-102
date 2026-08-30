# Prácticas de administración de datos en Microsoft 365 (**Slides:** 12-19)
---

# 1. Buzones de archivo en Microsoft 365 / Habilitación de Archive Mailboxes  (Slides 14-15)

Los Archive Mailboxes permiten ampliar la capacidad de almacenamiento del correo y mover automáticamente mensajes antiguos fuera del buzón principal. 

* [BROWSER] https://admin.exchange.microsoft.com
    * [MENU] Recipients → Mailboxes
        * [LINK] Buzón de usuario
           * [TAB] Others
              * 👁️ ->Mailbox archive -> Estado Enabled / Disabled

---

# 2. Recuperación y retención de correos en Exchange Online (Slide 16)

Exchange Online permite recuperar mensajes eliminados dentro del período de retención configurado y aplicar configuraciones de conservación para cumplir requisitos de negocio y cumplimiento.

* [BROWSER] Outlook on the Web
    * [MENU] Deleted Items
        * 👁️ -> Recover deleted items
        * 👁️ -> Restorable messages

* [BROWSER] https://admin.exchange.microsoft.com
    * [MENU] Recipients → Mailboxes
        * [LINK] User mailbox
            * [TAB] Mailbox
                * 👁️ -> Retention settings
                * 👁️ -> Deleted item retention

---

# 3.  Restore Deleted Data in SharePoint Online (Slide 17)

SharePoint Online uses a two-stage recycle bin to recover deleted content for up to 93 days.

* [BROWSER] https://<tenant>.sharepoint.com
    * [SITE] Team Site
        * [MENU] Recycle Bin
            * 👁️ -> Deleted files
            * 👁️ -> Restore
            * 👁️ -> First-stage Recycle Bin

* [BROWSER] https://<tenant>-admin.sharepoint.com
    * [MENU] Active Sites
        * [LINK] Site
            * 👁️ -> Site Collection Recycle Bin
            * 👁️ -> Second-stage recovery

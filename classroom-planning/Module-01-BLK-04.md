# [TEÓRICO] Gestión de usuarios, licencias e invitados
**Slides:** 17-29
**Duración:** 60-75 minutos

---

# 1. Modelos de identidad (Slides 17-19)

## Mensaje principal

Microsoft soporta tres modelos de identidad:

- Cloud Identity : El usuario existe únicamente en Microsoft Entra ID, No existe Active Directory local.
- Synchronized Identity: El usuario existe en Active Directory local. Se sincroniza mediante Entra Connect.
- Federated Identity: El usuario existe en Active Directory local. La autenticación es realizada por un proveedor federado.

## Demo

* [BROWSER] https://entra.microsoft.com

     * [MENU] Identity → Users → All users
          * 👁️ -> Usuarios del tenant

     * [SEARCH] Entra Connect
          * 👁️ -> Mostrar si existe sincronización híbrida

---

# 2. Crear usuarios (Slide 20)

## Mensaje principal

Microsoft permite crear usuarios mediante:
- Microsoft 365 Admin Center
- Importación masiva
- PowerShell
- Sincronización de directorio

## Demo

* [BROWSER] https://admin.cloud.microsoft/

     * [MENU] Users → Active users

          * [BUTTON] Add a user

               * 👁️ -> Nombre
               * 👁️ -> Username
               * 👁️ -> Password
               * 👁️ -> Licencias
               * 👁️ -> Roles

---

# 3. Administrar usuarios (Slide 21)

## Mensaje principal

Una vez creado el usuario pueden administrarse:
- Estado de inicio de sesión
- Ubicación
- Roles
- Licencias

## Demo

* [BROWSER] https://admin.cloud.microsoft/

     * [MENU] Users → Active users

          * [ITEM] Seleccionar usuario

               * [TAB] Account
                    * 👁️ -> Block sign-in

               * [TAB] Roles
                    * 👁️ -> Roles administrativos

               * [TAB] Licenses and apps
                    * 👁️ -> Licencias asignadas

---

# 4. Licencias de usuario (Slide 22)

## Mensaje principal

Las licencias habilitan los servicios que un usuario puede utilizar.

## Demo

* [BROWSER] https://admin.cloud.microsoft/

     * [MENU] Users → Active users

          * [ITEM] Seleccionar usuario

               * [TAB] Licenses and apps

                    * 👁️ -> Microsoft 365 E5
                    * 👁️ -> Servicios habilitados
                    * 👁️ -> Servicios deshabilitados

---

# 5. Recuperar usuarios eliminados (Slide 23)

## Mensaje principal

Los usuarios eliminados pueden recuperarse durante el período de retención.

## Demo

* [BROWSER] https://admin.cloud.microsoft/

     * [MENU] Users → Deleted users

          * 👁️ -> Usuarios eliminados

          * [BUTTON] Restore user

---

# 6. Operaciones masivas (Slide 24)

## Mensaje principal

Microsoft permite crear, eliminar y restaurar usuarios mediante archivos CSV.

## Demo

* [BROWSER] https://entra.microsoft.com

     * [MENU] Identity → Users → All users

          * [BUTTON] Bulk operations

               * 👁️ -> Bulk create
               * 👁️ -> Bulk delete
               * 👁️ -> Bulk restore

---

# 7. Guest Users (Slides 25-26)

## Mensaje principal

Los usuarios externos pueden colaborar mediante Microsoft Entra B2B.

- Mantienen sus credenciales externas.
- Aparecen como Guest dentro del tenant.

## Demo

* [BROWSER] https://entra.microsoft.com

     * [MENU] Identity → Users → All users

          * [BUTTON] New user

               * [OPTION] Invite external user

                    * 👁️ -> Nombre
                    * 👁️ -> Email
                    * 👁️ -> Tipo Guest

* [BROWSER] https://xxxx-admin.sharepoint.com

     * [MENU] Policies → Sharing

          * 👁️ -> Configuración para invitados

---

# 8. Mail Contacts (Slide 27)

## Mensaje principal

Un Mail Contact representa una persona externa dentro de la libreta global de direcciones.

## Demo

* [BROWSER] https://admin.exchange.microsoft.com

     * [MENU] Recipients → Contacts

          * [BUTTON] Add mail contact

               * 👁️ -> Nombre
               * 👁️ -> Email externo



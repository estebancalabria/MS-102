# [TEÓRICO] Permisos, roles y grupos de roles
**Slides:** 3-16  
**Duración:** 70-90 minutos

---

# 1. Modelo de permisos de Microsoft 365 (Slides 4-6)

## Mensaje principal

Microsoft 365 utiliza un modelo basado en:
* Roles : Los roles definen qué puede hacer un administrador.
* Scopes : Los scopes definen sobre qué objetos puede actuar.
* Assignments : Los assignments conectan usuarios con roles.

## Demo

* [BROWSER] https://admin.cloud.microsoft/
    * [MENU] Users → Active users
        * [ITEM] Seleccionar usuario
        * [TAB] Roles
            * 👁️ -> Roles administrativos asignados

* [BROWSER] https://entra.microsoft.com
    * [MENU] Identity → Roles & administrators
        * 👁️ -> Roles disponibles
        * 👁️ -> Administradores asignados

---

# 2. Roles administrativos (Slides 7-9)

## Mensaje principal

No todos los administradores necesitan ser Global Administrator. Microsoft recomienda asignar únicamente los permisos necesarios para cada tarea.

## Demo

* [BROWSER] https://admin.cloud.microsoft/
    * [MENU] Users → Active users
        * [ITEM] Seleccionar usuario
        * [TAB] Manage roles

            * 👁️ -> Global Administrator
            * 👁️ -> Exchange Administrator
            * 👁️ -> License Administrator
            * 👁️ -> Groups Administrator
            * 👁️ -> Helpdesk Administrator

---

# 3. Buenas prácticas para la asignación de roles (Slide 8)

## Mensaje principal

Microsoft recomienda:

* Menor privilegio posible
* MFA para administradores
* Revisar permisos periódicamente
* Limitar la cantidad de Global Administrators
* Utilizar PIM cuando sea posible

## Demo

* [BROWSER] https://admin.cloud.microsoft/
    * [MENU] Users → Active users
        * [ITEM] Seleccionar administrador
            * 👁️ -> Roles asignados

* [BROWSER] https://entra.microsoft.com
    * [MENU] Protection → Authentication methods
        * 👁️ -> Métodos de autenticación configurados

---

# 4. Delegación administrativa a partners (Slide 10)

## Mensaje principal

Una organización puede delegar parte de la administración a un Partner Microsoft. Los partners pueden recibir permisos administrativos limitados o completos.

## Demo

* [BROWSER] https://admin.cloud.microsoft/
    * [MENU] Settings → Partner relationships
        * 👁️ -> Partners configurados
        * 👁️ -> Permisos delegados

---

# 5. Role Groups (Slide 11)

## Mensaje principal

Los Role Groups permiten asignar permisos a grupos en lugar de hacerlo usuario por usuario. Esto simplifica la administración.

## Demo

* [BROWSER] https://admin.exchange.microsoft.com
    * [MENU] Roles → Admin roles
        * 👁️ -> Role Groups disponibles

* [ITEM] Organization Management
    * 👁️ -> Miembros
    * 👁️ -> Roles incluidos

---

# 6. Administrative Units (Slide 12)

## Mensaje principal

Las Administrative Units permiten delegar administración sobre una parte específica de la organización. Cada unidad puede tener sus propios administradores.

## Demo

* [BROWSER] https://entra.microsoft.com
    * [MENU] Identity → Administrative units
        * 👁️ -> Administrative Units existentes
        * [BUTTON] Add administrative unit

---

# 7. Permisos de SharePoint y prevención de oversharing (Slide 13)

## Mensaje principal

Copilot y los usuarios pueden acceder a toda la información para la que tengan permisos. Por eso es importante revisar el modelo de permisos y compartición.

## Demo

* [BROWSER] https://admin.cloud.microsoft/
    * [MENU] Show all
    * [MENU] Admin centers → SharePoint

* (NEW WINDOW)

* [BROWSER] https://xxxx-admin.sharepoint.com
    * [MENU] Policies → Sharing
        * 👁️ -> Nivel de compartición externa

    * [MENU] Active Sites
        * [ITEM] Seleccionar sitio
            * [TAB] Permissions
                * 👁️ -> Usuarios con acceso

## Explicación

* Un usuario solamente puede ver contenido para el que posee permisos.
* Los permisos excesivos generan riesgo de oversharing.

---

# 8. Privileged Identity Management (Slide 14)

## Mensaje principal

PIM permite otorgar privilegios temporales.

Los administradores elevan permisos únicamente cuando los necesitan.

Esto reduce la superficie de ataque.

## Demo

* [BROWSER] https://entra.microsoft.com

    * [MENU] Identity Governance → Privileged Identity Management

        * [MENU] Microsoft Entra Roles

            * 👁️ -> Eligible Assignments

            * 👁️ -> Active Assignments

            * 👁️ -> Activación Just-In-Time

## Explicación

* Un usuario puede ser elegible para un rol sin tenerlo activo permanentemente.
* El acceso se activa durante un período determinado y luego se revoca automáticamente.


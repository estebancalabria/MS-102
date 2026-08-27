# [TEÓRICO] Grupos en Microsoft 365
**Slides:** 30-38
**Duración:** 45-60 minutos

---

# 1. Introducción a los grupos (Slides 30-31)

## Mensaje principal

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

## Demo

* [BROWSER] https://admin.cloud.microsoft/

     * [MENU] Teams & Groups → Active teams and groups

          * 👁️ -> Microsoft 365 Groups

---

# 3. Microsoft 365 Groups (Slide 32)

## Mensaje principal

Un Microsoft 365 Group proporciona:

- Correo compartido
- Calendario compartido
- SharePoint Site
- Teams
- OneNote

Es el grupo recomendado para colaboración.

## Demo

* [BROWSER] https://admin.cloud.microsoft/

     * [MENU] Teams & Groups → Active teams and groups

          * [BUTTON] Add a group

               * [OPTION] Microsoft 365

               * 👁️ -> Nombre
               * 👁️ -> Owners
               * 👁️ -> Members

---

# 4. Distribution Groups (Slide 32)

## Mensaje principal

Se utilizan para distribuir correos electrónicos a múltiples usuarios.

No proporcionan herramientas de colaboración.

## Demo

* [BROWSER] https://admin.exchange.microsoft.com

     * [MENU] Recipients → Groups

          * [BUTTON] Add distribution group

               * 👁️ -> Nombre
               * 👁️ -> Miembros

---

# 5. Security Groups (Slide 32)

## Mensaje principal

Se utilizan para asignar permisos.

No están orientados al correo.

## Demo

* [BROWSER] https://entra.microsoft.com

     * [MENU] Identity → Groups → All groups

          * [BUTTON] New group

               * [OPTION] Security

               * 👁️ -> Nombre
               * 👁️ -> Members

---

# 6. Mail Enabled Security Groups (Slide 32)

## Mensaje principal

Combinan:

- Seguridad
- Distribución de correo

Permiten asignar permisos y recibir correos.

## Demo

* [BROWSER] https://admin.exchange.microsoft.com

     * [MENU] Recipients → Groups

          * [BUTTON] Add mail-enabled security group

               * 👁️ -> Nombre
               * 👁️ -> Correo
               * 👁️ -> Miembros

---

# 7. Dynamic Distribution Groups (Slides 32-34)

## Mensaje principal

La pertenencia se calcula automáticamente mediante reglas.

Ejemplo:

- Todos los usuarios del departamento Ventas.
- Todos los usuarios de Argentina.

## Demo

* [BROWSER] https://entra.microsoft.com

     * [MENU] Identity → Groups → All groups

          * [BUTTON] New group

               * [OPTION] Security

                    * 👁️ -> Membership type = Dynamic User

                    * 👁️ -> Dynamic query

---

# 8. Shared Mailboxes (Slide 32)

## Mensaje principal

Permiten que varias personas compartan el mismo buzón.

Ejemplos:

- soporte@empresa.com
- ventas@empresa.com

## Demo

* [BROWSER] https://admin.exchange.microsoft.com

     * [MENU] Recipients → Shared

          * 👁️ -> Shared Mailboxes

          * [BUTTON] Add shared mailbox

---

# 9. Administrar grupos (Slide 33)

## Mensaje principal

Buenas prácticas:

- Mantener convenciones de nombres.
- Tener al menos dos owners.
- Definir procesos de mantenimiento.
- Utilizar grupos para administrar permisos.

## Demo

* [BROWSER] https://admin.cloud.microsoft/

     * [MENU] Teams & Groups → Active teams and groups

          * [ITEM] Seleccionar grupo

               * 👁️ -> Owners
               * 👁️ -> Members

---

# 10. Naming Policy (Slide 35)

## Mensaje principal

Microsoft permite controlar:

- Prefijos
- Sufijos
- Palabras bloqueadas

## Demo

* [BROWSER] https://entra.microsoft.com

     * [SEARCH] Naming policy

          * 👁️ -> Prefixes
          * 👁️ -> Suffixes
          * 👁️ -> Blocked words

---

# 11. Grupos en Exchange y SharePoint (Slide 36)

## Mensaje principal

Exchange y SharePoint utilizan grupos para administrar:

- Correo
- Permisos
- Colaboración

## Demo

* [BROWSER] https://admin.exchange.microsoft.com

     * [MENU] Recipients → Groups

          * 👁️ -> Tipos de grupos disponibles

* [BROWSER] https://xxxx-admin.sharepoint.com

     * [MENU] Active sites

          * [ITEM] Seleccionar sitio

               * 👁️ -> Permissions
               * 👁️ -> Site members

---

# 12. Knowledge Check (Slide 37)

## Kahoot

- ¿Cuál es el grupo recomendado para colaboración?
- ¿Qué grupo usarías para enviar correos masivos?
- ¿Qué grupo usarías para asignar permisos?
- ¿Qué es un grupo dinámico?
- ¿Qué es un Shared Mailbox?
- ¿Para qué sirve una Naming Policy?

---

# 13. Resumen (Slide 38)

## Mensaje principal

En este módulo vimos:

- Microsoft 365 Groups
- Distribution Groups
- Security Groups
- Mail Enabled Security Groups
- Dynamic Groups
- Shared Mailboxes
- Naming Policy
- Integración con Exchange y SharePoint

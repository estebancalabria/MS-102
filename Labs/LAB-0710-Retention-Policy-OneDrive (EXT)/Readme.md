# Lab - Configure OneDrive Retention Policy and Verify Content Preservation (todo con la cuenta de Administrator)

En este ejercicio se crea una retention policy aplicada únicamente al OneDrive de la cuenta Administrator. Luego se carga un archivo de prueba, se elimina de OneDrive y se verifica mediante Content Search que sigue siendo recuperable gracias a la retention policy.

No se usa ningún usuario de prueba ni se delega acceso a otro OneDrive: todos los pasos se realizan con la misma cuenta Administrator.

---

# Task 0: Assign eDiscovery Permissions to the Administrator Account

Ser Global Admin no otorga automáticamente permisos de eDiscovery. Sin este paso, el Content Search del Task 4 puede fallar con errores de permisos.

[WINDOWS] equipo del lab (sesión: Administrator)

- [BROWSER] Microsoft Purview portal
- Settings (esquina superior derecha)
  - Roles and groups
  - [MENU] Role groups
- Buscar y seleccionar **eDiscovery Manager**
- Edit
  - [TAB] Manage eDiscovery Manager
  - Choose users → Administrator → Select → Next
- Next → Review the role group and finish → Save → Done
- Verificar que Administrator aparece listado en eDiscovery Manager

⚠️ La propagación de permisos puede tardar algunos minutos.

---

# Task 1: Create a OneDrive Retention Policy

Se crea una policy denominada **Administrator OneDrive retention**, aplicada únicamente al OneDrive de la cuenta Administrator.

## Abrir Data Lifecycle Management

[WINDOWS] equipo del lab (sesión: Administrator)

- [MENU] Microsoft 365 admin center
  - Admin centers → Microsoft Purview
- [BROWSER] Microsoft Purview portal
- [MENU] Solutions
  - Data Lifecycle Management
- [MENU]
  - Policies
  - Retention policies

## Crear la policy

[TAB] Retention policies

- + New retention policy

### [TAB] Name your retention policy

- Name: **Administrator OneDrive retention**
- Next

### [TAB] Policy Scope

- Mantener configuración por defecto
- Next

### [TAB] Choose the type of retention policy to create

- Static
- Next

## Seleccionar ubicación

### [TAB] Choose where to apply this policy

- Desactivar Exchange mailboxes
- Desactivar Microsoft 365 Group mailboxes & sites
- Desactivar SharePoint classic and communication sites

### OneDrive accounts

- Edit
  - [DIALOG] OneDrive accounts
  - Seleccionar Administrator
  - Done

Verificar:

- OneDrive accounts → On, 1 account incluido
- Todas las demás ubicaciones → Off

- Next

## Configurar la retención

### [TAB] Decide if you want to retain content, delete it, or both

- Retain items for a specific period
  - Type: Custom
  - Years: 1
  - Months: 0
  - Days: 0

- Start the retention period based on:
  - When items were created

- At the end of the retention period:
  - Delete items automatically

### Configuración

| Configuración | Valor |
|--------------|--------|
| Retain items for a specific period | 1 year |
| Start the retention period based on | When items were created |
| At the end of the retention period | Delete items automatically |

- Next

## Revisar y crear

### [TAB] Review and finish

- Revisar configuración
- Submit

  - [DIALOG] You successfully created a retention policy

- Done

### [TAB] Retention policies

Verificar:

- Administrator OneDrive retention
- Status: Enabled

Con esto queda creada la retention policy para el OneDrive de Administrator.

---

⚠️ Nota importante

Las retention policies pueden tardar hasta 24 horas en distribuirse completamente a OneDrive.

Si se elimina el archivo antes de que la policy se aplique realmente, el contenido podría perderse definitivamente y no aparecer en el Content Search.

Opciones para el instructor:

- Crear la policy varias horas o un día antes del laboratorio.
- Verificar previamente que la policy ya figura como activa en el entorno.

---

# Task 2: Upload a Test File to OneDrive

Se crea un archivo de prueba en el OneDrive personal de Administrator.

[BROWSER] OneDrive (sesión: Administrator)

- New
  - Word document

- Cambiar el nombre a:

  - **Prueba Retention OneDrive.docx**

- Escribir el siguiente contenido:

  - Este archivo se utilizará para validar una retention policy de OneDrive.

- Guardar el documento

- Esperar unos segundos hasta confirmar que el archivo aparece en My files.

---

# Task 3: Delete the Test File

Se elimina el archivo desde OneDrive.

[BROWSER] OneDrive (sesión: Administrator)

- Localizar:

  - Prueba Retention OneDrive.docx

- Seleccionar el archivo
- Delete

  - El archivo se mueve a Recycle Bin

- [MENU] Recycle Bin

- Seleccionar el archivo

- Delete permanently

⚠️ Con esto se simula que el usuario intenta eliminar permanentemente el documento.

---

# Task 4: Verify the File Is Preserved Despite the Deletion

Se utiliza Microsoft Purview Content Search para comprobar que el archivo sigue siendo recuperable gracias a la retention policy.

[BROWSER] Microsoft Purview portal

- [MENU] Solutions → eDiscovery
- [MENU] Content Search

## Crear la búsqueda

- Create a search

### [DIALOG] Enter details to get started

- Search name:
  - Verificacion OneDrive retention

- Create

---

## [TAB] Query

### Agregar Data Source

- Search and add
- Buscar y seleccionar:
  - OneDrive de Administrator

- Save and close
- Save

### Condition builder

- Property:
  - File name

- Operator:
  - contains

- Value:
  - Prueba Retention OneDrive

- Run query

---

## Elegir resultados

### [DIALOG] Choose search results

- Sample

- Select the number of sample items to generate per location:
  - 1

- Select the number of locations to get samples from:
  - 10

- Tenant-wide source configuration:
  - dejar todas las opciones sin marcar

- Run query

- Esperar a que finalice el procesamiento

---

## [TAB] Sample

Verificar que aparece un resultado similar a:

- Prueba Retention OneDrive.docx

Seleccionar el resultado para revisar el contenido.

Esto confirma que el archivo eliminado permanentemente sigue siendo recuperable gracias a la retention policy aplicada al OneDrive.

⚠️ Si no aparecen resultados y la eliminación fue reciente, verificar primero que la retention policy ya había terminado de propagarse antes de borrar el archivo.

---

# Resultado final del ejercicio

Al finalizar este ejercicio:

1. La cuenta Administrator dispone de una retention policy aplicada exclusivamente a su OneDrive.
2. Se creó y almacenó un archivo de prueba en OneDrive.
3. El archivo fue eliminado y purgado desde la papelera de reciclaje.
4. El Content Search de Microsoft Purview confirma que el archivo sigue siendo recuperable gracias a la retention policy.
5. Se demuestra cómo Microsoft Purview protege contenido de OneDrive incluso después de una eliminación permanente por parte del usuario.

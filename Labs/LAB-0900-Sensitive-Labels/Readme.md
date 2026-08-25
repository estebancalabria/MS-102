# Learning Path 9 - Lab 9 - Exercise 1 - Implement Sensitivity Labels with Microsoft Purview Information Protection

> Como parte del piloto de Microsoft 365 en Adatum, se implementarán Sensitivity Labels mediante Microsoft Purview Information Protection.
>
> En este laboratorio se instala el cliente de Microsoft Purview Information Protection, se habilita el soporte para etiquetas de sensibilidad en SharePoint y OneDrive, se crea una nueva Sensitivity Label con cifrado, marcas visuales y autoetiquetado, se publica una Label Policy y finalmente se valida una etiqueta previamente creada mediante la protección y compartición controlada de documentos.
>
> ⚠️ IMPORTANTE: Las nuevas Sensitivity Labels y Label Policies pueden tardar hasta 24 horas en propagarse por Microsoft 365. Debido a ello, la etiqueta creada en este laboratorio no podrá probarse inmediatamente. En su lugar se utilizará una etiqueta preexistente llamada **Project - Falcon**, que posee una configuración equivalente.

---

# Task 1: Install the Microsoft Purview Information Protection Client

> Se instala el cliente Microsoft Purview Information Protection en LON-CL1 para habilitar funcionalidades de clasificación y protección avanzadas en aplicaciones Microsoft Office.

### Descargar el instalador

* [WINDOWS] Switch a **LON-CL1**
  * Verificar:
    * Sesión iniciada como **adatum\administrator**
    * Edge abierto
    * Holly Dickson autenticada en Microsoft 365

* [BROWSER] Nueva pestaña

  * Navegar a:

    [Microsoft Purview Information Protection Client](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

  * **Download**

* [DIALOG] Choose the download you want

  * Seleccionar:

    ```text
    PurviewInfoProtection.exe
    ```

  * **Download**

### Instalar el cliente

* [BROWSER] Downloads

  * Esperar que finalice la descarga

  * Seleccionar:

    **Open file**

* [DIALOG] Microsoft Azure Information Protection Setup

  * Seleccionar:

    * ✅ I acknowledge that the AIP Add-in for Office will be uninstalled (required)
    * ❌ Help improve Microsoft Purview Information Protection by sending usage statistics to Microsoft

  * **I agree**

* Esperar la finalización de la instalación.

* **Close**

Con esto queda instalado el cliente **Microsoft Purview Information Protection** en LON-CL1.

---

# Task 2: Enable Sensitivity Labels for Files in SharePoint and OneDrive

> Se habilita el procesamiento de archivos protegidos por Sensitivity Labels dentro de SharePoint Online y OneDrive.
>
> Esto permite funcionalidades como:
>
> * Coauthoring
> * eDiscovery
> * Data Loss Prevention
> * Search
> * Colaboración sobre archivos cifrados
>
> Además se habilita el soporte para archivos PDF protegidos.

⚠️ Los cambios de configuración de SharePoint y OneDrive pueden tardar aproximadamente 15 minutos en aplicarse.

---

## Habilitar Sensitivity Labels para Office Online

* [WINDOWS] LON-CL1

* [MENU] Microsoft 365 admin center

  * Si es necesario:

    **Show all**

  * Admin centers
    * **Microsoft Purview**

* [BROWSER] Microsoft Purview

* [MENU]

  * Solutions
    * Information Protection
      * Sensitivity labels

* [TAB] Sensitivity labels

Aparecerá el mensaje:

```text
Your organization has not turned on the ability to process content in Office online files ...
```

* Seleccionar:

  **Turn on now**

⚠️ El cambio se ejecuta inmediatamente.

---

## Habilitar protección PDF

* [MENU]

  * Information Protection
    * Policies
      * Auto-labeling policies

* [TAB] Auto-labeling

Localizar el banner:

```text
Protect PDFs with Auto-labeling
```

* Seleccionar el banner.

* [DIALOG]

  * **Confirm**

⚠️ La protección de PDF queda habilitada para SharePoint y OneDrive.

* Dejar todas las pestañas abiertas.

Con esto SharePoint y OneDrive ya pueden procesar archivos Office y PDF protegidos mediante Sensitivity Labels.

---

# Task 3: Create a Sensitivity Label

> Se crea una nueva Sensitivity Label denominada **PII**, destinada a identificar información sensible como números de seguridad social o números ABA bancarios.
>
> La etiqueta incluirá:
>
> * Marcado visual (header, footer y watermark)
> * Auto-labeling
> * Clasificación predeterminada
> * Publicación para todos los usuarios del tenant

---

## Crear la etiqueta

* [WINDOWS] LON-CL1

* [MENU]

  * Microsoft Purview
    * Solutions
      * Information Protection
        * Sensitivity labels

* [TAB] Sensitivity labels

  * **+Create a label**

---

## Datos básicos

* [TAB] Provide basic details for this label

| Campo | Valor |
|---------|---------|
| Name | PII |
| Display name | PII |
| Description for users | Documents, files, and emails with PII |
| Description for admins | Documents, files, and emails with PII |
| Label color | Cualquiera |

* **Next**

---

## Definir alcance

* [TAB] Define the scope for this label

Verificar seleccionados:

* Files & other data assets
* Emails
* Meetings

* **Next**

---

## Configurar protección

* [TAB] Choose protection settings

Seleccionar:

* ✅ Control access
* ✅ Apply content marking

* **Next**

---

## Configuración de Access Control

> En este laboratorio no se habilitará cifrado. La estrategia utilizada es crear inicialmente etiquetas sin cifrado y habilitarlo posteriormente.

* [TAB] Access control

Seleccionar:

```text
Remove access control settings if already applied to items
```

* **Next**

---

## Configurar marcas visuales

* [TAB] Content marking

* Activar:

  ```text
  Content marking = On
  ```

Seleccionar:

* Add a watermark
* Add a header
* Add a footer

---

### Watermark

```text
Sensitive - Do Not Share
```

| Parámetro | Valor |
|------------|---------|
| Font size | 25 |
| Font color | Blue |
| Layout | Diagonal |

---

### Header

```text
Sensitive - Do Not Share
```

| Parámetro | Valor |
|------------|---------|
| Font size | 25 |
| Font color | Red |
| Alignment | Center |

---

### Footer

```text
Sensitive - Do Not Share
```

| Parámetro | Valor |
|------------|---------|
| Font size | 25 |
| Font color | Red |
| Alignment | Center |

* **Next**

---

## Configurar Auto-labeling

* [TAB] Auto-labeling for files and emails

Activar:

```text
Auto-labeling = On
```

### Agregar condición

* +Add condition
  * Content contains

* Add
  * Sensitive info types

---

### Provocar error intencional

* [DIALOG] Sensitive info types

Seleccionar TODOS los tipos de información sensible.

* **Add**

Configurar:

| Campo | Valor |
|---------|---------|
| When content matches these conditions | Automatically apply the label |
| Display this message | Sensitive content has been detected and will be encrypted |

* **Next**
* **Create label**

---

## Analizar el error

Aparecerá:

```text
Client Error
```

Indicando:

```text
Generated rule blob exceeds maximum size
```

⚠️ Este error se provoca intencionalmente para mostrar un límite importante de Microsoft Purview.

La selección masiva de Sensitive Info Types supera el límite interno de:

```text
49152
```

---

## Corregir el error

* Seleccionar:

  **OK**

* Edit en la sección Auto-labeling

### Eliminar condición existente

* Eliminar la condición:

  ```text
  Content contains
  ```

### Crear una nueva condición

* +Add condition
  * Content contains

* Add
  * Sensitive info types

Seleccionar únicamente:

* ABA routing number
* U.S. Social Security Number (SSN)

* Add

* **Next**

---

## Finalizar creación

* Review your settings and finish

* **Create label**

* [DIALOG]

  * Seleccionar:

    ```text
    Don't create a policy yet
    ```

* **Done**

---

# Publicar la etiqueta

* [TAB] Sensitivity labels

* Seleccionar:

  ```text
  PII
  ```

* **Publish label**

---

## Create Policy

### Choose sensitivity labels to publish

* Seleccionar:

  ```text
  PII
  ```

* **Next**

### Assign admin units

* **Next**

### Publish to users and groups

Mantener:

```text
All users and groups
```

* **Next**

---

## Policy Settings

Seleccionar:

```text
Users must provide a justification to remove a label or lower its classification
```

* **Next**

---

## Configurar etiquetas predeterminadas

Seleccionar **PII** en todos los apartados:

* Documents
* Emails
* Meetings
* Fabric and Power BI

* **Next**

---

## Nombre de la política

Name:

```text
PII Policy
```

Description:

```text
The purpose of this policy is to detect sensitive information such as ABA bank routing numbers and US social security numbers in emails and documents, and to encrypt this information when it's discovered. The user must provide an explanation for removing the classification label.
```

* **Next**

---

## Crear policy

* Review and finish

* **Submit**

* [DIALOG]

  ```text
  New policy created
  ```

* **Done**

Con esto quedan creadas la etiqueta **PII** y la policy **PII Policy**.

---

# Task 4: Assign a Pre-existing Sensitivity Label to a Document

> Como las nuevas etiquetas pueden tardar hasta 24 horas en propagarse, se utilizará la etiqueta existente **Project - Falcon** para validar el comportamiento de Microsoft Purview Information Protection.

---

## Revisar la etiqueta Project - Falcon

* [MENU]

  * Information Protection
    * Sensitivity labels

* [TAB] Sensitivity labels

Seleccionar:

```text
Project - Falcon
```

Revisar la configuración.

Cerrar el panel.

---

## Crear documento de prueba

* [MENU]

  * Search | M365 Copilot
    * Apps

* Abrir:

  **Word**

* [TAB] Word

  * Create blank document

* Escribir:

```text
Testing a sensitivity label on a document with personally identifiable information (PII); in this case, a U.S Social Security Number: 111-11-1111.
```

---

## Aplicar la etiqueta

* Ribbon

  * Sensitivity

Seleccionar:

```text
Project - Falcon
```

Verificar que aparece el watermark:

```text
CONFIDENTIAL - ProjectFalcon
```

---

## Validar Reading View

* View
  * Reading View

Verificar que el watermark aparece diagonalmente atravesando la página.

Volver a:

* Edit Document
  * Edit

---

## Validar justificación obligatoria

* Sensitivity

Seleccionar nuevamente:

```text
Project - Falcon
```

* [DIALOG] Justification Required

Seleccionar:

```text
Other (explain)
```

Ingresar:

```text
Testing what happens when a label is removed from a document
```

* **Change**

Verificar que desaparece el watermark.

---

## Reaplicar la etiqueta

* Sensitivity

  * Project - Falcon

Verificar que vuelve a aparecer el watermark.

---

## Guardar documento

Cambiar nombre a:

```text
ProtectedDocument1
```

Verificar ubicación:

```text
Holly Dickson > Documents
```

Dejar el documento abierto.

Con esto queda creado el documento protegido mediante la etiqueta **Project - Falcon**.

---

# Task 5: Protect a Document Using Microsoft Purview Information Protection

> Se compartirá el documento con Joni Sherman utilizando primero permisos de solo lectura y posteriormente permisos de edición.
>
> Además se validará que otros usuarios no autorizados no pueden acceder al contenido.

---

## Compartir documento con permiso View Only

* [WINDOWS] LON-CL1

* Abrir Outlook Web

* New mail

| Campo | Valor |
|---------|---------|
| To | Joni Sherman |
| CC | Email personal del alumno |
| Subject | Protected Document Test - View only permission |

Mensaje:

```text
Open the protected document attached to this email and try to change it.
```

---

### Compartir desde Word

* Volver a **ProtectedDocument1**

* Share
  * Share

* Link settings

Seleccionar:

```text
People you choose
```

Cambiar:

```text
Can edit → Can view
```

* Apply

Agregar:

```text
Joni Sherman
```

* Copy link

Pegar el enlace en el correo.

* Send

⚠️ Puede aparecer:

```text
Recipients can't access links
```

Seleccionar:

```text
Send anyway
```

---

## Validar acceso View Only

* [WINDOWS] LON-CL2

* Iniciar sesión como:

```text
Joni Sherman
```

Abrir correo:

```text
Protected Document Test - View only permission
```

Abrir documento.

Verificar:

* Se abre en Reading View.
* Aparece watermark.
* No permite edición.
* Mensaje:

```text
Read only. This document is read-only.
```

---

## Validar acceso denegado desde correo personal

Abrir el correo recibido en la cuenta personal del alumno.

Intentar abrir el documento.

Verificar que:

```text
Pick an account
```

o solicitud de acceso.

Esto confirma que el documento no fue compartido con ese usuario.

---

## Compartir documento con permiso Edit

* [WINDOWS] LON-CL1

Crear un nuevo correo:

| Campo | Valor |
|---------|---------|
| To | Joni Sherman |
| Subject | Protected Document Test - Edit permission |

---

### Modificar permisos

* ProtectedDocument1
  * Share

* Link settings

Seleccionar:

```text
People you choose
```

Configurar:

```text
Can edit
```

Agregar:

```text
Joni Sherman
```

* Copy link

Pegar en el correo.

* Send

---

## Validar acceso Edit

* [WINDOWS] LON-CL2

Abrir:

```text
Protected Document Test - Edit permission
```

Abrir el documento.

Verificar:

* El documento abre en modo edición.
* Es posible modificar texto.
* La protección sigue vigente.
* Solamente Joni posee permisos de edición.

Con esto queda validado el funcionamiento de Microsoft Purview Information Protection mediante Sensitivity Labels, controlando accesos, permisos, clasificaciones y protección de documentos.

---

# Resultado final del laboratorio

Al finalizar este laboratorio:

* Se instaló Microsoft Purview Information Protection Client.
* Se habilitó soporte para Sensitivity Labels en SharePoint y OneDrive.
* Se habilitó protección de PDF.
* Se creó la Sensitivity Label **PII**.
* Se creó y publicó la Label Policy **PII Policy**.
* Se validó el comportamiento de la etiqueta existente **Project - Falcon**.
* Se comprobó el requerimiento de justificación al remover etiquetas.
* Se aplicó protección basada en permisos de compartición.
* Se verificó acceso de solo lectura.
* Se verificó acceso de edición.
* Se verificó denegación de acceso para usuarios no autorizados.

**End of Lab 9**

🎉 **Congratulations! You have completed the final lab of the course.**

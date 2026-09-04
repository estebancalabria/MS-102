# Learning Path 8 - Lab 8 - Exercise 1 - Manage DLP Policies

> Como parte del piloto de Microsoft 365 en Adatum, se implementarán políticas de Data Loss Prevention (DLP) para proteger información sensible frente a compartición accidental o no autorizada.
>
> En este ejercicio se crea una DLP Policy personalizada que detecta direcciones IP en correos electrónicos y archivos compartidos. La política contiene dos reglas:
>
> * Cuando se detecta una sola dirección IP, el usuario recibe una advertencia, pero el mensaje puede enviarse.
> * Cuando se detectan dos o más direcciones IP, el contenido se bloquea y el usuario deberá justificar el envío para poder invalidar la restricción.
>
> Posteriormente se deshabilita la funcionalidad **Send to Kindle**, ya que permite compartir documentos fuera del alcance de los controles DLP.

---

# Task 1: Create a DLP Policy with Custom Settings

> Se crea una DLP Policy personalizada denominada **IP Address DLP policy**. La política analiza correos electrónicos y documentos en Microsoft 365 buscando direcciones IP.
>
> La policy contendrá dos reglas:
>
> * **Single IP Address rule**: muestra una advertencia cuando se detecta una dirección IP.
> * **Multiple IP Address rule**: bloquea el contenido cuando se detectan dos o más direcciones IP, permitiendo override con justificación de negocio.

## Abrir Data Loss Prevention

* [BROWSER] https://purview.microsoft.com
  * Edge debería continuar abierto con sesión iniciada como **Holly Dickson**
 * [MENU] Navigation pane
   * **Solutions**
     * **Data Loss Prevention**
       * **Policies**

---

## Crear una nueva DLP Policy

* [TAB] Policies
  * **+Create policy**

### Seleccionar el tipo de política

* [TAB] Choose the type of data to protect
  * Seleccionar:

    **Enterprise applications and devices**

  * **Next**

### Revisar las plantillas disponibles

* [TAB] Start with a template or create a custom policy

  * Revisar brevemente las categorías disponibles:
    * Financial
    * Privacy
    * Medical and Health
    * Otros templates disponibles

  * Observar que:
    * Cada categoría proporciona regulaciones predefinidas.
    * La categoría **Custom** permite crear una política desde cero.

* Seleccionar:

  * Category: **Custom**
  * Template: **Custom policy**

* **Next**

### Definir nombre y descripción

* [TAB] Name your DLP policy

  * Name:

    `IP Address DLP policy`

  * Description:

    `This policy detects the presence of IP addresses in emails. End users are notified of the detection and admins receive a notification. Emails with 2 or more IP addresses are blocked from being sent.`

* **Next**

### Assign admin units

* [TAB] Assign admin units
  * Mantener configuración por defecto
  * **Next**

### Seleccionar ubicaciones protegidas

* [TAB] Choose where to assign the policy

Verificar que se encuentran seleccionadas las siguientes ubicaciones:

* Exchange email
* SharePoint sites
* OneDrive accounts
* Teams chats and channel messages

Desactivar cualquier otra ubicación que aparezca habilitada.

* Verificar:

| Ubicación | Estado |
|------------|---------|
| Exchange email | On |
| SharePoint sites | On |
| OneDrive accounts | On |
| Teams chats and channel messages | On |
| Resto de ubicaciones | Off |

* **Next**

### Seleccionar configuración avanzada

* [TAB] Define policy settings

  * Seleccionar:

    **Create or customize advanced DLP rules**

* **Next**

---

## Crear la regla "Single IP Address rule"

* [TAB] Customize advanced DLP rules
  * **+Create rule**

### Configuración básica

* Name:

  `Single IP Address rule`

* Description:

  `Email contains an IP address`

### Configurar condición

* [SECTION] Conditions
  * **+Add condition**
    * **Content contains**

* [SECTION] Content contains
  * Add → **Sensitive info types**

* [DIALOG] Sensitive info types
  * Search:

    `IP`

  * Seleccionar:

    **IP Address**

  * **Add**

### Configurar notificaciones

* [SECTION] User notifications

  * Activar:

    **Use notifications to inform your users and help educate them on the proper use of sensitive info**

  * Seleccionar:

    * Notify users in Office 365 service with a policy tip
    * Customize the policy tip text
    * Show the policy tip as a dialog for the end user before send

* Policy tip personalizado:

```text
ATTENTION! You have entered sensitive information (an IP address) in this message. You will not be prevented from sending this message, but please review whether the recipients are authorized to see this sensitive data.
```

### Configurar incident reports

* [SECTION] Incident reports

  * Verificar que:

    **Send an alert to admins when a rule match occurs**

    está en **On**

### Guardar la regla

* **Save**

---

## Crear la regla "Multiple IP Address rule"

* [TAB] Customize advanced DLP rules
  * **+Create rule**

### Configuración básica

* Name:

  `Multiple IP Address rule`

* Description:

  `Email contains two or more IP addresses`

### Configurar condición

* [SECTION] Conditions
  * **+Add condition**
    * **Content contains**

* Content contains
  * Add → Sensitive info types

* Buscar:

  `IP`

* Seleccionar:

  **IP Address**

* **Add**

### Configurar instance count

* En la fila **IP Address**

Cambiar:

* Instance count:

  `1 → 2`

De esta manera la regla solamente se activará cuando existan **dos o más direcciones IP**.

---

### Configurar acción de bloqueo

* [SECTION] Actions
  * **+Add an action**

Seleccionar:

* Restrict access or encrypt the content in Microsoft 365 locations

Expandir la sección si fuera necesario.

Mantener seleccionada la opción:

* Block users from receiving email or accessing shared SharePoint, OneDrive, and Teams files

Seleccionar:

* **Block everyone**

---

### Configurar notificaciones

* [SECTION] User notifications

Activar:

* Use notifications to inform your users and help educate them on the proper use of sensitive info

Seleccionar:

* Notify users in Office 365 service with a policy tip
* Customize the policy tip text
* Show the policy tip as a dialog for the end user before send

Policy tip personalizado:

```text
ATTENTION! You have entered sensitive information (multiple IP addresses) in this message. You will be blocked if you attempt to send this message. Overriding this block indicates you have authorized sending this sensitive data to the recipients.
```

---

### Configurar User Overrides

* [SECTION] User overrides

Seleccionar:

* Allow overrides from Microsoft 365 files and Microsoft Fabric items

Activar además:

* Require a business justification to override
* Override the rule automatically if they report it as a false positive

---

### Configurar incident reports

* [SECTION] Incident reports

Verificar que:

* Send an alert to admins when a rule match occurs

permanece en **On**

### Guardar la regla

* **Save**

---

## Activar la política

* [TAB] Customize advanced DLP rules

Verificar que aparecen ambas reglas:

* Single IP Address rule
* Multiple IP Address rule

* **Next**

### Policy Mode

* [TAB] Policy mode

Seleccionar:

* **Turn the policy on immediately**

* **Next**

### Revisar y crear

* [TAB] Review and finish

Revisar la configuración.

* **Submit**

Esperar la confirmación:

* **New policy created**

* **Done**

* Dejar todas las pestañas abiertas para el siguiente task.

Con esto queda creada la DLP Policy **IP Address DLP policy**.

---

# Task 2: Turn Off the Send to Kindle Feature that Bypasses DLP Policies

> La característica **Send to Kindle** permite enviar documentos Word directamente a bibliotecas Kindle.
>
> Este mecanismo no es evaluado por las DLP Policies, por lo que puede utilizarse para sacar información fuera de los controles de protección corporativos.
>
> Como Adatum no utilizará esta funcionalidad, se crea una política de Microsoft Intune para deshabilitarla.

---

## Abrir Microsoft Intune

* [WINDOWS] LON-CL1
  * Edge continúa abierto con sesión de Holly Dickson

* [MENU] Microsoft 365 admin center
  * Admin centers
    * **Microsoft Intune**

* [BROWSER] Microsoft Intune admin center

* [MENU]
  * **Apps**

### Abrir Policies for Microsoft 365 Apps

* [TAB] Apps | Overview

* [MENU] Manage apps
  * **Policies for Microsoft 365 apps**

---

## Crear la política

* [TAB] Apps | Policies for Microsoft 365 apps

* **Create**

### Datos básicos

* [TAB] Start with the basics

Name:

```text
Turn off Send to Kindle setting
```

* **Next**

### Scope

* [TAB] Choose the scope

Seleccionar:

* **This policy configuration applies to all users**

* **Next**

---

## Configurar el ajuste Send to Kindle

* [TAB] Configure Settings

En el cuadro Search escribir:

```text
Kindle
```

Presionar Enter.

* Debería aparecer únicamente:

  **Turn off Send to Kindle**

* Seleccionar el setting.

---

### Revisar configuración

* [DIALOG] Turn off Send to Kindle

* Revisar:
  * Plataformas soportadas
  * Aplicaciones soportadas

* Seleccionar:

  **Show more**

* Leer la descripción completa.

---

### Habilitar la configuración

* [SECTION] Configuration setting

Seleccionar:

```text
Enabled
```

⚠️ En este caso, habilitar el setting significa deshabilitar la funcionalidad Send to Kindle.

* Seleccionar:

  **Apply**

---

## Crear la policy

* [TAB] Configure Settings

Verificar:

| Setting | Status |
|----------|----------|
| Turn off Send to Kindle | Configured |

* **Next**

### Review configuration and create

* **Create**

Esperar la confirmación:

* Policy configuration created

* **Done**

* Dejar todas las pestañas abiertas para el siguiente ejercicio.

Con esto queda deshabilitada la funcionalidad **Send to Kindle** para los usuarios de Adatum, evitando la evasión de los controles DLP mediante exportación de documentos Word hacia Kindle.

---

# Learning Path 8 - Lab 8 - Exercise 2 - Test the DLP Policy

> Se validan las dos reglas configuradas en la policy **IP Address DLP policy**.
>
> Primero se prueba el comportamiento cuando un correo contiene una única dirección IP y posteriormente se prueba el bloqueo y override cuando el correo contiene múltiples direcciones IP.

⚠️ En algunos entornos de laboratorio las DLP Policies pueden tardar en propagarse debido a throttling entre las máquinas virtuales y el tenant de Microsoft 365. Si la funcionalidad no responde inmediatamente, esperar unos minutos antes de repetir la prueba.

---

## Task 1: Test the First DLP Policy Rule

> Se valida la regla **Single IP Address rule** enviando un correo con una única dirección IP. El usuario debe recibir un Policy Tip, pero el mensaje debe enviarse correctamente.

### Enviar correo de prueba

* [WINDOWS] LON-CL1
  * Holly Dickson logueada en Microsoft 365

* [MENU] Home | Microsoft 365
  * Abrir **Outlook**

* [TAB] Outlook on the web

  * **New mail**

Completar:

| Campo | Valor |
|---------|---------|
| To | Lynne Robbins |
| Subject | DLP Policy Test 1 |
| Message | Hey Lynne - I will configure this IP address: 192.168.0.1 |

* Verificar que aparece el **Policy Tip** de DLP.

* Seleccionar:

  **Send**

---

### Verificar envío

* [MENU] Sent Items
  * Confirmar que el mensaje fue enviado.

* [MENU] Inbox

Verificar recepción del correo:

```text
Notification: DLP Policy Test 1
```

Enviado por:

```text
Microsoft Outlook
```

Revisar el contenido.

---

### Verificar recepción en Lynne

* [WINDOWS] Switch a LON-CL2

* Abrir:

  [Outlook on the Web](https://outlook.office365.com)

* Iniciar sesión como:

  **Lynne Robbins**

* Revisar Inbox.

Verificar recepción del correo:

```text
DLP Policy Test 1
```

Comprobar que la dirección IP continúa presente en el cuerpo del mensaje.

* Mantener Outlook abierto.

* Volver a LON-CL1.

Con esto queda validada la regla **Single IP Address rule**.

---

## Task 2: Test the Second DLP Policy Rule

> Se valida la regla **Multiple IP Address rule** enviando un mensaje que contiene dos direcciones IP.
>
> El mensaje debe bloquearse inicialmente y posteriormente enviarse utilizando la funcionalidad de override con justificación de negocio.

### Crear el correo

* [WINDOWS] LON-CL1
  * Outlook de Holly abierto

* **New mail**

Completar:

| Campo | Valor |
|---------|---------|
| To | Lynne Robbins |
| Subject | DLP Policy Test 2 |
| Message | Hey Lynne - I will test the following IP addresses: 192.168.0.1 and 172.16.0.1 |

* Verificar que aparece el Policy Tip.

* Seleccionar:

  **Send**

---

### Verificar bloqueo

* Debería aparecer:

```text
Send blocked
```

* Seleccionar:

  **OK**

* Verificar en Sent Items que el mensaje no fue enviado.

* Abrir la carpeta **Drafts**

* Abrir el borrador correspondiente.

---

### Realizar override

En el Policy Tip:

* **Show details**
  * **Override**

Mantener seleccionada:

* I have a business justification

Ingresar:

```text
Lynne must be informed of the IP addresses I'm testing
```

* **Override**

Verificar que el mensaje del Policy Tip indique que el usuario decidió continuar con el envío.

---

### Enviar correo

* Seleccionar:

  **Send**

* Verificar en Sent Items que el mensaje fue enviado.

---

### Verificar notificación DLP

* [MENU] Inbox

Verificar recepción del correo:

```text
Notification: DLP Policy Test 2
```

Enviado por:

```text
Microsoft Outlook
```

Revisar el contenido.

---

### Validar recepción en Lynne

* [WINDOWS] Switch a LON-CL2

* Outlook de Lynne debería continuar abierto.

* Revisar Inbox.

Verificar recepción del correo:

```text
DLP Policy Test 2
```

Confirmar que ambas direcciones IP permanecen visibles en el mensaje.

* Mantener Outlook abierto.

* Volver a LON-CL1.

Con esto queda validada la regla **Multiple IP Address rule**, incluyendo bloqueo de envío, override con justificación y generación de notificaciones DLP.

---

# Resultado final del laboratorio

Al finalizar este laboratorio:

* Se creó la DLP Policy **IP Address DLP policy**.
* Se implementó una regla de advertencia para una única dirección IP.
* Se implementó una regla de bloqueo para múltiples direcciones IP.
* Se configuraron incident reports para los administradores.
* Se configuraron Policy Tips personalizados para los usuarios.
* Se habilitó la capacidad de override con justificación de negocio.
* Se deshabilitó la funcionalidad **Send to Kindle** mediante Microsoft Intune.
* Se validó el funcionamiento de ambas reglas mediante pruebas reales de correo electrónico.

**End of Lab 8**

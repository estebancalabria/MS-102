# Learning Path 8 - Lab X - Exercise 1 - Create and Test a DLP Policy

> Como parte de las iniciativas de protección de datos de Adatum, se implementará una política de Data Loss Prevention (DLP) para impedir que los usuarios envíen números de tarjetas de crédito por correo electrónico.
>
> En este ejercicio se crea una DLP Policy que detecta números de tarjeta de crédito y bloquea automáticamente el envío del mensaje.

---

# Task 1: Create a DLP Policy

## Abrir Data Loss Prevention

* [BROWSER] https://purview.microsoft.com

* [MENU] Navigation pane
  * Solutions
    * Data Loss Prevention
      * Policies

---

## Crear una nueva DLP Policy

* [TAB] Policies
  * **+ Create policy**

### Seleccionar el tipo de política

* [TAB] Choose the type of data to protect

Seleccionar:

* Enterprise applications and devices

* **Next**

---

### Crear una política personalizada

* [TAB] Start with a template or create a custom policy

Seleccionar:

* Category: **Custom**
* Template: **Custom policy**

* **Next**

---

### Definir nombre

* [TAB] Name your DLP policy

Name:

```text
Credit Card DLP Policy
```

Description:

```text
Blocks emails that contain credit card numbers.
```

* **Next**

---

### Assign admin units

* Mantener configuración por defecto

* **Next**

---

### Seleccionar ubicaciones protegidas

* [TAB] Choose where to assign the policy

Habilitar únicamente:

* Exchange email

Deshabilitar todas las demás ubicaciones.

* **Next**

---

### Configuración avanzada

* [TAB] Define policy settings

Seleccionar:

* Create or customize advanced DLP rules

* **Next**

---

## Crear la regla

* [TAB] Customize advanced DLP rules
  * **+ Create rule**

### Configuración básica

Name:

```text
Block Credit Card Numbers
```

Description:

```text
Blocks emails containing credit card numbers.
```

---

### Configurar condición

* [SECTION] Conditions
  * **+ Add condition**
    * **Content contains**

* [SECTION] Content contains
  * Add → Sensitive info types

Buscar:

```text
Credit Card Number
```

Seleccionar:

* Credit Card Number

* **Add**

---

### Configurar acción

* [SECTION] Actions
  * **+ Add an action**

Seleccionar:

* Restrict access or encrypt the content in Microsoft 365 locations

Mantener:

* Block users from receiving email

Seleccionar:

* Block everyone

---

### Configurar notificaciones

* [SECTION] User notifications

Activar:

* Use notifications to inform your users and help educate them on the proper use of sensitive info
* Notify users in Office 365 service with a policy tip
* Customize the policy tip text
* Show the policy tip as a dialog for the end user before send

Policy Tip:

```text
This message contains a credit card number and cannot be sent.
```

---

### Guardar la regla

* **Save**

---

## Activar la política

* Verificar que aparece la regla:

  * Block Credit Card Numbers

* **Next**

### Policy Mode

Seleccionar:

* Turn the policy on immediately

* **Next**

### Review and finish

* **Submit**

Esperar:

* New policy created

* **Done**

---

# Task 2: Test the DLP Policy

> Se valida el funcionamiento de la política enviando un correo electrónico con un número de tarjeta de crédito.

---

## Crear el correo

* [WINDOWS] LON-CL1

* Abrir Outlook

* **New mail**

Completar:

| Campo | Valor |
|---------|---------|
| To | Lynne Robbins |
| Subject | Credit Card Test |
| Message | Customer credit card number: 4532 0151 1283 0366 |

---

### Intentar enviar

* Seleccionar:

  **Send**

---

## Verificar el bloqueo

Verificar:

* Aparece un Policy Tip indicando que se detectó información sensible.
* El mensaje no puede enviarse.
* Outlook muestra una advertencia de bloqueo.

---

## Confirmar que el correo no fue enviado

* [MENU] Sent Items

Verificar:

* El correo **no aparece** en elementos enviados.

---

## Resultado

Al finalizar este laboratorio:

* Se creó una DLP 

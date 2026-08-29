# [TEÓRICO] Configuración inicial del tenant
**Slides:** 3-14  
**Duración:** 50-60 minutos

---

# 1. ¿Qué es un tenant? (Slides 3-5)

## Mensaje principal

Cuando una organización compra Microsoft 365 no solamente adquiere licencias.

Microsoft crea un tenant de Microsoft Entra ID donde se almacenan:

- Usuarios
- Grupos
- Aplicaciones
- Configuraciones
- Políticas

El tenant es el límite administrativo de la organización dentro de Microsoft 365. 【1-62c152】

## Demo

* [BROWSER] https://admin.cloud.microsoft/
     * [TOP-NAVBAR] [LINK] Contoso
         * 👁️ -> Nombre del tenant
         * 👁️ -> Dominio onmicrosoft.com
     * [MENU] Billing -> Your products
        * 👁️ -> Microsoft Power Apps for Developer
        * [LINK] Add More Products (Marketplace)
            * [ ] Tildar checkbox de hasta 3 productos a comparar
            * [LINK] Compare products
                 * 👁️ -> Tabla comparativa lado a lado (features por producto)
     * [MENU] Billing -> Licenses
        * 👁️ ->Microsoft 365 E5
        * Microsoft 365 E5
        * Total licenses
        * Assigned licenses
        * Available licenses
       

---

# 2. Configurar el Organizational Profile (Slide 6)

## Mensaje principal

* Antes de crear usuarios debemos definir la identidad de la organización.
* El perfil organizativo incluye varias cosas como nombre, direccion, etc
* La región elegida durante la creación del tenant es muy importante porque afecta:
- Servicios disponibles
- Facturación
- Regulaciones
- Ubicación de datos


## Demo

* [BROWSER] https://admin.cloud.microsoft/
     * [MENU] Settings → Org Settings
        * [TAB] Organization Profile
           * [LINK] Irganization information
                  - Contacto técnico
                  - Información corporativa

---

# 3. Compartición en SharePoint y OneDrive (Slide 9)

## Mensaje principal

Una de las primeras decisiones de seguridad consiste en definir cómo se compartirá información con usuarios externos.

La configuración existe en varios niveles:

```text
Tenant
   ↓
SharePoint
   ↓
Sitio
```

## Demo

* [BROWSER] https://admin.cloud.microsoft/
     * [MENU] Show All
     * [MENU] Admin centers → SharePoint
* (NEW WINDOW)
* [BROWSER] https://xxxx-admin.sharepoint.com
     * [MENU] Policies → Sharing


* Explicación
   * Esta configuración controla cómo se comparte información fuera de la organización.
   * La configuración más restrictiva siempre prevalece. ``


---

# 6. Configuración de Teams (Slide 10)

## Mensaje principal

Teams debe ser gobernado. Existen configuraciones Organizativas, Políticas de reuniones, Políticas de mensajería

## Demo

* [BROWSER] https://admin.cloud.microsoft/
     * [MENU] Show All
     * [MENU] Admin centers → Teams
* (NEW WINDOW)
* [BROWSER] https://admin.teams.microsoft.com/
     * [MENU] (Show ALL)
     * [MENU] Meetings → Meetings policies
        * [ITEM] Global (Org-wide default)
           * 👁️ ->  Mostrar que se puede hacer en una meeting de teams
           * 👁️ ->  Mostrá opciones concretas como Recording, Transcription y Screen sharing.
     * [MENU] Messaging → Messaging policies
          * [ITEM] Global (Org-wide default)
           * 👁️ ->  Mostrar que se puede hacer con los mensajes de teams

---

# 7. Auditoría Unificada (Slide 11)

## Mensaje principal

La auditoría permite responder preguntas como:

- ¿Quién eliminó un usuario?
- ¿Quién compartió un archivo?
- ¿Quién modificó una configuración?
- ¿Quién creó un Team?

Entra ID muestra quién inició sesión.

Purview Audit muestra qué acciones realizaron los usuarios y administradores después. 【1-c77bd8】

## Demo

* [BROWSER] https://admin.cloud.microsoft/
     * [MENU] Show All
     * [MENU] Admin centers → Microsoft Purview
* (NEW WINDOW)
* [BROWSER] https://purview.microsoft.com
     * [MENU] Solutions → Audit
         * [BUTTON] Start recording audit
         * 👁️ -> Búsqueda de actividades
         * 👁️ -> Actividades de usuarios
         * 👁️ -> Actividades administrativas

## Explicación

* Microsoft centraliza la auditoría de Microsoft 365 en Purview.
* Desde aquí pueden investigarse acciones realizadas sobre usuarios, grupos, archivos, Teams y otros servicios.

---

# 8. Tenant Readiness Checklist (Slide 12)

## Mensaje principal

Antes de poner el entorno en producción debemos validar que todo esté preparado.

### Identidad

- ¿Los usuarios ya fueron creados?
   - [BROWSER] https://admin.cloud.microsoft/
      - [MENU] Users → Active users

- ¿Los administradores tienen los roles correctos?
   - [BROWSER] https://admin.cloud.microsoft/
      - [MENU] Roles → Role assignments

- ¿MFA está configurado?
   - [BROWSER] https://entra.microsoft.com
      - [MENU] Protection → Authentication methods

### Correo

- ¿Los usuarios tienen buzón?
   - [BROWSER] https://admin.exchange.microsoft.com
      - [MENU] Recipients → Mailboxes

- ¿El flujo de correo funciona correctamente?
   - [BROWSER] https://admin.exchange.microsoft.com
      - [MENU] Mail flow

### Infraestructura

- ¿El dominio corporativo ya fue agregado?
   - [BROWSER] https://admin.cloud.microsoft/
      - [MENU] Settings → Domains

- ¿Los registros DNS ya fueron configurados?
   - [BROWSER] https://admin.cloud.microsoft/
      - [MENU] Settings → Domains
         - [ITEM] Seleccionar dominio

- ¿Existe sincronización con Active Directory?
   - [BROWSER] https://entra.microsoft.com
      - [SEARCH] Entra Connect

### Dispositivos

- ¿Los dispositivos están enrolados?
   - [BROWSER] https://intune.microsoft.com
      - [MENU] Devices

- ¿Existe una estrategia de gobierno para los dispositivos?
   - [BROWSER] https://intune.microsoft.com
      - [MENU] Devices → Compliance policies

   - [BROWSER] https://intune.microsoft.com
      - [MENU] Devices → Configuration profiles

### Herramientas mencionadas

- RCA (Remote Connectivity Analyzer)
   - [BROWSER] https://testconnectivity.microsoft.com

- SaRA (Support and Recovery Assistant)
   - [BROWSER] https://aka.ms/SaRA
  
---

# Resumen del bloque

Cuando una empresa implementa Microsoft 365 normalmente sigue este orden:

1. Comprender el tenant.
2. Validar suscripciones y licencias.
3. Configurar el perfil organizativo.
4. Definir reglas de compartición.
5. Configurar Teams.
6. Activar auditoría.
7. Revisar el checklist de preparación.

Recién después comenzamos a crear usuarios y grupos.

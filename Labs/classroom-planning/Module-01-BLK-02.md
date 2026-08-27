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

### Microsoft 365 Admin Center

Mostrar:

- Nombre del tenant
- Dominio onmicrosoft.com
- Suscripciones instaladas
- Cantidad de licencias

## Pregunta para la clase

¿Qué diferencia existe entre:

- Tenant
- Suscripción
- Licencia

---

# 2. Configurar el Organizational Profile (Slide 6)

## Mensaje principal

Antes de crear usuarios debemos definir la identidad de la organización.

El perfil organizativo incluye:

- Nombre
- Dirección
- Teléfono
- Contacto técnico
- Dominio principal

La región elegida durante la creación del tenant es muy importante porque afecta:

- Servicios disponibles
- Facturación
- Regulaciones
- Ubicación de datos

【1-62c152】

## Demo

### Settings → Org Settings → Organization Profile

Mostrar:

- Nombre de la organización
- Contacto técnico
- Información corporativa

---

# 3. Licencias y suscripciones (Slide 7)

## Mensaje principal

Un usuario sin licencia prácticamente no puede utilizar los servicios de Microsoft 365.

Las licencias determinan:

- Qué puede usar un usuario
- Cuántos usuarios pueden trabajar
- Qué servicios están disponibles

【1-62c152】

## Demo

### Billing → Licenses

Mostrar:

- Licencias compradas
- Licencias asignadas
- Licencias disponibles

## Pregunta para la clase

¿Qué ocurre si tengo:

- 100 usuarios
- 20 licencias

?

---

# 4. Servicios adicionales y Marketplace (Slide 8)

## Mensaje principal

Microsoft 365 puede ampliarse mediante:

- Servicios Microsoft
- Add-ons
- Azure Marketplace

Las organizaciones suelen agregar:

- Project
- Visio
- Stream
- Soluciones de terceros

【1-62c152】

## Demo

### Billing → Purchase Services

Mostrar:

- Catálogo de servicios

### Azure Marketplace

Mostrar:

- Marketplace
- Private Marketplace

---

# 5. Compartición en SharePoint y OneDrive (Slide 9)

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

Siempre prevalece la configuración más restrictiva.

【1-62c152】

## Demo

### SharePoint Admin Center

Ir a:

Policies → Sharing

Mostrar:

- Anyone
- New and Existing Guests
- Existing Guests
- Only People in your Organization

## Pregunta para la clase

Si el sitio permite compartir pero el tenant lo bloquea:

¿Funcionará?

---

# 6. Configuración de Teams (Slide 10)

## Mensaje principal

Teams debe ser gobernado.

Existen configuraciones:

- Organizativas
- Políticas de reuniones
- Políticas de mensajería

【1-62c152】

## Demo

### Teams Admin Center

Mostrar:

- Guest Access
- Meeting Policies
- Messaging Policies

Explicar ejemplos:

- Grabación
- Transcripción
- Invitados
- Compartición de pantalla

## Pregunta para la clase

¿Dónde configurarían que los usuarios puedan grabar reuniones?

---

# 7. Auditoría (Slide 11)

## Mensaje principal

Una organización debe poder responder:

- Quién hizo una acción
- Cuándo ocurrió
- Qué cambió

Para eso existe Unified Audit Logging.

【1-62c152】

## Demo

### Microsoft Purview

Ir a:

Audit

Mostrar:

- Búsqueda
- Actividades registradas
- Eventos auditables

## Caso práctico

Un administrador elimina un usuario.

¿Cómo averiguamos quién realizó la acción?

---

# 8. Tenant Readiness Checklist (Slide 12)

## Mensaje principal

Antes de poner el entorno en producción debemos validar que todo esté preparado.

### Identidad

- Usuarios
- Roles
- MFA

### Correo

- Mailboxes
- Mail Flow

### Infraestructura

- Dominios
- DNS
- Entra Connect

### Dispositivos

- Intune
- Gobernanza

【1-62c152】

## Herramientas mencionadas

- RCA (Remote Connectivity Analyzer)
- SaRA (Support and Recovery Assistant)

【1-62c152】

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

---

# Portales a mostrar durante la clase

- Microsoft 365 Admin Center
- Entra Admin Center
- SharePoint Admin Center
- Teams Admin Center
- Microsoft Purview
- Billing / Licenses

Tiempo estimado total: **50-60 minutos**

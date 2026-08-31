# [TEÓRICO] Privileged Identity Management (PIM) (**Slides:** 61-66)

---

# 1. ¿Qué es PIM? (Slides 61-62)

Microsoft Entra Privileged Identity Management (PIM) permite administrar, controlar y monitorear el acceso a roles privilegiados.

Ayuda a reducir el riesgo eliminando privilegios permanentes innecesarios.

- Gestiona acceso a Azure, Microsoft 365 e Intune.
- Aplica el principio de mínimo privilegio.
- Reduce la exposición de cuentas administrativas.

* [BROWSER] https://entra.microsoft.com
     * [MENU] Identity Governance → Privileged Identity Management
          * 👁️ -> Dashboard de PIM
          * 👁️ -> Roles privilegiados

---

# 2. Just-In-Time Administration (Slide 63)

PIM introduce el concepto de "Just-In-Time" (JIT).

Los usuarios no mantienen privilegios administrativos permanentes.

- El usuario recibe una asignación Eligible.
- El rol permanece inactivo.
- Se activa únicamente cuando es necesario.
- La elevación tiene una duración limitada.

* [BROWSER] https://entra.microsoft.com
     * [MENU] Identity Governance → Privileged Identity Management
          * [ITEM] Microsoft Entra Roles
               * 👁️ -> Eligible assignments
               * 👁️ -> Active assignments

---

# 3. Roles compatibles con PIM (Slide 63)

PIM puede utilizarse para proteger distintos tipos de roles.

- Microsoft Entra Roles
- Azure Roles
- PIM for Groups

Los roles más habituales son:

- Global Administrator
- Security Administrator
- Exchange Administrator
- Intune Administrator

* [BROWSER] https://entra.microsoft.com
     * [MENU] Identity Governance → Privileged Identity Management
          * [ITEM] Microsoft Entra Roles
               * 👁️ -> Lista de roles protegibles

---

# 4. Flujo de activación de un rol (Slide 64)

Cuando un usuario necesita privilegios administrativos debe activar el rol.

La organización puede exigir controles adicionales antes de conceder acceso.

- MFA
- Justificación empresarial
- Aprobación
- Tiempo máximo de activación

* [BROWSER] https://entra.microsoft.com
     * [MENU] Identity Governance → Privileged Identity Management
          * [ITEM] My roles
               * [BUTTON] Activate
                    * 👁️ -> Justification
                    * 👁️ -> Duration
                    * 👁️ -> MFA requirement

---

# 5. Aprobaciones y elevación de privilegios (Slide 64)

PIM permite implementar flujos de aprobación.

Algunos roles pueden requerir autorización previa antes de activarse.

Roles involucrados:

- Privileged Role Administrator
- Approver
- Eligible User

* [BROWSER] https://entra.microsoft.com
     * [MENU] Identity Governance → Privileged Identity Management
          * [ITEM] Approve requests
               * 👁️ -> Pending requests
               * 👁️ -> Approve
               * 👁️ -> Reject

---

# 6. Configuración de PIM (Slide 65)

La configuración de PIM normalmente incluye:

- Configurar parámetros del rol.
- Asignar usuarios elegibles.
- Definir aprobadores.
- Configurar expiración.
- Configurar requisitos MFA.

* [BROWSER] https://entra.microsoft.com
     * [MENU] Identity Governance → Privileged Identity Management
          * [ITEM] Microsoft Entra Roles
               * [ITEM] Global Administrator
                    * [TAB] Settings
                         * 👁️ -> Activation requirements
                         * 👁️ -> Approval requirements
                         * 👁️ -> Maximum duration

---

# 7. Asignar usuarios elegibles (Slide 65)

Los administradores pueden asignar usuarios como Eligible o Active.

- Active: acceso permanente.
- Eligible: acceso bajo demanda.

La recomendación es utilizar Eligible siempre que sea posible.

* [BROWSER] https://entra.microsoft.com
     * [MENU] Identity Governance → Privileged Identity Management
          * [ITEM] Microsoft Entra Roles
               * [ITEM] Global Administrator
                    * [BUTTON] Add assignments
                         * 👁️ -> Eligible
                         * 👁️ -> Active

---

# 8. Auditoría y seguimiento (Slide 66)

Todas las activaciones y cambios quedan registrados.

PIM proporciona trazabilidad completa de:

- Activaciones
- Solicitudes
- Aprobaciones
- Asignaciones
- Cambios de configuración

* [BROWSER] https://entra.microsoft.com
     * [MENU] Identity Governance → Privileged Identity Management
          * [ITEM] Audit history
               * 👁️ -> Activaciones realizadas
               * 👁️ -> Cambios de roles
               * 👁️ -> Historial de aprobaciones

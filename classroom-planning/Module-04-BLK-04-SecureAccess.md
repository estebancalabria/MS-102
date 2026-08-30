# [TEÓRICO] Administración del acceso seguro (**Slides:** 25-38)

---

# 1. Herramientas de identidad y acceso (Slide 27)

Microsoft Entra ID centraliza la administración de identidades, aplicaciones y acceso a los recursos de Microsoft 365. 【1-bfe876】

## Demo

* [BROWSER] https://entra.microsoft.com
    * [MENU] Identity → Overview
        * 👁️ -> Información general del tenant
    * [MENU] Applications → Enterprise applications
        * 👁️ -> Aplicaciones empresariales registradas

---

# 2. Administración y protección de contraseñas (Slide 28)


La protección de credenciales es un componente fundamental de la seguridad y Microsoft recomienda complementarla con MFA y controles adicionales de protección de contraseñas. 【1-bfe876】

## Demo

* [BROWSER] https://entra.microsoft.com
    * [MENU] Protection → Authentication methods
        * 👁️ -> Métodos configurados
    * [MENU] Protection → Password Protection
        * 👁️ -> Protección de contraseñas
        * 👁️ -> Smart Lockout

---

# 3. Directivas de acceso condicional (Slide 29)

Las políticas de acceso condicional permiten controlar el acceso según usuario, ubicación, dispositivo, aplicación y nivel de riesgo. 【1-bfe876】

## Demo

* [BROWSER] https://entra.microsoft.com
    * [MENU] Protection → Conditional Access → Policies
        * 👁️ -> Políticas configuradas
        * [ITEM] Seleccionar una política
            * 👁️ -> Usuarios incluidos
            * 👁️ -> Aplicaciones
            * 👁️ -> Condiciones
            * 👁️ -> Grant Controls

---

# 4. Autenticación multifactor (Slide 31)

MFA agrega una segunda validación al proceso de autenticación para reducir el riesgo de uso indebido de credenciales comprometidas. 【1-bfe876】

## Demo

* [BROWSER] https://entra.microsoft.com
    * [MENU] Protection → Authentication methods
        * 👁️ -> Microsoft Authenticator
        * 👁️ -> FIDO2 Security Keys
        * 👁️ -> SMS

---

# 5. Autenticación sin contraseña (Slide 32)

Los métodos passwordless eliminan la dependencia de contraseñas tradicionales y ayudan a mejorar seguridad y experiencia de usuario. 【1-bfe876】

## Demo

* [BROWSER] https://entra.microsoft.com
    * [MENU] Protection → Authentication methods
        * 👁️ -> Passkeys (FIDO2)
        * 👁️ -> Microsoft Authenticator
        * 👁️ -> Windows Hello for Business

---

# 6. Self-Service Password Reset (Slide 33)

Self-Service Password Reset permite que los usuarios restablezcan sus propias contraseñas sin intervención del soporte técnico. 【1-bfe876】

## Demo

* [BROWSER] https://entra.microsoft.com
    * [MENU] Protection → Password reset
        * 👁️ -> Estado de habilitación
        * 👁️ -> Usuarios y grupos incluidos
        * 👁️ -> Authentication methods

---

# 7. Security Defaults (Slide 35)


Security Defaults proporciona una configuración básica de seguridad recomendada por Microsoft para proteger rápidamente el tenant. 【1-bfe876】

## Demo

* [BROWSER] https://entra.microsoft.com
    * [MENU] Identity → Overview → Properties
        * 👁️ -> Manage Security Defaults

---

# 8. Sign-in Logs (Slide 36)

Los registros de inicio de sesión permiten investigar accesos, validar políticas de seguridad y analizar incidentes de autenticación. 【1-bfe876】

## Demo

* [BROWSER] https://entra.microsoft.com
    * [MENU] Identity → Monitoring & health → Sign-in logs
        * 👁️ -> Inicios de sesión recientes
        * 👁️ -> Estado del acceso
        * 👁️ -> MFA Requirement
        * 👁️ -> Ubicación
        * 👁️ -> Conditional Access


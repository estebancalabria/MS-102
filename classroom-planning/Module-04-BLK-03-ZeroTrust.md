# [TEÓRICO] Exploración del modelo de seguridad Zero Trust (**Slides:** 17-24)
---

# 1. Principios y componentes de Zero Trust (Slide 19)

Zero Trust parte de que ninguna solicitud debe considerarse confiable de forma predeterminada, por lo que cada acceso debe verificarse explícitamente, concederse con el menor privilegio posible y evaluarse asumiendo que la organización puede haber sido vulnerada. 

## Demo

* [BROWSER] [Abrir Microsoft Entra Admin Center](https://entra.microsoft.com)
    * [MENU] Identity → Overview
        * 👁️ -> Identidades del tenant
    * [MENU] Identity → Devices → All devices
        * 👁️ -> Dispositivos registrados y unidos a Microsoft Entra
    * [MENU] Identity → Applications → Enterprise applications
        * 👁️ -> Aplicaciones empresariales integradas

---

# 2. Planificación de una estrategia Zero Trust (Slide 20)

La implementación de Zero Trust requiere fortalecer las credenciales, reducir la superficie de ataque, automatizar la respuesta ante amenazas, aumentar la visibilidad mediante registros y alertas, y verificar explícitamente identidades, dispositivos y datos antes de permitir el acceso.

## Demo

* [BROWSER] [Abrir Microsoft Entra Admin Center](https://entra.microsoft.com)
    * [MENU] Protection → Authentication methods
        * 👁️ -> Métodos de autenticación habilitados
    * [MENU] Identity → Monitoring & health → Sign-in logs
        * 👁️ -> Registros de inicio de sesión
        * 👁️ -> Estado y resultado de las autenticaciones

---

# 3. Acceso condicional en una estrategia Zero Trust (Slide 21)

El acceso condicional permite verificar las señales asociadas a cada solicitud y aplicar controles según la identidad, el dispositivo, la ubicación, la aplicación y otras condiciones, evitando confiar únicamente en que el acceso procede de la red corporativa.

## Demo

* [BROWSER] [Abrir Microsoft Entra Admin Center](https://entra.microsoft.com)
    * [MENU] Protection → Conditional Access → Policies
        * 👁️ -> Políticas configuradas
        * [ITEM] Seleccionar una política
            * 👁️ -> Usuarios incluidos y excluidos
            * 👁️ -> Recursos de destino
            * 👁️ -> Condiciones configuradas
            * 👁️ -> Controles para conceder o bloquear el acceso
            * 👁️ -> Estado de la política

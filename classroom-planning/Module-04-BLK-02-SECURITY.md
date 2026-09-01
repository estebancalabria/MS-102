# [TEÓRICO] Análisis de vectores de amenazas y filtraciones de datos (**Slides:** 3-16)

---

# 1. Phishing y Spear Phishing (Slide 6) - Spoofing de correo electrónico (Slide 7) - Spam y Malware (Slide 8)
## Defender for 365

* El phishing es uno de los vectores de ataque más utilizados para obtener credenciales y acceso a los sistemas corporativos mediante correos aparentemente legítimos.
* El spoofing busca hacer creer al usuario que un correo fue enviado por una organización o remitente legítimo cuando en realidad proviene de un atacante.
* El malware suele distribuirse mediante correo electrónico utilizando archivos adjuntos o enlaces maliciosos que buscan comprometer dispositivos y datos corporativos.

* [BROWSER] https://security.microsoft.com
    * [MENU] Email & collaboration → Explorer
        * 👁️ -> Mensajes detectados como Phishing
        * 👁️ -> Acciones realizadas por Defender
        * 👁️ -> Correos bloqueados o puestos en cuarentena
        * 👁️ -> Detecciones Anti-phishing
        * 👁️ -> Eventos de Spoof Intelligence
    * [MENU] Email & collaboration → Review
        * [MENU] Quarantine
            * 👁️ -> Correos bloqueados
            * 👁️ -> Archivos adjuntos sospechosos
              
---

# 4. Microsoft Entra ID Protection (Slide 9)

Las cuentas comprometidas permiten a los atacantes acceder a recursos corporativos utilizando credenciales válidas y normalmente son el punto de inicio de ataques más avanzados. 
* Risky sign-in = el inicio de sesión que fue considerado riesgoso
* Risk detection = la señal/motivo que hizo que Microsoft lo considerara riesgoso
* Risky user = el usuario que acumula riesgo
Algunos ejemplos de risk detections:
* Anonymous IP address
* Leaked credentials
* Impossible travel
* Malicious IP address
* Password spray
* Unfamiliar sign-in properties
* Anomalous token

* [BROWSER] https://entra.microsoft.com
    * [MENU] Protection → Risky users
        * 👁️ -> Usuarios identificados como riesgosos
    * [MENU] Protection → Risky sign-ins
        * 👁️ -> Inicios de sesión sospechosos

---

# 5. Exfiltración y eliminación de datos (Slides 11-12)

La protección de datos requiere controles que eviten tanto la extracción no autorizada de información como la eliminación maliciosa de contenido crítico.

* [BROWSER] https://admin.cloud.microsoft
    * [MENU] Show all
    * [MENU] Admin centers → Purview
        * 👁️ -> Data Loss Prevention
        * 👁️ -> Políticas existentes

---

# 6. Exposición accidental de información (Slide 13)

La exposición accidental ocurre cuando usuarios comparten contenido sensible fuera de los límites previstos por la organización, muchas veces sin intención maliciosa.

## Demo

* [BROWSER] https://admin.cloud.microsoft
    * [MENU] Admin centers → SharePoint
        * [MENU] Policies → Sharing
            * 👁️ -> Configuración de compartición externa

---

# 7. Ataques de contraseñas y amenazas internas (Slide 14)

Las contraseñas débiles y el uso indebido de privilegios siguen siendo causas habituales de incidentes de seguridad tanto internos como externos.

## Demo

* [BROWSER] https://entra.microsoft.com
    * [MENU] Protection → Authentication methods
        * 👁️ -> Métodos de autenticación habilitados
    * [MENU] Protection → Identity Protection
        * 👁️ -> Vulnerabilidades detectadas


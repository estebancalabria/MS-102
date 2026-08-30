# [TEÓRICO] Protección del correo electrónico (**Slides:** 3-13)
---

# 1. Exchange Online Protection (Slides 4-6)


Exchange Online Protection (EOP) proporciona la capa básica de protección de correo en Microsoft 365 mediante filtrado antimalware, antispam y análisis de amenazas antes de que lleguen al buzón del usuario. 【1-a42428】


* [BROWSER] https://security.microsoft.com
    * [MENU] Email & collaboration → Policies & rules → Threat policies
        * 👁️ -> Anti-malware policies
        * 👁️ -> Configuración predeterminada
        * 👁️ -> Políticas personalizadas

---

# 2. Protección antispam (Slide 7)

EOP analiza todos los correos entrantes y les asigna niveles de confianza para identificar spam, phishing y correo masivo no deseado. 


* [BROWSER] https://security.microsoft.com
    * [MENU] Email & collaboration → Policies & rules → Threat policies
        * 👁️ -> Anti-spam policies
        * 👁️ -> Acciones configuradas para Spam
        * 👁️ -> Acciones configuradas para High confidence phishing

---

# 3. Zero-hour Auto Purge (Slide 8)


Zero-hour Auto Purge (ZAP) permite retirar mensajes maliciosos detectados después de haber sido entregados a los usuarios. 


* [BROWSER] https://security.microsoft.com
    * [MENU] Email & collaboration → Explorer
        * 👁️ -> Correos puestos en cuarentena
        * 👁️ -> Detecciones posteriores a la entrega

---

# 4. Protección contra Spoofing (Slides 9-10)


Microsoft 365 utiliza tecnologías como SPF, DKIM, DMARC y Spoof Intelligence para validar remitentes y reducir ataques de suplantación de identidad. 【1-a42428】


* [BROWSER] https://security.microsoft.com
    * [MENU] Email & collaboration → Policies & rules → Threat policies
        * 👁️ -> Anti-phishing policies
    * [MENU] Email & collaboration → Policy → Tenant Allow/Block Lists
        * 👁️ -> Spoofed senders

---

# 5. Filtrado de correo saliente (Slide 11)


El correo saliente también es supervisado para detectar cuentas comprometidas y evitar que la organización envíe spam a terceros. 

* [BROWSER] https://security.microsoft.com
    * [MENU] Email & collaboration → Policies & rules → Threat policies
        * 👁️ -> Outbound spam policies
        * 👁️ -> Límites y acciones configuradas



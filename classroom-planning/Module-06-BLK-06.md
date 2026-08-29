# [TEÓRICO] Administración de Safe Links
**Slides:** 36-45
**Duración:** 45-60 minutos

---

# 1. Introducción a Safe Links (Slides 37-38)

## Mensaje principal

Safe Links protege a los usuarios frente a URL maliciosas utilizadas en campañas de phishing mediante validación y análisis en tiempo real antes de acceder al sitio web. 【1-535a0f】

## Demo

* [BROWSER] https://security.microsoft.com

    * [MENU] Email & collaboration → Policies & rules → Threat policies

        * 👁️ -> Safe Links

        * 👁️ -> Preset security policies

---

# 2. Configuración de políticas Safe Links (Slide 39)

## Mensaje principal

Las directivas Safe Links permiten controlar cómo se inspeccionan enlaces, aplicar análisis en tiempo real y registrar los clics realizados por los usuarios. 【1-535a0f】

## Demo

* [BROWSER] https://security.microsoft.com

    * [MENU] Email & collaboration → Policies & rules → Threat policies

        * [MENU] Safe Links

            * 👁️ -> Real-time URL scanning

            * 👁️ -> Track user clicks

            * 👁️ -> Internal email protection

---

# 3. Administración y prioridad de políticas (Slides 40-41)

## Mensaje principal

Las directivas pueden administrarse desde Defender o PowerShell y se aplican en función de su prioridad y alcance sobre usuarios, grupos o dominios. 【1-535a0f】

## Demo

* [BROWSER] https://security.microsoft.com

    * [MENU] Email & collaboration → Policies & rules → Threat policies

        * [MENU] Safe Links

            * 👁️ -> Lista de políticas

            * 👁️ -> Prioridad de aplicación

---

# 4. Exclusiones mediante reglas de transporte (Slide 42)

## Mensaje principal

Es posible excluir determinados remitentes o escenarios confiables utilizando reglas de flujo de correo en Exchange Online. 【1-535a0f】

## Demo

* [BROWSER] https://admin.exchange.microsoft.com

    * [MENU] Mail flow → Rules

        * 👁️ -> Reglas existentes

        * 👁️ -> Condiciones y excepciones

---

# 5. Experiencia del usuario final (Slide 43)

## Mensaje principal

Cuando un usuario selecciona un enlace, Safe Links valida el destino y permite el acceso o muestra una advertencia según el nivel de riesgo detectado. 【1-535a0f】

## Demo

* [BROWSER] https://security.microsoft.com

    * [MENU] Email & collaboration → Explorer

        * 👁️ -> URL click reports

        * 👁️ -> Detecciones relacionadas con Safe Links

---

# Resumen del bloque

1. Comprender cómo funciona Safe Links.
2. Configurar protección frente a URL maliciosas.
3. Administrar prioridades y ámbitos de aplicación.
4. Implementar exclusiones mediante reglas de transporte.
5. Analizar el comportamiento observado por los usuarios.

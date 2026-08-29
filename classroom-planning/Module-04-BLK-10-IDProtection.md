# [TEÓRICO] Análisis de Microsoft Entra ID Protection
**Slides:** 73-80
**Duración:** 45-60 minutos

---

# 1. Riesgo de usuario y riesgo de inicio de sesión (Slides 75-76)

## Mensaje principal

Microsoft Entra ID Protection utiliza señales de riesgo y análisis basados en machine learning para detectar identidades potencialmente comprometidas y accesos sospechosos. 【1-8134d2】

## Demo

* [BROWSER] https://entra.microsoft.com

    * [MENU] Protection → Identity Protection → Risky users

        * 👁️ -> Usuarios identificados como riesgosos

        * 👁️ -> Nivel de riesgo

        * 👁️ -> Estado de remediación

    * [MENU] Protection → Identity Protection → Risky sign-ins

        * 👁️ -> Inicios de sesión de riesgo

        * 👁️ -> Nivel de riesgo detectado

---

# 2. Directivas basadas en riesgo (Slide 76)

## Mensaje principal

Las políticas basadas en riesgo permiten automatizar respuestas frente a accesos sospechosos o identidades comprometidas aplicando MFA o bloqueando el acceso según el nivel de riesgo detectado. 【1-8134d2】

## Demo

* [BROWSER] https://entra.microsoft.com

    * [MENU] Protection → Identity Protection → User risk policy

        * 👁️ -> Usuarios incluidos

        * 👁️ -> Nivel de riesgo configurado

        * 👁️ -> Controles de acceso

    * [MENU] Protection → Identity Protection → Sign-in risk policy

        * 👁️ -> Configuración de la política

        * 👁️ -> Controles aplicados

---

# 3. Vulnerabilidades y detección de eventos de riesgo (Slide 77)

## Mensaje principal

Identity Protection identifica vulnerabilidades y actividades potencialmente maliciosas, incluyendo credenciales filtradas, ubicaciones inusuales y accesos sospechosos. 【1-8134d2】

## Demo

* [BROWSER] https://entra.microsoft.com

    * [MENU] Protection → Identity Protection → Dashboard

        * 👁️ -> Vulnerabilities

        * 👁️ -> Risk detections

        * 👁️ -> Users with leaked credentials

        * 👁️ -> Unfamiliar sign-in properties

---

# 4. Investigación y mitigación de riesgos (Slide 78)

## Mensaje principal

El panel de Identity Protection permite investigar incidentes, priorizar riesgos y aplicar acciones para reducir el impacto de una posible identidad comprometida. 【1-8134d2】

## Demo

* [BROWSER] https://entra.microsoft.com

    * [MENU] Protection → Identity Protection → Overview

        * 👁️ -> Resumen de riesgos

    * [MENU] Protection → Identity Protection → Risk detections

        * [ITEM] Seleccionar detección

            * 👁️ -> Detalles del evento

            * 👁️ -> Usuario afectado

            * 👁️ -> Nivel de riesgo

            * 👁️ -> Acciones de remediación

---

# Resumen del bloque

1. Analizar usuarios de riesgo.
2. Analizar inicios de sesión riesgosos.
3. Revisar políticas basadas en riesgo.
4. Detectar credenciales filtradas.
5. Identificar eventos sospechosos.
6. Investigar incidentes de identidad.
7. Aplicar acciones de mitigación.

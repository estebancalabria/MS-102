# Zero Trust

## Introducción

Las organizaciones necesitan un modelo de seguridad que:

* Se adapte a la complejidad del entorno moderno.
* Adopte el trabajo móvil.
* Proteja personas, dispositivos, aplicaciones y datos sin importar su ubicación.

**Zero Trust** es el modelo de seguridad de Microsoft 365 orientado a esta realidad. Aborda amenazas externas e internas y considera la seguridad, el riesgo empresarial y la complejidad de un mundo cada vez más conectado.

El entrenamiento busca ayudar a las organizaciones a:

* Tratar seguridad, cumplimiento, identidad y administración de dispositivos como un conjunto interdependiente.
* Extender la protección a datos, dispositivos, identidades, plataformas y nubes, sean de Microsoft o no.

---

## Principios y componentes de Zero Trust

Zero Trust es una estrategia de seguridad basada en **“nunca confiar, siempre verificar”**. En lugar de asumir que todo lo que está detrás del firewall corporativo es seguro, cada solicitud se considera potencialmente comprometida y debe ser autenticada, autorizada y cifrada antes de conceder acceso.

Utiliza microsegmentación, acceso con mínimos privilegios, inteligencia y análisis para reducir el movimiento lateral y detectar anomalías en tiempo real.

### Principios

* **Verificar explícitamente:** autenticar y autorizar considerando todos los datos disponibles: identidad, ubicación, estado del dispositivo, servicio o carga de trabajo, clasificación de datos y anomalías.
* **Usar acceso con mínimos privilegios:** limitar el acceso mediante JIT, JEA, políticas adaptativas basadas en riesgo y protección de datos.
* **Asumir una brecha:** minimizar el impacto de una brecha y evitar el movimiento lateral mediante segmentación, cifrado de extremo a extremo y análisis para detectar amenazas y mejorar las defensas.

### Seis componentes

* **Identidades:** verificar identidades mediante autenticación sólida y aplicar mínimo privilegio.
* **Endpoints:** supervisar el estado y cumplimiento de dispositivos, incluyendo IoT, smartphones, BYOD, dispositivos de partners y servidores locales o cloud.
* **Aplicaciones:** descubrir shadow IT, controlar permisos, accesos, acciones de usuarios, configuraciones y comportamientos anómalos.
* **Datos:** clasificar, etiquetar y cifrar los datos y restringir su acceso según sus atributos.
* **Infraestructura:** evaluar versiones, configuraciones y acceso JIT; utilizar telemetría para detectar ataques y comportamientos riesgosos.
* **Redes:** segmentar redes, aplicar microsegmentación, protección contra amenazas, cifrado de extremo a extremo, monitoreo y análisis.

Zero Trust reemplaza la confianza predeterminada por una **confianza basada en excepciones**, con capacidades integradas para detectar amenazas, responder y bloquear eventos no deseados.

---

## Plan para implementar Zero Trust

Zero Trust considera todo como si estuviera en Internet, incluso los recursos ubicados dentro de redes consideradas seguras. El modelo tradicional supone que usuarios y dispositivos dentro de la red son confiables, pero vulnerabilidades, phishing, sitios maliciosos o archivos infectados pueden comprometerlos.

Las organizaciones deben pasar de la confianza implícita a la **verificación explícita**.

### Cinco pasos para proteger la infraestructura de identidad

1. **Fortalecer las credenciales:** utilizar contraseñas seguras y MFA.
2. **Reducir la superficie de ataque:** eliminar protocolos inseguros, limitar puntos de entrada y controlar el acceso administrativo.
3. **Automatizar la respuesta a amenazas:** reducir el tiempo disponible para que los atacantes permanezcan en el entorno.
4. **Aumentar la visibilidad:** utilizar auditoría, registros y alertas para detectar patrones de compromiso.
5. **Habilitar autoservicio para usuarios:** reducir fricción y mantener la productividad.

### Verificación explícita

Se debe verificar explícitamente:

* Las afirmaciones de autenticación.
* Los dispositivos.
* La clasificación y cifrado de los datos.

El riesgo de cada sesión debe considerar:

* Identidad del usuario.
* Estado del dispositivo.
* Aplicaciones utilizadas.
* Sensibilidad de los datos solicitados.

Las políticas determinan cuándo permitir, bloquear o restringir el acceso y pueden exigir:

* MFA.
* Limitación de funcionalidades, como descargas.
* Controles de cumplimiento, como términos de uso.

Estas políticas protegen frente a amenazas externas e internas y crean controles para que los empleados utilicen los recursos de forma responsable.

---

## Zero Trust con Microsoft Entra Conditional Access

**Microsoft Entra ID** proporciona la verificación de identidad adaptativa necesaria para Zero Trust.

**Conditional Access** permite definir políticas basadas en prácticamente cualquier aspecto del inicio de sesión, incluyendo el riesgo del usuario o de la sesión.

Puede considerar:

* Rol del usuario.
* Membresía de grupos.
* Estado y cumplimiento del dispositivo.
* Aplicaciones móviles.
* Ubicación.
* Riesgo del inicio de sesión.

Según estas condiciones, puede:

* Permitir el acceso.
* Denegarlo.
* Solicitar MFA.
* Aplicar términos de uso.
* Aplicar restricciones de acceso.

Microsoft Entra ID Protection y Conditional Access toman decisiones dinámicas considerando usuario, dispositivo, ubicación y riesgo de sesión. Primero se evalúa el contexto del inicio de sesión y luego se aplican las políticas correspondientes para permitir únicamente accesos autorizados y conformes.

---

## Zero Trust Assessment

La implementación depende de:

* Requisitos de la organización.
* Tecnologías existentes.
* Etapa de seguridad.

La herramienta **Zero Trust Assessment** determina el nivel de madurez en:

* Identidades.
* Dispositivos.
* Aplicaciones.
* Infraestructura.
* Redes.
* Datos.

Clasifica la madurez en:

* **Traditional**
* **Advanced**
* **Optimal**

También proporciona recomendaciones para avanzar a la siguiente etapa.

---

## Estrategia de Zero Trust para redes

Zero Trust no se limita a proteger una red definida, sino todos los datos que circulan por los sistemas.

El cloud, los dispositivos móviles y otros endpoints han ampliado los límites tradicionales. Ya no existe necesariamente una red contenida y definida: existe un conjunto amplio de dispositivos y redes conectados mediante cloud.

### Objetivos para proteger las redes

* Prepararse para ataques antes de que ocurran.
* Minimizar el alcance y velocidad de propagación del daño.
* Aumentar la dificultad de comprometer el entorno cloud.

Se aplican los mismos principios:

* **Verificar explícitamente.**
* **Usar acceso con mínimos privilegios.**
* **Asumir una brecha.**

### Redes Zero Trust con Microsoft 365

La defensa tradicional basada en perímetro pierde relevancia debido al trabajo móvil, los servicios cloud públicos y BYOD. Un atacante que comprometa un endpoint puede expandirse rápidamente dentro de una red confiable.

Una red Zero Trust elimina la confianza basada en la ubicación de red y utiliza afirmaciones de confianza sobre usuarios y dispositivos para controlar el acceso.

#### Componentes

* **Identity Provider:** mantiene información de usuarios.
* **Device Directory:** registra dispositivos autorizados y sus características.
* **Policy Evaluation Service:** determina si usuario o dispositivo cumplen las políticas.
* **Access Proxy:** utiliza las señales anteriores para permitir o denegar acceso.

Las decisiones dinámicas permiten habilitar determinados recursos desde cualquier dispositivo y restringir recursos de alto valor a dispositivos administrados y conformes.

---

## Objetivos de implementación de Zero Trust para redes

### Situación inicial habitual

* Pocos perímetros de seguridad y redes abiertas y planas.
* Protección mínima contra amenazas y filtrado estático.
* Tráfico interno sin cifrar.

### Primeros objetivos

* **Segmentación:** múltiples microperímetros cloud de entrada/salida con cierta microsegmentación.
* **Protección contra amenazas:** filtrado y protección cloud-native contra amenazas conocidas.
* **Cifrado:** tráfico interno entre usuario y aplicación cifrado.

### Objetivos posteriores

* **Segmentación:** microperímetros cloud distribuidos y microsegmentación más profunda.
* **Protección contra amenazas:** protección y filtrado basados en machine learning y señales contextuales.
* **Cifrado:** todo el tráfico cifrado.

---

## Conditional Access para Zero Trust Networking

El control basado únicamente en quién puede acceder a un recurso no es suficiente. También debe considerarse **cómo se accede**.

Microsoft Entra ID Conditional Access es un componente fundamental para implementar Zero Trust en redes. Junto con Microsoft Entra ID Protection, toma decisiones dinámicas según:

* Usuario.
* Dispositivo.
* Ubicación.
* Riesgo de sesión.

Utiliza señales sobre el estado de seguridad del dispositivo Windows y la confiabilidad de la sesión e identidad.

Las organizaciones pueden decidir permitir, bloquear o restringir el acceso mediante MFA, términos de uso u otros controles.

Ejemplos:

* Exigir MFA desde una ubicación no confiable.
* Exigir MFA desde un dispositivo no administrado.
* Bloquear acceso desde determinadas naciones.
* Aplicar controles adicionales para aplicaciones o datos de alto riesgo.

Microsoft Entra ID calcula un nivel de riesgo para usuarios e inicios de sesión y proporciona políticas base de Conditional Access que aplican MFA en escenarios de alto riesgo.

---

# Adoptar un enfoque Zero Trust

El enfoque Zero Trust abarca cuatro áreas principales:

1. **Identity**
2. **Security**
3. **Compliance**
4. **Skilling**

## 1. Identity

La identidad es la primera línea de defensa en un entorno donde desaparecen los perímetros corporativos. Microsoft recomienda comenzar con una base sólida de identidad cloud, autenticación fuerte, protección de credenciales y dispositivos.

### Microsoft Entra ID

* **Passwordless authentication:** elimina la dependencia de contraseñas mediante:

  * Windows Hello for Business.
  * Microsoft Authenticator.
  * Claves de seguridad FIDO2 compatibles.
  * Temporary Access Pass para configurar o recuperar credenciales passwordless.
* **Microsoft Entra Conditional Access:** motor de políticas de Zero Trust que protege información sin restringir innecesariamente el acceso. Puede aplicar políticas según acciones del usuario y sensibilidad de los datos.
* **Microsoft Entra verifiable credentials:** permite verificar información como educación o certificaciones sin recopilar ni almacenar los datos personales correspondientes.

---

## 2. Security

La estrategia de seguridad parte del principio **assume breach**, buscando reducir la complejidad y fragmentación mediante soluciones integradas.

Microsoft combina capacidades **SIEM** y **XDR** para mejorar protección, visibilidad y respuesta.

### Capacidades

* **Microsoft Defender for Endpoint y Microsoft Defender for Office 365:** investigación y remediación desde Microsoft Defender, con alertas unificadas y análisis automatizado.
* **Microsoft Defender XDR y Microsoft Sentinel:** experiencias y esquemas comunes, conectores y automatización.
* **Threat Analytics:** informes de investigadores de seguridad de Microsoft para comprender, prevenir y mitigar amenazas activas.
* **Secured-core:** capacidades de seguridad integradas en hardware, firmware, drivers y sistema operativo, con protección desde antes del arranque.
* **Microsoft Defender for Endpoint:** disponible para Android, iOS, macOS, Linux y Windows.
* **Microsoft Sentinel:** supervisa entornos multicloud, incluyendo AWS, Google Cloud Platform, Salesforce, VMware y Cisco Umbrella.

> Microsoft 365 Defender pasó a denominarse **Microsoft Defender XDR**.

---

## 3. Compliance

Zero Trust también protege **desde dentro hacia fuera**, gestionando riesgos relacionados con los datos en Microsoft cloud, otras nubes y plataformas.

### Capacidades de Microsoft Purview

* **Coauthoring con Microsoft Purview Information Protection:** permite trabajar simultáneamente sobre documentos protegidos.
* **Microsoft Purview Insider Risk Management:** identifica posibles actividades de riesgo interno mediante análisis de logs y actividad histórica.
* **Data Loss Prevention (DLP):** disponible para navegadores Chrome y entornos locales como file shares y SharePoint Server.
* **Microsoft Purview Information Protection:** permite aplicar las mismas etiquetas de sensibilidad a datos almacenados en otras nubes o entornos locales.
* **Microsoft Purview:** solución unificada de gobierno de datos para entornos locales, multicloud y SaaS, con capacidad para analizar y clasificar datos en AWS S3, SAP ECC, SAP S4/HANA y Oracle Database.

---

## 4. Skilling

Microsoft busca reducir la brecha de habilidades de seguridad mediante recursos de formación y certificaciones.

### Certificaciones

* **Security, Compliance, and Identity Fundamentals:** fundamentos de seguridad, cumplimiento e identidad.
* **Information Protection Administrator Associate:** planificación e implementación de controles de cumplimiento.
* **Security Operations Analyst Associate:** diseño de sistemas de protección y respuesta ante amenazas.
* **Identity and Access Administrator Associate:** diseño, implementación y operación de sistemas de identidad y acceso mediante Microsoft Entra ID.

Microsoft también proporciona la **Microsoft Security Technical Content Library** como recurso de aprendizaje sobre seguridad.

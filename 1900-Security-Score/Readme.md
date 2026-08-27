# Microsoft Secure Score

## Introducción

Microsoft Secure Score es una herramienta de análisis de seguridad cuyo objetivo es:

* Mostrar qué acciones realizó una organización para reducir el riesgo sobre sus datos.
* Identificar qué puede hacer para reducir aún más ese riesgo.

Secure Score determina qué servicios de Microsoft 365 utiliza la organización, analiza su configuración y comportamiento y los compara con una línea base definida por Microsoft.

En lugar de reaccionar ante alertas de seguridad, permite **realizar seguimiento y planificar mejoras incrementales de seguridad a largo plazo**.

## ¿Qué es Microsoft Secure Score?

Microsoft Secure Score es una **medición de la postura de seguridad** de una organización. Cuantas más acciones de mejora se implementen, mayor será la puntuación.

Desde un panel centralizado del Microsoft 365 Security Center, permite supervisar y mejorar la seguridad de:

* Identidades.
* Datos.
* Aplicaciones.
* Dispositivos.
* Infraestructura.

Ayuda a:

* Informar sobre el estado actual de la postura de seguridad.
* Mejorarla mediante descubrimiento, visibilidad, orientación y control.
* Comparar resultados con referencias y establecer indicadores clave de rendimiento (KPI).
* Visualizar métricas y tendencias.
* Integrarse con otros productos de Microsoft.
* Compararse con organizaciones similares.

Las acciones recomendadas también pueden considerarse cubiertas por soluciones de terceros.

> **Importante:** Secure Score es un resumen numérico de la postura de seguridad basado en configuraciones, comportamiento de usuarios y otras mediciones relacionadas con la seguridad. No indica la probabilidad absoluta de sufrir una brecha ni garantiza que una organización esté protegida contra ellas. Representa el grado de adopción de controles de seguridad que pueden ayudar a reducir el riesgo.

## Cómo funciona Secure Score

Se obtienen puntos mediante:

* Configuración de características de seguridad recomendadas.
* Realización de tareas relacionadas con seguridad.
* Resolución de una acción mediante una aplicación, software de terceros o una mitigación alternativa.

Las acciones pueden otorgar:

* **Puntos completos:** cuando se completan totalmente.
* **Puntos parciales:** cuando se aplican solo a una parte de los usuarios o dispositivos.

Si una organización no puede o no desea implementar una acción, puede **aceptar el riesgo o el riesgo restante**.

Secure Score muestra recomendaciones de los productos compatibles con la licencia disponible. El panel muestra el conjunto completo de recomendaciones posibles para un producto, independientemente de la edición, suscripción o plan.

La postura de seguridad representada por Secure Score no cambia según las licencias adquiridas. Debe buscarse un equilibrio entre seguridad y usabilidad, ya que no todas las recomendaciones son adecuadas para todos los entornos.

El score se actualiza en tiempo real para reflejar la información mostrada en las visualizaciones y páginas de acciones recomendadas, y sincroniza diariamente los datos del sistema relacionados con los puntos obtenidos.

Para Microsoft Teams, el estado de las recomendaciones se actualiza cuando cambia la configuración, mientras que el estado de recomendación se actualiza una vez al mes.

## Puntuación de las acciones recomendadas

Cada acción recomendada vale **10 puntos o menos** y la mayoría se puntúa de forma binaria.

* Si se implementa completamente una acción, se obtiene el 100 % de sus puntos.
* Algunas acciones calculan los puntos como porcentaje del total de configuración.

Ejemplo:

* 100 usuarios en la organización.
* La MFA está habilitada para 50 usuarios.
* La acción vale 10 puntos.
* Puntuación obtenida: **5 puntos**.

`50 usuarios protegidos / 100 usuarios totales × 10 puntos = 5 puntos`

## Productos incluidos

Secure Score incluye recomendaciones para:

* Microsoft 365, incluido Exchange Online.
* Microsoft Entra ID.
* Microsoft Defender for Endpoint.
* Microsoft Defender for Identity.
* Microsoft Defender for Cloud Apps.
* Microsoft Teams.

Las recomendaciones no cubren todas las superficies de ataque de cada producto, pero proporcionan una línea base. Las acciones también pueden marcarse como cubiertas por terceros o mediante una mitigación alternativa.

> **Nota:** Azure Active Directory (Azure AD) ahora se denomina Microsoft Entra ID.

## Security Defaults

Secure Score incluye acciones recomendadas relacionadas con **Security Defaults de Microsoft Entra ID**.

Al habilitar Security Defaults, se obtienen los puntos completos para:

* Permitir que todos los usuarios puedan completar MFA para acceso seguro: **9 puntos**.
* Requerir MFA para roles administrativos: **10 puntos**.
* Habilitar una política para bloquear la autenticación heredada: **7 puntos**.

Security Defaults incluye características con una seguridad similar a las acciones recomendadas **Sign-in Risk Policy** y **User Risk Policy**. Microsoft recomienda marcar estas acciones como **Resolved through alternative mitigation** en lugar de configurarlas adicionalmente sobre Security Defaults.

# Evaluar la postura de seguridad

El panel de Secure Score organiza las acciones recomendadas en:

* **Identity:** cuentas y roles de Microsoft Entra.
* **Device:** Microsoft Defender for Endpoint.
* **Apps:** correo electrónico y aplicaciones cloud, incluidos Office 365 y Microsoft Defender for Cloud Apps.
* **Data:** mediante Microsoft Purview Information Protection.

En la pestaña **Overview** se puede consultar:

* Puntuación total.
* Evolución histórica del Secure Score.
* Comparaciones con organizaciones similares.
* Acciones recomendadas priorizadas.

## Consultar el score actual

En **Overview → Your secure score** se muestra:

* La puntuación como porcentaje.
* Los puntos obtenidos.
* El total de puntos posibles.

También pueden incluirse diferentes vistas:

* **Planned score:** puntuación proyectada si se completan las acciones planificadas.
* **Current license score:** puntuación alcanzable con las licencias actuales.
* **Achievable score:** puntuación alcanzable considerando las licencias y los riesgos aceptados.

# Mejorar Secure Score

Secure Score determina el estado actual de la postura de seguridad e identifica riesgos. Después, la organización debe analizar los resultados y planificar las mejoras considerando:

* Potencial de riesgo.
* Dificultad de implementación.
* Plazos de implementación.
* Impacto de cada acción sobre la puntuación.

Con estos factores se establecen prioridades y una hoja de ruta hacia un entorno más seguro.

La planificación e implementación debe involucrar a los principales responsables, como:

* CISO.
* Responsable de seguridad de TI.
* Administradores de Active Directory local.
* Administradores de Exchange.
* Administradores de Microsoft Entra ID.
* Administradores de redes.

## Diseñar un plan de actualización de seguridad

Cada organización define sus propios criterios de éxito:

* Algunas buscan alcanzar la puntuación máxima.
* Otras establecen una puntuación intermedia.
* Algunas priorizan las cinco acciones principales.
* Otras priorizan las acciones que requieren menor esfuerzo.

No existe un enfoque único.

Un enfoque habitual consiste en comenzar por acciones que tengan **bajo impacto sobre la productividad y proporcionen beneficios inmediatos**, como:

* Habilitar MFA para todas las cuentas administrativas.
* Asignar el rol de Global Administrator a más de un usuario.
* Habilitar auditoría en las cargas de trabajo.
* Habilitar auditoría de buzones.
* Revisar semanalmente los intentos de inicio de sesión:

  * Después de múltiples fallos.
  * Desde fuentes desconocidas.
  * Desde múltiples ubicaciones geográficas.

Las prioridades dependen de cada organización. Sectores regulados, como finanzas y salud, pueden utilizar plazos más agresivos e implementar soluciones como:

* Data Loss Prevention.
* Information Rights Management.

Estas soluciones pueden tener mayor impacto sobre los usuarios y requerir más tiempo de implementación.

Microsoft recomienda asignar un **sponsor** que ayude a organizar reuniones, eliminar obstáculos y mantener a los equipos dentro del cronograma.

La evaluación de Secure Score no debería ser un proyecto único. La postura de seguridad cambia con el tiempo debido a nuevos usuarios, administradores, regulaciones, servicios y características de Microsoft 365. Se recomienda ejecutar Secure Score periódicamente, aproximadamente cada seis meses.

# Acciones recomendadas

La pestaña **Recommended actions** muestra recomendaciones de seguridad relacionadas con posibles superficies de ataque y sus estados.

Las acciones pueden:

* Buscarse.
* Filtrarse.
* Agruparse.

Estados disponibles:

* **To address**
* **Planned**
* **Risk accepted**
* **Resolved through third party**
* **Resolved through alternate mitigation**
* **Completed**

Una vez completada una acción, el score puede tardar entre **24 y 48 horas** en reflejar los cambios.

## Ranking

Las acciones se priorizan según:

* Cantidad de puntos restantes.
* Dificultad de implementación.
* Impacto sobre los usuarios.
* Complejidad.

Las acciones con mayor prioridad tienen muchos puntos disponibles y bajo nivel de dificultad, impacto y complejidad.

## Detalles de una acción recomendada

Al seleccionar una acción se muestra una página con sus detalles.

Opciones:

* **Manage:** permite acceder al portal correspondiente para realizar el cambio y obtener los puntos de la acción.
* **Share:** permite copiar el enlace directo y compartirlo por correo electrónico, Microsoft Teams o Microsoft Planner.

También se pueden agregar **Notes** para registrar avances o comentarios y crear etiquetas propias para filtrar las acciones.

## Estados de las acciones

### To address

La organización reconoce que la acción es necesaria y planea abordarla en el futuro. También se aplica a acciones parcialmente completadas.

### Planned

Existen planes concretos para completar la acción.

### Risk accepted

La organización acepta el riesgo o el riesgo restante y decide no implementar la recomendación. No otorga puntos y puede consultarse en el historial o revertirse posteriormente.

### Resolved through third party / alternate mitigation

La acción ya está cubierta mediante una herramienta interna, aplicación de terceros o mitigación alternativa. Se obtienen los puntos correspondientes.

Microsoft no tiene visibilidad sobre el grado de completitud de la implementación cuando se utilizan estos estados.

## Acciones para dispositivos

Las acciones de Secure Score de la categoría **Device** no permiten seleccionar directamente un estado. El sistema dirige a la recomendación de seguridad correspondiente de **Microsoft Defender Vulnerability Management**.

* Una **Global exception** actualiza la justificación de la excepción en Secure Score. La actualización puede tardar hasta 2 horas.
* Una **Exception per device group** no actualiza Secure Score y la acción permanece como **To address**.

## Acciones completadas

Una acción obtiene el estado **Completed** cuando alcanza todos sus puntos posibles.

El sistema confirma las acciones completadas mediante datos de Microsoft y no permite modificar su estado.

# Evaluar información e impacto sobre usuarios

La sección **At a glance** muestra:

* Categoría.
* Ataques contra los que puede proteger.
* Producto involucrado.

Al completar una acción:

* **User impact** muestra el efecto sobre la experiencia de los usuarios.
* **Users affected** identifica a las personas afectadas.

## Implementación

La sección **Implementation** muestra:

* Prerrequisitos.
* Pasos necesarios para completar la acción.
* Estado actual de implementación.
* Enlaces de **Learn more**.

Los prerrequisitos pueden incluir licencias o acciones necesarias antes de implementar la recomendación. Se deben verificar las licencias disponibles y asignarlas a los usuarios correspondientes.

# Historial y objetivos

La pestaña **History** permite consultar la evolución del score a lo largo del tiempo.

Incluye:

* Gráfico histórico.
* Acciones realizadas en el período seleccionado.
* Puntos obtenidos.
* Categoría de cada acción.

Se puede personalizar:

* Rango de fechas.
* Categoría.

Al seleccionar una acción asociada a una actividad, se puede abrir su información completa y consultar el historial específico de esa acción.

# Métricas y tendencias

La pestaña **Metrics and trends** proporciona gráficos para analizar tendencias y establecer objetivos.

Incluye:

* **Your Secure Score zone:** personalizada según los objetivos y definiciones de puntuaciones buenas, aceptables y malas.
* **Regression trend:** evolución de los puntos perdidos debido a cambios de configuración, usuarios o dispositivos.
* **Comparison trend:** comparación del Secure Score con otras organizaciones a lo largo del tiempo.
* **Risk acceptance trend:** evolución de las acciones marcadas como **Risk accepted**.
* **Score changes:** puntos obtenidos, puntos perdidos y cambios en el score durante el período seleccionado.

El rango de fechas puede configurarse para toda la página de visualizaciones.

# Comparación con organizaciones similares

Secure Score permite comparar la puntuación con organizaciones similares mediante:

* **Comparison bar chart**, disponible en **Overview**.
* **Comparison trend**, disponible en **Metrics and trends**.

La comparación puede mostrar:

* Puntuación.
* Oportunidad de mejora.
* Promedio de organizaciones con una cantidad de usuarios similar.
* Comparaciones personalizadas.

Los datos de comparación son **anónimos**, por lo que Microsoft no sabe exactamente qué tenants forman parte de la comparación.

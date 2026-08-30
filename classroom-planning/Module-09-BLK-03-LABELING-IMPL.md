# Implementar etiquetas de confidencialidad (Slides: 22-31)

* [BROWSER] https://purview.microsoft.com

    * ## 2. Habilitar Sensitivity Labels para SharePoint y OneDrive (Slide 25)

    * [MENU] Solutions → Information Protection → Labels
        * 👁️ -> SharePoint y OneDrive pueden procesar documentos protegidos mediante etiquetas de confidencialidad.
        * 👁️ -> La funcionalidad permite coautoría, búsqueda, eDiscovery y DLP sobre contenido cifrado.
        * 👁️ -> Las etiquetas y configuraciones de protección permanecen asociadas al archivo.
        * 👁️ -> Los servicios pueden analizar contenido protegido para aplicar controles adicionales.

    * ## 3. Requisitos para crear etiquetas de confidencialidad (Slide 26)

    * [MENU] Solutions → Information Protection → Labels
        * 👁️ -> Antes de crear etiquetas deben revisarse los requisitos de licenciamiento.
        * 👁️ -> Es necesario definir la estrategia de clasificación de datos.
        * 👁️ -> Cada etiqueta debe tener configurados los controles de protección apropiados.
        * 👁️ -> Las etiquetas posteriormente deben publicarse mediante directivas.

    * ## 4. Crear y publicar etiquetas de confidencialidad (Slides 27-28)

    * [MENU] Solutions → Information Protection → Labels
        * 👁️ -> Las etiquetas se crean y configuran en Microsoft Purview.
        * 👁️ -> Las etiquetas pueden incluir cifrado, marcado visual y restricciones de acceso.
        * 👁️ -> Una organización puede crear múltiples etiquetas según sus necesidades.

    * [MENU] Solutions → Information Protection → Label policies
        * 👁️ -> Las directivas publican etiquetas a usuarios y grupos específicos.
        * 👁️ -> Las directivas determinan qué etiquetas estarán disponibles para cada usuario.
        * 👁️ -> La publicación de etiquetas se realiza mediante una Label Policy.

    * ## 5. Retirar y eliminar etiquetas de confidencialidad (Slide 29)

    * [MENU] Solutions → Information Protection → Labels
        * 👁️ -> Una etiqueta puede retirarse de una directiva sin ser eliminada.
        * 👁️ -> Los usuarios dejan de ver las etiquetas retiradas cuando se actualiza la directiva.
        * 👁️ -> Las etiquetas también pueden eliminarse definitivamente.
        * 👁️ -> El contenido previamente protegido continúa conservando la protección aplicada.

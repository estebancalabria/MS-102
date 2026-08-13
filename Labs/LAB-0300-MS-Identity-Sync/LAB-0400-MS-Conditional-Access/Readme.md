# LAB-0300-Conditional-Access

> Este lab implementa tres capas de seguridad de acceso para Adatum: MFA mediante una Conditional Access policy (excluyendo al equipo del pilot project), Pass-through Authentication (PTA) vía Microsoft Entra Connect Sync, y Microsoft Entra Smart Lockout configurado desde el Entra admin center.
> ⚠️ Excluir usuarios de MFA no es una práctica real recomendada; se hace acá solo para agilizar el resto del training.

## Task 1: Crear una Conditional Access policy para implementar MFA
> Se crea una policy que exige MFA a todos los usuarios y todas las apps/ubicaciones, excluyendo al grupo del pilot project (incluida Holly) para no tener que pasar por MFA en el resto del curso.
* [WINDOWS] LON-CL1 -> Browser (Holly logueada, admin center abierto)
* [MENU] Microsoft 365 admin center -> Admin centers -> **Identity** (abre Entra admin center en nueva pestaña; Pick an account -> Holly)
* [MENU] Entra ID -> **Authentication methods** -> **SMS** -> Enable -> Save
* [MENU] Entra ID -> **Conditional Access** -> Policies -> **+ New policy**
  * Name: `MFA for all Microsoft 365 users`
  * [TAB] Users or agents -> **0 users or agents select**
    * [TAB] Include -> **All users** (aparece warning de lockout, se resuelve abajo)
    * [TAB] Exclude -> tildar **Users and groups** -> Groups -> tildar **M365 pilot project** -> Select
  * [TAB] Target resources -> **No target resources selected** -> dropdown **Resources (formerly cloud apps)**
    * [TAB] Include -> default es **None** (⚠️ si se deja así, ningún cloud app pide MFA)
    * (opcional) **Select resources** -> None -> se abre panel Resources, solo para ver el nivel de granularidad -> **X** para cerrar sin seleccionar nada
    * [TAB] Include -> seleccionar **All resources (formerly 'All cloud apps')**
    * [TAB] Exclude -> revisar pero **no** seleccionar ningún app
  * **Network (NEW)** -> **Not configured** -> toggle **Configure** a **Yes**
    * [TAB] Include -> verificar **Any network or location**
    * [TAB] Exclude -> verificar **Selected networks and locations** -> Select en **None** (nada excluido)
  * [TAB] Access controls -> Grant -> **0 controls selected**
    * Verificar **Grant access** -> tildar **Require multifactor authentication** -> Select
  * **Enable policy** -> **On**
  * ⚠️ Tildar **I understand that my account will be impacted by this policy. Proceed anyway.**
  * **Create**
* Verificar en **Conditional Access | Policies** que la policy aparece con **State = On**
* Dejar LON-CL1 con las pestañas abiertas para el siguiente task

## Task 2: Probar MFA con un usuario incluido y uno excluido
> Se prueba la policy iniciando sesión primero como Adele (no está en el pilot project, debe pedir MFA) y después como Holly (sí está en el pilot project, no debe pedir MFA).
* [WINDOWS] LON-CL1 -> Microsoft 365 admin center -> ícono Holly -> **Sign out**
* Cerrar el browser (limpiar caché) -> reabrir Edge -> `https://www.microsoft365.com/`
* [LOGIN] Pick an account -> **Use another account** -> `AdeleV@xxxxxZZZZZZ.onmicrosoft.com` -> Next -> User Password -> Sign in
* Aparece **Let's keep your account secure** -> Next (pantalla de Microsoft Authenticator)
  * ⚠️ Si no se tiene teléfono, esto confirma que la policy pide MFA; saltar directo al paso de re-login como Holly
  * **Set up a different way to sign-in** (no confundir con "Set up a different authentication app")
  * [DIALOG] Add a sign-in method -> **Phone**
  * Elegir país -> ingresar número -> **Text a code** -> Next
  * Ingresar código de 6 dígitos recibido -> Next -> Done
  * Si aparece **Stay signed in?** -> tildar "Don't show this again" -> Yes
  * Si aparece **Welcome to Microsoft 365** -> flecha derecha x2 -> check
  * Si aparece **Create with Microsoft 365** -> cerrar con X
  * App launcher -> **Word** -> confirma acceso post-MFA
* [WINDOWS] Admin center -> ícono Adele -> **Sign out**
* Cerrar browser (limpiar caché) -> reabrir Edge -> `https://www.microsoft365.com/`
* [LOGIN] Pick an account -> `Holly@xxxxxZZZZZZ.onmicrosoft.com` -> Next -> Administrative Password -> Sign in
  * ⚠️ No debe pedir MFA (Holly está excluida) -> entra directo a **Microsoft 365 Home**
  * Welcome dialog / Create with M365 -> cerrar si aparecen
  * Admin icon -> volver a **Microsoft 365 admin center**
* Dejar LON-CL1 abierto con el admin center para el siguiente task

## Task 3: Implementar Microsoft Entra Pass-Through Authentication (PTA)
> Se reconfigura Microsoft Entra Connect Sync para cambiar el método de sign-in a PTA, permitiendo validar las passwords contra el AD on-premises sin sincronizarlas a la nube.
* [WINDOWS] LON-DC1
* [WINDOWS] Start -> All Apps -> **Azure AD Connect** -> **Azure AD Connect** (abre wizard de Microsoft Entra Connect Sync)
* Welcome -> mensaje de scheduler suspendido -> **Configure**
* [TAB] Additional tasks -> **Change user sign-in** -> Next
* Connect to Microsoft Entra ID -> username ya completo `Holly@xxxUPNxxx.onmicrosoft.com` -> password (Administrative Password) -> Next
* [TAB] User sign-in -> seleccionar **Pass-through authentication** -> Next
* [TAB] Enable single sign-on -> **Enter credentials**
  * [DIALOG] Forest Credentials -> `Adatum\Administrator` / `Pa55w.rd` -> OK
  * Esperar check verde -> Next
* [TAB] Ready to configure -> verificar tildado **Start the synchronization process when configuration completes** -> **Configure**
* [TAB] Configuration complete -> verificar mensaje de método de sign-in = PTA -> **Exit**
### Verificar PTA
* [WINDOWS] Edge -> pestaña Microsoft 365 admin center -> Admin centers -> **Identity**
* [MENU] Entra ID -> **Entra Connect** -> **Connect Sync**
  * Sección **User sign-in** -> verificar **Pass-through authentication = Enabled** -> click para abrir detalle
  * Verificar servidor listado: **LON-DC1.Adatum.com**
  * Cerrar con **X** -> **Home** para volver
* LON-DC1 queda abierto para el siguiente task

## Task 4: Implementar Microsoft Entra Smart Lockout
> Se configuran el umbral y duración de bloqueo por intentos fallidos y una lista de contraseñas prohibidas, primero viendo la alternativa on-premises (Group Policy) y luego configurando realmente en Entra admin center.
* [WINDOWS] LON-DC1 -> Server Manager -> Tools -> **Group Policy Management**
* Consola -> Forest:Adatum.com -> Domains -> Adatum.com -> click derecho **Default Domain Policy** -> **Edit**
* [MENU] Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Account Policies -> **Account Lockout Policy**
  * ⚠️ Ningún parámetro está definido acá; Adatum usará el Entra admin center en su lugar (más simple pero menos granular que Group Policy)
### Configurar en Entra admin center
* [WINDOWS] Edge -> Entra admin center
* [MENU] Entra ID -> **Authentication methods** -> **Password protection**
  * **Custom smart lockout**
    * Lockout threshold: `3`
    * Lockout duration in seconds: `90`
  * **Custom banned passwords**
    * Enforce custom list: **Yes**
    * Lista (una por línea): `Password01`, `F00tball01`, `Se@Hawks1`, `Never4get!!`
  * Mode: **Enforced**
  * **Save**
### Probar banned password
* Ícono Holly -> **View account** -> tile **Password** -> **CHANGE PASSWORD**
* Nueva pestaña -> Old password: Administrative Password -> New/Confirm password: `Never4get!!` -> Submit
  * ⚠️ Verificar mensaje de error (password prohibida)
* Cerrar pestaña de Change password
### Probar lockout threshold (con Laura)
* Ícono Holly -> **Sign out**
* Cerrar todas las pestañas salvo Sign in/Sign out -> Pick an account -> **Use another account**
* `laura@xxxxxZZZZZZ.onmicrosoft.com` -> Next
* Ingresar password incorrecta al azar -> Sign in -> ⚠️ error de password inválida
* Repetir 2 veces más (3 intentos en total) -> debe aparecer mensaje de cuenta bloqueada
  * ⚠️ Si no bloquea al 3er intento, esperar unos minutos (la propagación del cambio puede tardar 5-10 min) y reintentar
* Esperar **90 segundos** (duración del lockout configurada)
* Reintentar login: `laura@xxxxxZZZZZZ.onmicrosoft.com` -> password real de Laura (New User Password)
  * Aparece **Let's keep your account secure** (MFA, Laura no está en el pilot project) -> confirma que el login con password correcta funcionó
  * ⚠️ No hace falta completar el MFA de Laura

## Cierre
* Esta es la última tarea que usa LON-DC1 en este exercise -> se pueden cerrar todas las aplicaciones abiertas
* Continúa en Lab 4 - Exercise 2

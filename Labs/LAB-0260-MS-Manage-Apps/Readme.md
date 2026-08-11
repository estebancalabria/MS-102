# LAB-0230-Manage-M365-Apps-Installation

## Task 1: Verificar efecto de la licencia (sin licencia)
* [WINDOWS] LON-CL1 -> Browser (Holly logueada)
* [MENU] Users -> Active users
  * [LINK] Add a user
    * First name : Laura / Last name : Atkins / Username : laura
    * ⚠️ Verificar dominio = **xxxxxZZZZZZ.onmicrosoft.com** (no el custom domain, aunque aparezca como default)
    * Password : New User Password / destildar "Require change at first sign-in"
    * [TAB] Assign product licenses -> **Create user without product license (not recommended)**
    * [TAB] Optional settings -> Next -> Review -> Finish adding

* [WINDOWS] LON-CL2 -> Ctrl+Alt+Del -> Switch user -> Other user
  * Login : `adatum\laura` / Pa55w.rd
* [WINDOWS] Edge
  * (primer uso) Start without your data -> Continue without this data -> destildar "Make Microsoft experience..." -> Confirm and start browsing
  * https://www.microsoft365.com -> login Laura@xxxxxZZZZZZ.onmicrosoft.com
  * Home M365: verificar que **NO** aparece la columna de íconos de apps (sin licencia)
  * [LINK] Install apps -> Microsoft 365 apps -> abre **My account**
    * [TAB] Office Apps & devices -> View apps & devices
    * ⚠️ Verificar mensaje: no puede instalar porque no tiene licencia con apps de Office
* Cerrar pestañas "My account" y "Welcome to Edge", dejar Home | Microsoft 365 abierta

## Task 2: Verificar efecto del global Office download setting
* [WINDOWS] LON-CL1 -> Browser (Holly)
* [MENU] Show all -> Settings -> Org Settings
  * [TAB] Services -> **Microsoft 365 installation options**
    * [TAB] Installation -> sección Apps for Windows and mobile devices
      * Destildar **Office (includes Skype for Business)** -> Save -> cerrar (X)

### Asignar licencia a Laura (liberando de Pradeep)
* [MENU] Active users -> **Pradeep Gupta**
  * [TAB] Licenses and apps -> destildar Microsoft 365 E5 (no Teams) + Microsoft Teams Enterprise -> Save changes -> cerrar
* [MENU] Active users -> **Laura Atkins**
  * [TAB] Licenses and apps -> tildar ambas licencias -> Save changes -> cerrar
  * Verificar columna Licenses de Laura ya no dice "Unlicensed"

### Probar con setting apagado (debería fallar igual)
* [WINDOWS] LON-CL2 -> Edge (Laura logueada) -> Refresh
* [LINK] Install apps -> Install Microsoft 365 apps -> My account -> View apps & devices
  * ⚠️ Verificar mensaje: "the admin has turned off Office installs"

### Reactivar el setting
* [WINDOWS] LON-CL1 -> Browser (Holly)
* [MENU] Org Settings -> Services -> Microsoft 365 installation options
  * [TAB] Installation -> tildar de nuevo **Office (includes Skype for Business)** -> Save -> cerrar

### Confirmar que ahora sí puede
* [WINDOWS] LON-CL2 -> Edge (Laura) -> Refresh
  * Verificar que aparece botón **Install Office** (hasta 5 PC/Mac, 5 tablets, 5 smartphones)
  * ⚠️ NO clickear Install Office todavía (se hace en el próximo task)

## Task 3: Instalación user-driven de M365 Apps
* [WINDOWS] LON-CL2 -> Edge (Laura, My account) -> **Install Office**
  * Si aparece "Just a few more steps" -> Close
* [WINDOWS] Downloads -> abrir **OfficeSetup.exe**
  * Si pide UAC : `adatum\administrator` / Pa55w.rd -> Yes
  * Si aparece "Continuing could be expensive" (puede estar en la taskbar) -> **Continue**
  * Esperar instalación -> **Close** en "You're all set!"

### Validar instalación
* [WINDOWS] Start menu -> verificar apps instaladas (Word, PowerPoint, Outlook, OneNote, Excel, etc.)
* [WINDOWS] Word
  * Sign in -> Laura@xxxxxZZZZZZ.onmicrosoft.com -> password -> Sign in
  * "Automatically sign in to all apps" -> **Yes, all apps** -> Done
  * Accept license agreement -> Close
  * Abrir doc en blanco, escribir texto, guardar en Documents
  * (Si aparece "Check out our new look" -> Not now)
  * Cerrar Word

## Cierre
* [WINDOWS] Edge -> ícono usuario Laura (LA) -> Sign out -> cerrar Edge
* [WINDOWS] Ctrl+Alt+Del -> Sign out
* Login : Other user -> `lon-cl2\Admin` / Pa55w.rd
* LON-CL2 queda listo para el próximo lab

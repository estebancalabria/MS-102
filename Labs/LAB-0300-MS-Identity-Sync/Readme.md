# LAB-0301-Prepare-and-Implement-Identity-Synchronization

Este lab prepara y luego implementa la sincronización de identidades entre Adatum on-premises y Microsoft Entra ID: se configura el UPN suffix, se simula y corrige un error de directorio, se instala Microsoft Entra Connect Sync, se generan cambios de prueba en usuarios y grupos, se fuerza una sincronización manual y se valida el resultado desde el admin center y PowerShell.

> ⚠️ Los Tasks 4 a 6 deben ejecutarse sin demora entre ellos, para que Microsoft Entra Connect Sync no sincronice automáticamente los cambios antes de forzar la sincronización manual en el Task 7.

## Task 1: Configurar el UPN suffix

> Se reemplaza el dominio adatum.com por el dominio custom del tenant en todas las cuentas, para que el UPN coincida con el dominio que se usará para el sign-in en Microsoft Entra ID.
* [WINDOWS] LON-DC1 -> `adatum\administrator` / Pa55w.rd
  * [APP] Abrir **Server Manager**
     * [MENU] Tools -> **Active Directory Users and Computers**
        * En el panel izquierdo, verificar que el dominio del Active Directory local sea **adatum.com**
        * Este es el dominio on-premises que se utilizará como referencia en los comandos de Active Directory.
  
* [BROWSER] Ir a entra Admin center (https://admin.cloud.microsoft/)
  * [MENU] Settings -> Domain
    * Copiar el nombre del dominio **<tennant_domain>**

* [WINDOWS] PowerShell (Run as administrator)
  * Reemplazar el dominio on-premises **adatum.com** por **<tennant_domain>**
```powershell
 Set-ADForest -identity adatum.com -UPNSuffixes @{replace="<tennant_domain>"}
```

* **[VERIFY]**
  * [WINDOWS] Server Manager -> Tools -> **Active Directory Users and Computers**
      * Seleccionar cualquier usuario del dominio -> **Properties**
        * [TAB] Account
             * En **User logon name**, abrir el desplegable del dominio
             * Verificar que aparezcan:
               * `@adatum.com`
               * `@<tennant_domain>`
             * Cerrar la ventana de propiedades sin realizar cambios

  * Actualizar el UPN de todas las cuentas existentes al nuevo dominio
```powershell
    Get-ADUser -Filter * | ForEach-Object { Set-ADUser $_  -UserPrincipalName ($_.SamAccountName + "@<tennant_domain>" )}
```
  * ⚠️ Reemplazar `xxxUPNxxx` y `xxxCustomDomainxxx.xxx` por los valores reales del tenant/hosting provider
  * Continuar en PowerShell para el siguiente task

* **[VERIFY]**
  * [WINDOWS] Server Manager -> Tools -> **Active Directory Users and Computers**
      * Seleccionar cualquier usuario del dominio -> **Properties**
        * [TAB] Account
             * En **User logon name**, verificar que el UPN sea `usuario@<tennant_domain>`
             * Verificar que ya no utilice `@adatum.com`
             * Cerrar la ventana de propiedades sin realizar cambios

---

## Task 2: Preparar para Instalar Microsoft Entra Connect Sync

*  Se instala y configura **Microsoft Entra Connect Sync** para habilitar la sincronización continua entre el AD on-premises y Microsoft Entra ID, y se revisa el resultado de la primera sincronización completa.
> ⚠️ Si hay una ventana de PowerShell abierta de un task anterior, **cerrarla antes de continuar** (el módulo ADSync se instala con Entra Connect; si PowerShell ya estaba abierto, el cmdlet `Start-ADSyncSyncCycle` del Task 7 no estará disponible)

* [WINDOWS] LON-DC1 -> `adatum\administrator` (ya logueado)
* [BROWSER] Loguearse en https://admin.cloud.microsoft/ con cuenta administrador
   * [MENU] Microsoft 365 admin center -> Users -> Active users -> ícono **···** -> **Directory synchronization**
     * Wizard **Add or sync users to Microsoft Entra ID**
       * [TAB] About user synchronization -> revisar cloud/hybrid users -> Next
       * [TAB] Select a migration option -> **Continuous sync** -> Next
       * [TAB] Prepare by running IdFix -> Next (ya se corrigieron errores en Task 3)
       * [TAB] Elegir **Microsoft Entra Connect Sync**
           * Esto abre una ventana nueva para descargar el Connect Sync -> Archivo AzureADConnect.exe de 115 MB
           * Ejecutar el archivo descargado

> Es un buen momento para explicarla diferenci entre Connect Sync y Cloud Sync
> En este laboratorio se elige **Microsoft Entra Connect Sync** porque el escenario requiere **Microsoft Entra Hybrid Join**, que necesita sincronizar objetos de dispositivo.

---

## Task 3: Instalar Microsoft Entra Connect Sync en el DS
     
* [WINDOWS] Instalacion **Microsoft Entra Connect Sync**
   * Welcome -> tildar **I agree to the license terms and privacy notice** -> Continue
   * Express Settings -> **Use express settings**
   * Connect to Microsoft Entra ID -> Username: <USUARIO ADMINISTRADOR GLOBAL ADMINISTRATOR< -> Next -> Sign in (password)
   * Connect to AD DS -> Username: `Adatum\Administrator` / Password: `Pa55w.rd` -> Next (tab fuera del campo password si Next no habilita)
   * Microsoft Entra sign-in configuration -> tildar **Continue without matching all UPN suffixes to verified domains** -> Next
   * Ready to configure -> tildar **Start the synchronization process when configuration completes** -> Install

> ⚠️ NO tildar **Exchange hybrid deployment** (no corresponde en este lab)

   * Esperar -> Configuration complete -> Exit

---

## Task 4 : Verificar la sincronizacion

> [!WARN]
> ⚠️ Si "Azure AD Connect" no expande en el Start menu -> reiniciar LON-DC1, volver a loguear `Adatum\Administrator`/Pa55w.rd, abrir Edge -> `https://portal.office.com` -> login Holly -> Admin -> reintentar abrir Synchronization Service

* [WINDOWS] Start -> Azure AD Connect -> **Synchronization Service**
  * [TAB] Operations -> esperar export profile de **<tenant_domain> - AAD** -> status **completed-export-errors** -> seleccionar la fila
     * Panel **Export Statistics** -> ver usuarios agregados/actualizados
     * Panel **Export Errors** -> abrir los 2 links **DataValidationFailed** -> confirmar que corresponden a **Ngoc Bich Tran** y **An Dung Dao** (Export Error tab -> Detail -> Close -> Close)
      
* **[VERIFY]**
  * En **Export Statistics**, identificar un usuario con resultado **Added**
  * Copiar el nombre del usuario
  * [BROWSER] Microsoft 365 admin center -> **Users -> Active users**
    * Buscar el usuario
    * Verificar que el usuario sincronizado aparezca en Microsoft Entra ID
    * Abrir el usuario
      * Verificar que el nombre y el UPN correspondan al usuario de Active Directory

> [!WARN]
> ⚠️ Esta primera sync fue **Full Synchronization**; las siguientes (cada 30 min) serán **Delta Synchronization**

---

## Task 5: Crear cuentas de grupo para probar la sincronización en grupos Built-IN

> Se crean/modifican grupos on-premises (un built-in y uno nuevo) para verificar más adelante cuáles sincronizan a Microsoft 365 y cuáles no.
* [WINDOWS] LON-DC1 -> `Administrator` (ya logueado)
  * [MENU] Server Manager -> Tools -> **Active Directory Users and Computers**
    * [TREEVIEW] -> Adatum.com -> carpeta **Builtin** -> doble click **Print Operators**
      * [TAB] Members -> Add -> escribir `Ashlee Pickett; Juanita Cook; Morgan Brooks` -> Check Names -> OK -> OK

 > [!WARN]
> ⚠️ Los grupos built-in **NO** se sincronizan a Microsoft 365, aunque se les agreguen miembros (se validará en Task 8)

---

## Task 6 : Crear un grupo de seguridad sincronizable

Se crea el grupo Manufacturing dentro de la OU Research, configurándolo como grupo de seguridad universal y mail-enabled para que pueda sincronizarse con Microsoft Entra ID.

* [TREEVIEW] -> Adatum.com -> OU **Research** -> click derecho -> New -> Group
   * Group name: `Manufacturing`
   * Group scope: `Universal`
   * Group type: `Security` -> OK
     
* OU **Research** -> doble click **Manufacturing**
  * Campo **E-mail**: `manufacturing@adatum.com` (esto hace que sincronice como **mail-enabled security group**)
  * [TAB] Members -> Add -> `Bernardo Rutter; Charlie Miller; Dawn Williamson` -> Check Names -> OK -> OK

---

## Task 7: Cambiar la pertenencia de un grupo para probar la sincronización

> Se remueven miembros del grupo **Research** on-premises, para confirmar después que la baja también se refleja en Microsoft 365 tras la sincronización.
* [WINDOWS] LON-DC1 -> Active Directory Users and Computers (continúa abierto)
   * OU **Research** -> doble click grupo **Research**
       * [TAB] Members -> seleccionar `Cai Chu`, `Shannon Booth`, `Tia Zecirevic` (Ctrl+click) -> **Remove** -> Yes -> verificar que ya no aparecen -> OK


> [!WARN]
> ⚠️ Continuar de inmediato con el Task 7 para que Entra Connect Sync no sincronice automáticamente estos cambios antes de forzar la sync manual

---

## Task 8: Forzar una sincronización manual

Se ejecuta desde PowerShell un ciclo de sincronización delta para aplicar de inmediato los cambios de usuarios y grupos, sin esperar los 30 minutos del ciclo automático.

* [WINDOWS] Start -> click derecho -> **Windows PowerShell (Admin)**
  * Forzar sync delta

```powershell
    Start-ADSyncSyncCycle -PolicyType Delta
```

> [!WARN]
> ⚠️ Si da error, verificar que el servicio **Microsoft Azure AD Sync** esté iniciado (puede haberse detenido si se reinició la VM) e intentar de nuevo

> [!WARN]
>  ⚠️ Si el cmdlet no se reconoce, reiniciar LON-DC1 para que termine de instalarse el módulo

 * Esperar a que termine -> minimizar PowerShell (no cerrar)


---

## Task 9: Validar los resultados de la sincronización de directorio

Se valida en el Microsoft 365 admin center y por PowerShell que los cambios de grupos y usuarios se sincronizaron correctamente desde on-premises.

* **[VERIFY]**
 * [BROWSER] Edge -> pestañas **Home | Microsoft 365** / **Active users**
 * [MENU] Microsoft 365 admin center -> Teams & groups -> Active teams & groups
   * [TAB] Security groups
     * Verificar que **Print Operators** **NO** aparece (built-in, no sincroniza)
     * Verificar que **Manufacturing** sí aparece (⚠️ puede tardar ~10 min, refrescar)
       * Columna **Email**: debe mostrar `manufacturing<tenant_domain>` (cambiado desde `manufacturing@adatum.com` durante la sync)
       * Columna **Sync status** -> hover -> **Synced from on-premises**
       * Ícono **···** -> hover -> mensaje indicando que solo se administra desde on-premises

* **[VERIFY]**
  * [BROWSER] Microsoft 365 admin center -> Teams & groups -> **Active teams & groups**
    * [TAB] Security groups -> buscar y abrir **Research**
      * [TAB] Members
        * Verificar que **NO** estén:
          * `Cai Chu`
          * `Shannon Booth`
          * `Tia Zecirevic`
---

# Anexo - Validar grupos sincronizados mediante Microsoft Graph PowerShell

> [!WARN]
> Este anexo requiere  Powershell 7
> Instalar Powershell 7 de  https://github.com/PowerShell/PowerShell/releases/download/v7.6.5/PowerShell-7.6.5-win-x64.msi
     
* [WINDOWS] PowerShell (Run as administrator)
  A* Instalar submódulos de Graph necesarios (Yes to All si pide confirmar repositorio no confiable)
   
```powershell
    Install-Module Microsoft.Graph.Groups
    Install-Module Microsoft.Graph.Users
```

  * Conectar con permisos de solo lectura
    
```powershell
    Connect-MgGraph -Scopes 'Group.Read.All', 'User.Read.All'
```
    * Seleccionar cuenta de Administrador -> password -> Sign in
    * Si aparece **Permissions requested** -> tildar **Consent on behalf of your organization** -> Accept

  * Listar grupos
    
```powershell
    Get-MgGroup | Sort-Object DisplayName | Format-Table Id, DisplayName, Description, GroupTypes
```

  * Copiar el **object ID** del grupo **Research** -> ver sus miembros con nombre
 
```powershell
    Get-MgGroupMember -GroupId 'object ID de Research' -All | ForEach {Get-MgUser -UserId $_.Id}
```
  * Verificar que **NO** están: Cai Chu, Shannon Booth, Tai Zecirevic
  
  * Copiar el **object ID** del grupo **Manufacturing** -> reemplazar el ID en el comando anterior (flecha arriba, pegar) -> ver sus miembros
    
```powershell
    Get-MgGroupMember -GroupId 'object ID de Manufacturing' -All | ForEach {Get-MgUser -UserId $_.Id}
```
    * Verificar que **SÍ** están: Bernardo Rutter, Charlie Miller, Dawn Williamson

---

# FIN del LAB

---

# Anexo - Troubleshooting de Problemas

## Task 1: Preparar cuentas de usuario con problemas (simular error)
> Se corre un script que rompe intencionalmente el userPrincipalName de un usuario, para luego practicar cómo detectar y corregir ese tipo de error antes de sincronizar.
* [WINDOWS] LON-DC1 -> PowerShell
  * Cambiar al directorio de labfiles
```cmd
    CD C:\labfiles\
```
  * Ejecutar script que rompe intencionalmente una cuenta (Klemen Sic)
```powershell
    .\CreateProblemUsers.ps1
```
  * ⚠️ Esperar a que termine el script antes de continuar
  * El script agrega un `@` extra al **userPrincipalName** de **Klemen Sic**
* Minimizar PowerShell

## Task 2: Identificar y corregir errores de directorio
> Se busca la cuenta con el UPN malformado y se corrige, ya sea por PowerShell o por Active Directory Users and Computers, dejando el resto de errores preexistentes intactos para validarlos más adelante durante la sincronización.
* [WINDOWS] LON-DC1 -> `Administrator` (ya logueado)
* [WINDOWS] PowerShell (abrir si no está abierto, Run as administrator)
* Buscar usuarios con doble `@@` en el UPN
```powershell
  Get-ADUser -Filter * -Properties UserPrincipalName | Where-Object { $_.UserPrincipalName -like "*@@*" } | Format-Table Name, SamAccountName, UserPrincipalName
```
  * Debe listar solo a **Klemen Sic** con su UPN malformado
* Elegir **una** de las dos opciones para corregirlo:

### Opción A - Corregir con PowerShell

* Reconstruir el UPN de Klemen a partir de su SamAccountName
```powershell
  Get-ADUser -Filter * -Properties UserPrincipalName | Where-Object { $_.UserPrincipalName -like "*@@*" } | ForEach-Object { Set-ADUser $_ -UserPrincipalName ($_.SamAccountName + "@xxxUPNxxx.xxxCustomDomainxxx.xxx") }
```
* Volver a correr el comando de búsqueda del paso anterior -> no debe devolver resultados
* Saltar Opción B

### Opción B - Corregir con Active Directory Users and Computers

* [MENU] Server Manager -> Tools -> **Active Directory Users and Computers**
* [MENU] View -> verificar/tildar **Advanced Features** (habilita la pestaña Attribute Editor)
* Click derecho en **adatum.com** -> **Find** -> Name: `Klemen` -> Find Now -> doble click en **Klemen Sic**
* [TAB] Attribute Editor -> localizar **userPrincipalName** -> confirmar que contiene `@@`
* Seleccionar **userPrincipalName** -> Edit -> quitar el `@` extra (dejar un solo `@`) -> OK
* OK para cerrar la ventana de propiedades -> cerrar Active Directory Users and Computers
* ⚠️ **An Dung Dao** y **Ngoc Bich Tran** tienen errores de directorio preexistentes -> **dejarlos sin corregir** (se usarán más adelante para ver cómo Microsoft Entra Connect Sync reporta errores no resueltos)


## * Fin del lab

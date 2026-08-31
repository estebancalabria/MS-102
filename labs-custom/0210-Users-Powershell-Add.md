# LAB — Crear usuarios de Microsoft 365 con PowerShell

## Objetivo

En este laboratorio vamos a utilizar **Microsoft Graph PowerShell** para conectarnos a Microsoft Entra ID y crear usuarios de Microsoft 365 mediante PowerShell.

---

## 1. Instalar Microsoft Graph PowerShell

* **[WINDOWS]** Abrir **PowerShell 7**.
* Ejecutar:

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
```

* Si aparece el mensaje solicitando confirmar la instalación desde PowerShell Gallery, seleccionar:

```text
Y
```

---

## 2. Importar el módulo

* Ejecutar:

```powershell
Import-Module Microsoft.Graph
```

* Verificar que el módulo esté disponible:

```powershell
Get-Module Microsoft.Graph
```

---

## 3. Conectarse a Microsoft Entra ID

* Ejecutar:

```powershell
Connect-MgGraph -Scopes "User.ReadWrite.All"
```

* Iniciar sesión con la cuenta de administrador del tenant.

* Si aparece una ventana solicitando permisos, aceptar.

---

## 4. Verificar la conexión

* Ejecutar:

```powershell
Get-MgContext
```

* Verificar que se muestre información similar a:

```text
Account
TenantId
Scopes
```

El usuario conectado debe tener permisos suficientes para crear usuarios.

---

## 5. Consultar los usuarios existentes

* Ejecutar:

```powershell
Get-MgUser -All
```

* Para mostrar solamente información relevante:

```powershell
Get-MgUser -All |
    Select-Object DisplayName, UserPrincipalName, AccountEnabled
```

---

## 6. Crear un usuario

* Definir el perfil de contraseña:

```powershell
$PasswordProfile = @{
    Password = "Pa55w.rd123!"
    ForceChangePasswordNextSignIn = $true
}
```

* Crear el usuario:

```powershell
New-MgUser `
    -DisplayName "Juan Pérez" `
    -GivenName "Juan" `
    -Surname "Pérez" `
    -UserPrincipalName "juan.perez@wwlx422640.onmicrosoft.com" `
    -MailNickname "juan.perez" `
    -AccountEnabled `
    -PasswordProfile $PasswordProfile
```

> Reemplazar `wwlx422640.onmicrosoft.com` por el dominio del tenant utilizado en el laboratorio.

---

## 7. Verificar el usuario creado

* Ejecutar:

```powershell
Get-MgUser -UserId "juan.perez@wwlx422640.onmicrosoft.com"
```

* También podemos mostrar los datos principales:

```powershell
Get-MgUser -UserId "juan.perez@wwlx422640.onmicrosoft.com" |
    Select-Object DisplayName, GivenName, Surname, UserPrincipalName, AccountEnabled
```

Resultado esperado:

```text
DisplayName       : Juan Pérez
GivenName         : Juan
Surname           : Pérez
UserPrincipalName : juan.perez@wwlx422640.onmicrosoft.com
AccountEnabled    : True
```

---

## 8. Crear varios usuarios

* Crear una lista de usuarios:

```powershell
$Users = @(
    @{
        FirstName = "Ana"
        LastName  = "García"
        Username  = "ana.garcia"
    },
    @{
        FirstName = "Pedro"
        LastName  = "López"
        Username  = "pedro.lopez"
    },
    @{
        FirstName = "Laura"
        LastName  = "Martínez"
        Username  = "laura.martinez"
    }
)
```

* Ejecutar el siguiente script:

```powershell
foreach ($User in $Users) {

    $PasswordProfile = @{
        Password = "Pa55w.rd123!"
        ForceChangePasswordNextSignIn = $true
    }

    New-MgUser `
        -DisplayName "$($User.FirstName) $($User.LastName)" `
        -GivenName $User.FirstName `
        -Surname $User.LastName `
        -UserPrincipalName "$($User.Username)@wwlx422640.onmicrosoft.com" `
        -MailNickname $User.Username `
        -AccountEnabled `
        -PasswordProfile $PasswordProfile
}
```

> Reemplazar el dominio por el dominio del tenant utilizado en el laboratorio.

---

## 9. Comprobar los usuarios

* Ejecutar:

```powershell
Get-MgUser -All |
    Select-Object DisplayName, UserPrincipalName, AccountEnabled |
    Format-Table
```

Deberían aparecer los usuarios creados durante el laboratorio.

---

## 10. Desconectarse de Microsoft Graph

* Ejecutar:

```powershell
Disconnect-MgGraph
```

---

# Resultado esperado

Al finalizar el laboratorio, el alumno habrá aprendido a:

* Instalar **Microsoft Graph PowerShell**.
* Importar el módulo de Microsoft Graph.
* Autenticarse contra **Microsoft Entra ID**.
* Consultar usuarios de Microsoft 365.
* Crear un usuario mediante PowerShell.
* Crear múltiples usuarios mediante un script.
* Verificar los usuarios creados.
* Desconectarse de Microsoft Graph.

## Comandos utilizados

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser

Import-Module Microsoft.Graph

Connect-MgGraph -Scopes "User.ReadWrite.All"

Get-MgContext

Get-MgUser -All

New-MgUser

Disconnect-MgGraph
```

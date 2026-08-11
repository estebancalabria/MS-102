# LAB-0140-Custom-Domain

## Crear zona DNS on-premises
* [WINDOWS] LON-DC1 -> login Administrator / Pa55w.rd
* [WINDOWS] Powershell (Run as administrator)
```powershell
dnscmd /zoneadd xxxUPNxxx.xxxCustomDomainxxx.xxx /DsPrimary
```
* Minimizar Powershell (no cerrar)

## Agregar el dominio en M365
* [WINDOWS] Browser -> https://admin.microsoft.com -> login Holly
* [MENU] Show all -> Settings -> Domains
  * [LINK] + Add domain
    * Domain name : xxxUPNxxx.xxxCustomDomainxxx.xxx
    * Use this domain
* Verify ownership -> método **TXT record**
  * Copiar el **TXT value** (MS=msXXXXXXXX)
  * ⚠️ NO tocar el botón Verify todavía

## Crear el TXT de verificación en DNS Manager
* [WINDOWS] Server Manager
  * [MENU] Tools -> DNS
* [WINDOWS] DNS Manager
  * Forward Lookup Zones -> zona **xxxUPNxxx.xxxCustomDomainxxx.xxx**
  * Click derecho -> Other New Records... -> Text (TXT) -> Create Record
    * Record name : (vacío)
    * Text : pegar el TXT value copiado
* [WINDOWS] Browser -> click en botón **Verify**
> [!NOTE]
> Puede tardar 5-10 min en propagar. Si falla, esperar y click en "Try again"

## Agregar registros DNS del servicio Exchange
* [WINDOWS] Browser (misma pestaña, tras el Verify exitoso aparece la página **Add DNS records**)
  * Sección **Exchange and Exchange Online Protection** (única tildada, no tocar Skype/Intune)
  * Expandir las 3 subsecciones (flecha >): MX Records, CNAME Records, TXT Records
* MX Record
  * [WINDOWS] Browser -> copiar expected value (ej: xxxUPNxxx-xxxCustomDomainxxx-xxx.mail.protection.outlook.com)
  * [WINDOWS] DNS Manager
    * Click derecho en la zona -> New Mail Exchanger (MX)...
      * Host or child domain : (vacío)
      * FQDN mail server : pegar
  * [WINDOWS] Browser -> Continue -> verificar check verde en MX
* CNAME Record
  * [WINDOWS] Browser -> copiar expected value (ej: autodiscover.outlook.com)
  * ⚠️ NO usar el Host Name sugerido (autodiscover.xxxUPNxxx), usar solo **autodiscover**
  * [WINDOWS] DNS Manager
    * Click derecho -> New Alias (CNAME)...
      * Alias name : autodiscover
      * FQDN target host : pegar
  * [WINDOWS] Browser -> Continue -> verificar check verde en CNAME
* TXT Record (SPF)
  * [WINDOWS] Browser -> copiar expected TXT value (ej: v=spf1 include:spf.protection.outlook.com -all)
  * [WINDOWS] DNS Manager
    * Click derecho -> Other New Records... -> Text (TXT) -> Create Record
      * Record name : (vacío)
      * Text : pegar
  * [WINDOWS] Browser -> Continue

## Finalizar
* Si los 3 records validan -> **Domain setup is complete** -> Done
* [MENU] Domains -> verificar status **Healthy** para el nuevo dominio
* ⚠️ El nuevo dominio queda como default -> volver a marcar **xxxxxZZZZZZ.onmicrosoft.com** como default (Holly todavía no quiere migrar)
* Dejar LON-DC1 abierto (Edge + Powershell) para el lab de sincronización de identidad

## Verificación (opcional)
> [!NOTE]
> El dominio nuevo solo resuelve en DNS interno del tenant, no en internet público. No sirve mandar un mail real desde afuera; se prueba mandando un mail dentro del tenant.

* [MENU] Active users -> Holly Dickson -> Manage username
  * Cambiar sufijo a **Holly@xxxUPNxxx.xxxCustomDomainxxx.xxx**
* [WINDOWS] Browser -> Outlook web -> login como Holly (nueva dirección)
  * Redactar mail nuevo -> Para: la misma dirección de Holly -> Enviar
  * Verificar que llega a la bandeja de entrada
* Opcional: abrir el mail -> **...** -> **View message source**
  * Confirmar que pasó por `mail.protection.outlook.com` (el MX configurado)

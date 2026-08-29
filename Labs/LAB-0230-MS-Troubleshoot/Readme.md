# LAB-0220-Monitor-Troubleshoot-M365

## Test 1: Enviar mail a dominio inválido
* [WINDOWS] LON-CL1 -> Browser -> Home M365 (logueado como Holly)
* [MENU] Apps -> Outlook
* [WINDOWS] Outlook (Holly)
  * New mail
    * To : user@alt.none -> Use this address
    * Subject : Testing invalid domain
    * Send
  * Esperar NDR (non-delivery report) en el Inbox -> abrir en ventana nueva
  * Copiar el texto desde **"Original message headers"** hasta el final -> Ctrl+C

## Analizar el header (dominio inválido)
* [WINDOWS] Browser -> nueva pestaña -> https://testconnectivity.microsoft.com
* [MENU] Message Analyzer
  * Pegar el diagnóstico copiado -> **Analyze headers**
  * Revisar secciones: Summary / Received headers / Other headers
  * Problema esperado (Other headers, Hop 1): dominio **@alt.none** no existe (DNS inválido)
* Clear (resetear el analyzer)

## Test 2: Enviar mail a mailbox inexistente
* [WINDOWS] Browser -> volver a pestaña Outlook (Holly)
  * New mail
    * To : nnnnnnnnTuNombre@outlook.com (random) -> Use this address
    * Subject : Testing invalid mailbox
    * Send
  * Esperar NDR -> abrir en ventana nueva
  > [!NOTE]
  > Si no llega NDR en ~1 min, probar con otra dirección random (puede que ese mailbox exista)
  * Copiar el texto desde **"Diagnostic information for administrators"** hasta el final -> Ctrl+C

## Analizar el header (mailbox inválido)
* [WINDOWS] Browser -> pestaña Message Header Analyzer
  * Pegar diagnóstico -> Analyze headers
  * Buscar en el texto pegado (no siempre aparece en Other headers): `550 5.5.0 Requested action not taken: mailbox unavailable`
* Cerrar pestañas de Message Header Analyzer y Remote Connectivity Analyzer

## Message trace en Exchange admin center
* [WINDOWS] Browser -> pestaña admin center
* [MENU] Show all -> Admin centers -> Exchange
* [WINDOWS] Exchange admin center (nueva pestaña)
* [MENU] Mail flow -> Message trace
  * [TAB] Default queries -> **+Start a trace**
    * Senders : Holly Dickson
    * Recipients : All (default)
    * Time range : slider -> 1 day
    * Detailed search options -> Delivery status : **Failed**
    * Report type : Summary report (default)
    * Search
  * Resultados: deberían aparecer los 2 mails fallidos (alt.none y outlook.com)
  > [!NOTE]
  > El mail a outlook.com puede no figurar como Failed si el server remoto lo marcó como delivered
  * Click en fecha/hora de cada mensaje -> revisar sender/recipient/status/error + "How to fix it"
    * Expandir Message events / More information
  * Volver a Message trace (breadcrumb superior)
* Cerrar pestaña de Outlook (dejar el resto abierto)

## Revisar Service Health
* [WINDOWS] Browser -> pestaña admin center
* [MENU] Health -> Service health
  * [TAB] Overview (default)
  * [TAB] Issue history
    * Filtro default: últimos 7 días
    * Click en Title de un incidente -> revisar detalle -> cerrar

## Revisar Reports (Usage)
* [MENU] Reports -> Usage
  * Ver charts: **Active users - Microsoft 365 Services** y **Email activity**
  > [!NOTE]
  > Puede haber poca data por uso limitado del lab
  * Email activity -> **View more** -> abre Exchange report dashboard
    * [TAB] Email activity (default) -> [TAB] Mailbox usage
      * Cambiar rango (Past 30 days -> 7/90/180 días) para ver cómo cambia
      * Scroll abajo: detalle de mailbox por usuario
  * Breadcrumb -> Usage -> volver a Usage Overview, repasar otros reports disponibles

## Reports en Exchange admin center
* [WINDOWS] Browser -> pestaña Exchange admin center
* [MENU] Reports -> Mail flow
  * **Inbound messages report** (el único con data) -> revisar
  * Breadcrumb -> Mail flow -> repasar el resto de los reports disponibles
* Cerrar pestaña Exchange admin center

## Enviar un caso a Microsoft Support (sin completarlo)
* [WINDOWS] Browser -> pestaña admin center
* [MENU] Support -> View service requests
  * Verificar que no hay tickets abiertos
* [MENU] Support -> Help & Support
  * Campo Message : "Can't install Office" -> flecha
  * Revisar artículos recomendados -> abrir uno, revisar, cerrar pestaña
  * Ícono headset (del medio) -> abre **Contact support**
    * ⚠️ NO completar el formulario ni enviar (dispara un llamado real de soporte)
    * Solo revisar los campos -> cerrar con la **X**

## Cierre
* Dejar LON-CL1 y Edge abiertos para el próximo ejercicio

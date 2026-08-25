# Lab: Asignar licencias a un grupo (Group-based licensing) — MS-102

**Objetivo:** Crear un grupo de seguridad y asignarle una licencia (Office 365 E3), desactivando un service plan específico dentro de ella.

**Duración estimada:** 15 minutos

**Prerrequisitos:**
- Acceso al Microsoft Entra admin center con rol de Administrador de usuarios o Administrador global
- Al menos una licencia disponible de Office 365 E3 en el tenant (puede ser licencia de prueba)
- 1-2 usuarios de prueba ya creados

---

## Parte 1 — Crear el grupo

1. [BROWSER] Ingresá a **https://entra.microsoft.com** con tu cuenta de administrador.
2. [MENU] Navegá a **Identity** > **Groups** > **All groups**.
3. [TAB] Hacé clic en **New group**.
4. [DIALOG] Completá:
   - **Group type**: Security
   - **Group name**: `All-Users-Baseline-License`
   - **Membership type**: Assigned (para este lab alcanza con agregar los usuarios manualmente)
5. [TAB] En **Members**, seleccioná tus usuarios de prueba.
6. [BROWSER] Hacé clic en **Create**.

---

## Parte 2 — Asignar la primera licencia (Office 365 E3)

1. [MENU] Abrí el grupo `All-Users-Baseline-License` que acabás de crear.
2. [MENU] En el panel izquierdo del grupo, hacé clic en **Licenses**.
3. [TAB] Hacé clic en **+ Assign licenses** (o **Assignments** > **Add**, según la versión del portal).
4. [DIALOG] En la lista de productos, marcá el checkbox de **Office 365 E3**.
5. [LINK] Hacé clic en **Options**, al lado del producto seleccionado — se despliega la lista de service plans incluidos.
6. [DIALOG] Desmarcá el service plan **Power Automate**, dejando el resto activado.
7. [BROWSER] Hacé clic en **Save**.

---

## Parte 3 — Verificar la asignación

1. [MENU] En el grupo, andá a **Licenses** > **Assignments**.
2. Confirmá que aparece la licencia **Office 365 E3**.
3. [TAB] Hacé clic en ella para revisar que los service plans estén como corresponde (Power Automate desactivado).
4. [MENU] Navegá a **Identity** > **Users** > selecciona uno de tus usuarios de prueba > **Licenses**.
5. Confirmá que el usuario recibió la licencia de forma automática por pertenecer al grupo (puede tardar unos minutos en procesarse).

---

## Limpieza (opcional)

1. [MENU] Abrí el grupo `All-Users-Baseline-License` > **Licenses** > **Assignments** > quitá la licencia asignada.
2. [MENU] Eliminá el grupo desde **All groups** > seleccionar grupo > **Delete**.

---

## Puntos clave para el examen

- Las licencias se asignan a grupos desde **Identity > Groups > [grupo] > Licenses**, no desde el M365 admin center clásico.
- Un mismo grupo puede tener **varias licencias apiladas** (no hace falta un grupo por producto).
- Dentro de cada licencia se pueden **desactivar service plans individuales** sin necesidad de un grupo aparte.
- Solo funciona con grupos de tipo **Security** o **Microsoft 365** (no con grupos de distribución).
- Funciona tanto con grupos **asignados** como **dinámicos**.
- Requiere licencia **Entra ID P1** para usar con grupos dinámicos (no así con grupos asignados manualmente).

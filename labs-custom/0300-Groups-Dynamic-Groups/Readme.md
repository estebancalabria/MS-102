# Lab: Grupos dinámicos en Microsoft Entra ID (MS-102)

**Objetivo:** Crear un grupo dinámico de seguridad que incluya automáticamente a todos los usuarios cuyo puesto (Job Title) sea "Support Engineer" y cuyo departamento contenga la palabra "Support".

**Duración estimada:** 20-25 minutos

**Prerrequisitos:**
- Suscripción de Microsoft 365 con rol de Administrador de usuarios o Administrador global
- Licencia Microsoft Entra ID P1 o P2 (los grupos dinámicos requieren licenciamiento premium)
- Al menos 3 usuarios de prueba con distintos valores de `jobTitle` y `department`

---

## Parte 1 — Crear usuarios de prueba (si no existen)

1. [BROWSER] Ingresá a **https://entra.microsoft.com** con tu cuenta de administrador.
2. [MENU] En el panel izquierdo, navegá a **Identity** > **Users** > **All users**.
3. [TAB] Hacé clic en **New user** > **Create new user**.
4. [DIALOG] Completá los campos básicos (nombre, usuario) y en la pestaña **Job info** completá `Job title` y `Department`:
   - User1 → Job title: `Support Engineer`, Department: `IT support`
   - User2 → Job title: `Support Engineer`, Department: `SupportCore`
   - User3 → Job title: `Systems Engineer`, Department: `IT support`
5. [BROWSER] Confirmá la creación de cada usuario y esperá a que aparezcan en la lista de **All users** (puede tardar unos minutos en propagarse).

---

## Parte 2 — Crear el grupo dinámico

1. [MENU] Navegá a **Identity** > **Groups** > **All groups**.
2. [TAB] Hacé clic en **New group**.
3. [DIALOG] Completá:
   - **Group type**: Security
   - **Group name**: `Support-Engineers-Dynamic`
   - **Membership type**: **Dynamic User** (no "Assigned")
4. [LINK] Hacé clic en **Add dynamic query** — esto abre el editor de reglas.

---

## Parte 3 — Configurar la regla de membresía

1. [DIALOG] En el editor de reglas, elegí la opción de **Edit** para escribir la sintaxis directamente (en vez de usar los menús desplegables).
2. Ingresá la siguiente regla:

```
(user.jobTitle -eq "Support Engineer") and (user.department -contains "Support")
```

3. [BROWSER] Hacé clic en **Validate Rule (Preview)** en la parte inferior del editor.
4. [DIALOG] Seleccioná los usuarios de prueba (User1, User2, User3) y hacé clic en **Validate**.
5. Verificá el resultado esperado:

| Usuario | jobTitle | department | ¿Cumple la regla? |
|---|---|---|---|
| User1 | Support Engineer | IT support | ✅ Sí |
| User2 | Support Engineer | SupportCore | ✅ Sí |
| User3 | Systems Engineer | IT support | ❌ No |

6. [BROWSER] Hacé clic en **Save** para guardar la regla.
7. [TAB] Volvé a la pestaña principal y hacé clic en **Create** para crear el grupo.

---

## Parte 4 — Verificar la membresía

1. [MENU] Navegá a **Identity** > **Groups** > **All groups** y abrí `Support-Engineers-Dynamic`.
2. [TAB] Hacé clic en **Members**.
3. Confirmá que aparecen únicamente User1 y User2 (la evaluación de reglas dinámicas puede tardar hasta 24 horas en producción, aunque en tenants de prueba suele ser casi inmediata).

---

## Limpieza (opcional)

1. [MENU] Eliminá el grupo `Support-Engineers-Dynamic` desde **All groups** > seleccionar grupo > **Delete**.
2. [MENU] Eliminá los usuarios de prueba desde **All users** si ya no los necesitás.

---

## Puntos clave para el examen

- Los grupos dinámicos requieren licencia **Entra ID P1/P2**.
- `-eq` compara igualdad exacta; `-contains` evalúa si el string incluye una subcadena en cualquier posición.
- Las reglas se combinan con `and` / `or`, y se pueden anidar con paréntesis.
- Además de `userType`, se pueden usar otros atributos como `jobTitle`, `department`, `country`, `companyName`, `extensionAttribute1-15`, etc.
- La membresía se recalcula automáticamente; no se puede agregar ni quitar usuarios manualmente en un grupo dinámico.

## Lab: Delegar administración regional con un Administrative Unit

**Objetivo:** Crear un AU, agregarle miembros y asignar un rol scoped, para practicar el flujo completo de least privilege delegation.

**Prerrequisitos:**
- Cuenta con rol Global Administrator o Privileged Role Administrator
- Al menos 2 usuarios de prueba en el tenant (ej: uno "Argentina", uno "Chile")

---

### Parte 1 — Crear el Administrative Unit

```
[BROWSER] https://entra.microsoft.com

[MENU] Identity → Roles & admins → Admin units
[ITEM] + Add
[CAMPO] Name: "AU-Sucursal-Chile"
[CAMPO] Description: "Usuarios de la oficina de Chile"
[BOTÓN] Review + create
```

👁️ -> Verificar que el AU aparece en el listado

---

### Parte 2 — Agregar miembros al AU

```
👁️ -> Abrir "AU-Sucursal-Chile"
[MENU] Users
[ITEM] Add members
👁️ -> Seleccionar los usuarios de prueba de Chile
[BOTÓN] Select
```

👁️ -> Confirmar que los usuarios aparecen listados dentro del AU

---

### Parte 3 — Asignar un rol scoped al AU

```
[MENU] Identity → Roles & admins → Roles & admins
👁️ -> Buscar "Helpdesk Administrator"
[ITEM] Add assignments
[SELECCIONAR] Member: [usuario admin de prueba]
[SELECCIONAR] Scope type: Administrative unit
[SELECCIONAR] Administrative unit: "AU-Sucursal-Chile"
[BOTÓN] Assign
```

---

### Parte 4 — Validar el alcance

```
👁️ -> Loguearse como el usuario con el rol asignado
[MENU] Users → All users
```

**Resultado esperado:** el admin scoped solo puede ver/administrar (resetear contraseña, bloquear sign-in) a los usuarios dentro de "AU-Sucursal-Chile". Al buscar un usuario fuera del AU, no debería poder gestionarlo.


---

**Punto de discusión para cerrar el lab:** comparar qué pasaría si el mismo rol se hubiera asignado con Scope type = "Directory" (tenant completo) en vez de "Administrative unit" — ahí se nota el contraste directo con least privilege.

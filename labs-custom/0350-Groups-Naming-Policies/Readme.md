# Laboratorio rápido: Configurar una Group Naming Policy

**Objetivo:** Configurar una política de nombres para Microsoft 365 Groups y bloquear palabras reservadas. 【1-58adad】

**Duración:** 5 minutos

---

## Tarea 1 - Configurar una Naming Policy

1. Abrir Microsoft Entra Admin Center.
2. Navegar a:

   Identity → Groups → Naming policy

3. Configurar una política de prefijo:

```text
[Department]-[GroupName]
```

Ejemplos esperados:

```text
IT-Projects
HR-Recruiting
Finance-Budget
```

La Naming Policy aplica automáticamente el prefijo o sufijo al nombre y alias del grupo. 【1-58adad】

---

## Tarea 2 - Configurar palabras bloqueadas

En **Custom blocked words**, agregar:

```text
CEO
Executive
Admin
Global
```

Guardar la configuración.

Microsoft permite impedir el uso de palabras específicas en nombres y alias de grupos. 【1-58adad】

---

## Tarea 3 - Validar la política

1. Ir al Microsoft 365 Admin Center.
2. Crear un nuevo Microsoft 365 Group.
3. Intentar utilizar el siguiente nombre:

```text
CEO Team
```

### Resultado esperado

✅ El sistema impide la creación del grupo porque contiene una palabra bloqueada.

---

## Tarea 4 - Crear un grupo válido

Intentar crear un grupo con el siguiente nombre:

```text
Projects
```

### Resultado esperado

✅ El grupo se crea respetando la Naming Policy configurada.

---

## Verificación

Comprobar que:

- Existe una Naming Policy configurada.
- La palabra "CEO" está bloqueada.
- Un grupo válido puede crearse correctamente.
- El nombre final cumple la convención establecida.

---

## Knowledge Check

**A company wants all Microsoft 365 Groups to automatically include the department name. What should be configured?**

- A. Dynamic Membership Rule
- B. Group Expiration Policy
- ✅ C. Group Naming Policy
- D. Administrative Unit

**Answer:** C 【1-58adad】

---

## Desafío opcional

Modificar la política para utilizar un sufijo:

```text
[GroupName]-ARG
```

Crear un nuevo grupo y verificar cómo cambia automáticamente el nombre generado. 【1-58adad】

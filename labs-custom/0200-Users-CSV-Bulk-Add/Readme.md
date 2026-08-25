# Mini Lab: Importar usuarios masivamente con CSV (MS-102)

**Objetivo:** Crear un archivo CSV a mano con 1-2 usuarios y cargarlo en el Microsoft 365 admin center usando **Add multiple users**.

**Duración estimada:** 10 minutos

**Prerrequisitos:**
- Acceso al Microsoft 365 admin center con rol de Administrador de usuarios o Administrador global
- Editor de texto simple (Notepad, VS Code, etc.) o Excel

---

## Parte 1 — Descargar la plantilla (opcional pero recomendado)

1. [BROWSER] Ingresá a **https://admin.microsoft.com** con tu cuenta de administrador.
2. [MENU] Navegá a **Users** > **Active users**.
3. [TAB] Hacé clic en **Add multiple users**.
4. [DIALOG] En el panel que se abre, marcá la opción **I'd like to upload a CSV with user information**.
5. [LINK] Hacé clic en **Download a blank CSV file with required headers** para ver las columnas exactas que espera el sistema.

> Si preferís armar el archivo 100% a mano sin descargar la plantilla, podés saltar directo a la Parte 2 — las columnas mínimas son las que se detallan ahí.

---

## Parte 2 — Crear el CSV a mano

1. Abrí un editor de texto plano (Notepad, VS Code) — **no uses Word**, porque agrega formato que rompe el CSV.
2. Escribí las columnas obligatorias como primera fila, y los datos de tus usuarios en las filas siguientes:

```
User Name,First Name,Last Name,Display Name
usuario1@tudominio.onmicrosoft.com,Juan,Perez,Juan Perez
usuario2@tudominio.onmicrosoft.com,Maria,Gomez,Maria Gomez
```

3. Guardá el archivo como `usuarios.csv` (asegurate de que la extensión sea `.csv`, no `.txt`).

> Recordá: solo **User Name** y **Display Name** son estrictamente obligatorios. First Name y Last Name son opcionales, pero conviene incluirlos para que el usuario quede bien identificado.

---

## Parte 3 — Cargar el CSV en el admin center

1. [BROWSER] Volvé a **Users** > **Active users** > **Add multiple users** (si cerraste el panel, abrilo de nuevo).
2. [DIALOG] Marcá **I'd like to upload a CSV with user information**.
3. [TAB] Hacé clic en **Browse** y seleccioná tu archivo `usuarios.csv`.
4. [BROWSER] El sistema valida el archivo automáticamente. Si hay errores (columnas faltantes, dominio inválido, usuario duplicado), te los va a marcar en pantalla — corregí el CSV y volvé a subirlo.
5. [DIALOG] Una vez validado, hacé clic en **Next**.

---

## Parte 4 — Configurar licencias y ubicación

1. [DIALOG] Seleccioná la **Usage location** (ej. Argentina).
2. [DIALOG] Asigná una licencia si tenés disponible (o "Create user without product license" si solo querés probar la carga).
3. [BROWSER] Hacé clic en **Next** y revisá el resumen.
4. [TAB] Hacé clic en **Add** para confirmar la creación.

---

## Parte 5 — Verificar el resultado

1. [DIALOG] Al finalizar, el sistema ofrece descargar un **archivo de resultados** con las contraseñas temporales generadas para cada usuario nuevo — descargalo y guardalo, no se puede recuperar después.
2. [MENU] Navegá a **Users** > **Active users** y confirmá que `Juan Perez` y `Maria Gomez` aparecen en la lista.

---

## Limpieza (opcional)

1. [MENU] Seleccioná cada usuario de prueba en **Active users** > **Delete user** para eliminarlos.

---

## Puntos clave para el examen

- El admin center de Microsoft 365 acepta **CSV**, no JSON ni XML, para carga masiva de usuarios.
- Columnas obligatorias: **User Name** (UPN) y **Display Name**. El resto son opcionales.
- El archivo debe guardarse como `.csv` real (no `.txt` renombrado, no exportado desde Word).
- El sistema valida el archivo antes de importar y muestra errores por fila si algo falta o está mal formado.

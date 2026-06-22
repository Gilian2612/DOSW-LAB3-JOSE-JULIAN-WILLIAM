# Evidencias del Product Backlog en Jira — Bankify

> **Documento:** `jira.md` · **Parte 6 — Product Backlog en Jira (20%)**
> **Responsable:** Julian
> **Épica asociada:** Depósitos controlados a cuentas bancarias
> **Workspace de Jira:** _(pegar aquí el enlace al workspace `DOSW_LAB_...`)_

---

## Cómo usar este archivo

Este documento contiene **todo el contenido listo para copiar y pegar en Jira** y los
espacios donde debes insertar las **capturas de pantalla** que exige el checklist de la
Parte 6. Pasos sugeridos:

1. Crea en Jira la épica, las 4 historias y las 12 tareas usando los textos de abajo.
2. A medida que las creas, anota el **ID real que asigna Jira** (p. ej. `DOSW-1`) en la
   columna correspondiente y reemplaza los placeholders `[EPIC-XX]`, `[STORY-XX]`, `[TASK-XX]`.
3. Toma la captura de cada elemento y guárdala en `docs/images/jira/`.
4. Reemplaza cada bloque `📸 _(insertar captura...)_` por la imagen real:
   `![Descripción](../images/jira/nombre.png)`
5. Actualiza también `scrum_work_bankify.md` con los IDs reales (actividad #4).

> 💡 Crea la carpeta `docs/images/jira/` para guardar todas las capturas de esta parte.

---

## Checklist de la Parte 6

| # | Actividad en Jira | Evidencia | Estado |
|---|-------------------|-----------|:------:|
| 1 | Crear la épica: título, descripción y fecha de vencimiento | Captura de la épica | ☐ |
| 2 | Crear las 4 historias de usuario: título y descripción | Captura de cada historia | ☐ |
| 3 | Crear las 12 tareas: título, descripción y actividades relacionadas | Captura de cada tarea | ☐ |
| 4 | Actualizar `scrum_work_bankify.md` con los IDs de Jira | Archivo actualizado | ☐ |
| 5 | Captura del cronograma/timeline en Jira | Captura del timeline | ☐ |

---

## 1. Épica

| Campo | Valor |
|-------|-------|
| **ID en Jira** | `[EPIC-XX]` |
| **Tipo** | Epic |
| **Título** | Depósitos controlados a cuentas bancarias |
| **Fecha de vencimiento** | _(definir, p. ej. fin del Sprint 1)_ |

**Descripción (pegar en Jira):**

> Como plataforma, Bankify debe permitir que un usuario autenticado deposite dinero en
> una cuenta —propia o de un tercero— de forma controlada, validando que la cuenta
> destino sea válida y esté activa, que el monto sea correcto, aplicando el incremento
> de saldo de manera transaccional y dejando registro auditable de la operación con su
> respectivo comprobante.

📸 _(insertar captura de la épica creada en Jira)_

---

## 2. Historias de Usuario

### HU-01 · Depósito a cuenta propia

| Campo | Valor |
|-------|-------|
| **ID en Jira** | `[STORY-XX]` |
| **Tipo** | Story |
| **Épica padre** | `[EPIC-XX]` |
| **Prioridad** | Alto |

**Descripción (pegar en Jira):**

> Como cliente propietario autenticado, quiero depositar dinero en mi propia cuenta
> para aumentar el saldo del que dispongo.
>
> **Criterios de aceptación:** el saldo se incrementa exactamente en el monto
> depositado; la operación es transaccional (sin estados parciales ante fallo); el
> cliente recibe confirmación visual; el tiempo de respuesta es menor a 2 segundos.

📸 _(insertar captura de la historia HU-01)_

---

### HU-02 · Depósito a cuenta de terceros

| Campo | Valor |
|-------|-------|
| **ID en Jira** | `[STORY-XX]` |
| **Tipo** | Story |
| **Épica padre** | `[EPIC-XX]` |
| **Prioridad** | Alto |

**Descripción (pegar en Jira):**

> Como usuario autenticado, quiero depositar dinero en la cuenta de otra persona
> indicando su número de cuenta para transferirle fondos.
>
> **Criterios de aceptación:** el saldo de la cuenta destino se incrementa en el monto
> indicado; el sistema confirma el banco destino (2 primeros dígitos) antes de procesar;
> no se requiere ser propietario de la cuenta destino; se genera el mismo registro y
> comprobante que en un depósito propio.

📸 _(insertar captura de la historia HU-02)_

---

### HU-03 · Validación de monto y cuenta destino

| Campo | Valor |
|-------|-------|
| **ID en Jira** | `[STORY-XX]` |
| **Tipo** | Story |
| **Épica padre** | `[EPIC-XX]` |
| **Prioridad** | Medio |

**Descripción (pegar en Jira):**

> Como usuario, quiero que el sistema valide el número de cuenta destino y el monto
> antes de ejecutar el depósito para evitar operaciones inválidas o erróneas.
>
> **Criterios de aceptación:** se valida que la cuenta tenga 10 dígitos numéricos y
> banco registrado (2 primeros dígitos); se rechazan montos no positivos o con formato
> inválido; si la cuenta no existe o está inactiva no se ejecuta el depósito; ninguna
> validación deja el saldo en estado inconsistente.

📸 _(insertar captura de la historia HU-03)_

---

### HU-04 · Comprobante del depósito

| Campo | Valor |
|-------|-------|
| **ID en Jira** | `[STORY-XX]` |
| **Tipo** | Story |
| **Épica padre** | `[EPIC-XX]` |
| **Prioridad** | Bajo |

**Descripción (pegar en Jira):**

> Como usuario, quiero recibir un comprobante del depósito realizado para tener
> evidencia de la operación.
>
> **Criterios de aceptación:** cada depósito exitoso genera un comprobante con id único,
> fecha y hora, cuenta destino, monto y usuario; el comprobante se visualiza
> inmediatamente; queda registrado en el log de transacciones; es de solo lectura.

📸 _(insertar captura de la historia HU-04)_

---

## 3. Tareas

> Cada tarea debe quedar **vinculada a su historia padre** en Jira (campo "Parent" o
> relación correspondiente). Esa vinculación es la "actividad relacionada" que pide el
> checklist.

### Tareas de HU-01 · Depósito a cuenta propia

| ID en Jira | Título | Historia padre | Descripción (pegar en Jira) |
|-----------|--------|----------------|------------------------------|
| `[TASK-XX]` | Endpoint de depósito | `[STORY-XX]` HU-01 | Diseñar e implementar `POST /api/accounts/{numero}/deposit` que reciba el monto a depositar. |
| `[TASK-XX]` | Lógica transaccional de saldo | `[STORY-XX]` HU-01 | Implementar en el dominio el incremento de saldo de forma atómica, con rollback ante cualquier fallo. |
| `[TASK-XX]` | Formulario de depósito (propio) | `[STORY-XX]` HU-01 | Construir el formulario UI para depositar en una cuenta propia, con validación básica y confirmación. |

📸 _(insertar captura de las 3 tareas de HU-01)_

### Tareas de HU-02 · Depósito a cuenta de terceros

| ID en Jira | Título | Historia padre | Descripción (pegar en Jira) |
|-----------|--------|----------------|------------------------------|
| `[TASK-XX]` | Soporte de cuenta destino externa | `[STORY-XX]` HU-02 | Adaptar el servicio de depósito para aceptar una cuenta destino que no pertenece al usuario que deposita. |
| `[TASK-XX]` | Búsqueda y verificación de cuenta destino | `[STORY-XX]` HU-02 | Implementar la consulta que verifica la existencia y el estado de la cuenta destino antes de depositar. |
| `[TASK-XX]` | Flujo UI de depósito a terceros | `[STORY-XX]` HU-02 | Construir la pantalla para ingresar el número de cuenta destino, mostrar el banco confirmado y el monto. |

📸 _(insertar captura de las 3 tareas de HU-02)_

### Tareas de HU-03 · Validación de monto y cuenta

| ID en Jira | Título | Historia padre | Descripción (pegar en Jira) |
|-----------|--------|----------------|------------------------------|
| `[TASK-XX]` | Validación de número de cuenta | `[STORY-XX]` HU-03 | Implementar el validador de formato (10 dígitos numéricos) y de banco registrado (prefijo de 2 dígitos). |
| `[TASK-XX]` | Validación de monto | `[STORY-XX]` HU-03 | Implementar la validación del monto: positivo, numérico y dentro de los límites permitidos. |
| `[TASK-XX]` | Manejo de errores en UI | `[STORY-XX]` HU-03 | Definir y mostrar mensajes claros de error y bloquear el envío hasta que los datos sean válidos. |

📸 _(insertar captura de las 3 tareas de HU-03)_

### Tareas de HU-04 · Comprobante de depósito

| ID en Jira | Título | Historia padre | Descripción (pegar en Jira) |
|-----------|--------|----------------|------------------------------|
| `[TASK-XX]` | Modelo de transacción/comprobante | `[STORY-XX]` HU-04 | Crear la entidad/tabla `transaccion_deposito` con id único, timestamp, cuenta, monto y usuario. |
| `[TASK-XX]` | Servicio de generación de comprobante | `[STORY-XX]` HU-04 | Implementar el servicio que arma y devuelve el comprobante tras un depósito exitoso. |
| `[TASK-XX]` | Pantalla de confirmación/comprobante | `[STORY-XX]` HU-04 | Construir la vista UI que muestra el comprobante del depósito realizado. |

📸 _(insertar captura de las 3 tareas de HU-04)_

---

## 4. Actualización de `scrum_work_bankify.md`

Una vez Jira asigne los IDs reales, se actualizó el archivo
`docs/planning/scrum_work_bankify.md` reemplazando los placeholders por los IDs
(`EPIC-XX`, `STORY-XX`, `TASK-XX`). ✅

> Marca esta casilla cuando el archivo quede actualizado y commiteado.

---

## 5. Cronograma / Timeline en Jira

Captura del cronograma (vista Timeline) mostrando la épica con sus historias y tareas
distribuidas en el tiempo.

📸 _(insertar captura del timeline de Jira)_

---

## Mapa rápido de IDs

> Tabla de control para registrar todos los IDs reales de un vistazo.

| Elemento | Título | ID Jira |
|----------|--------|---------|
| Épica | Depósitos controlados a cuentas bancarias | `[EPIC-XX]` |
| HU-01 | Depósito a cuenta propia | `[STORY-XX]` |
| HU-02 | Depósito a cuenta de terceros | `[STORY-XX]` |
| HU-03 | Validación de monto y cuenta | `[STORY-XX]` |
| HU-04 | Comprobante del depósito | `[STORY-XX]` |
| TASK | Endpoint de depósito | `[TASK-XX]` |
| TASK | Lógica transaccional de saldo | `[TASK-XX]` |
| TASK | Formulario de depósito (propio) | `[TASK-XX]` |
| TASK | Soporte de cuenta destino externa | `[TASK-XX]` |
| TASK | Búsqueda y verificación de cuenta destino | `[TASK-XX]` |
| TASK | Flujo UI de depósito a terceros | `[TASK-XX]` |
| TASK | Validación de número de cuenta | `[TASK-XX]` |
| TASK | Validación de monto | `[TASK-XX]` |
| TASK | Manejo de errores en UI | `[TASK-XX]` |
| TASK | Modelo de transacción/comprobante | `[TASK-XX]` |
| TASK | Servicio de generación de comprobante | `[TASK-XX]` |
| TASK | Pantalla de confirmación/comprobante | `[TASK-XX]` |

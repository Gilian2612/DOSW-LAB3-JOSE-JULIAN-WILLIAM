# Desglose del Trabajo — Bankify

> Responsable de la épica: Julian
> Requerimiento funcional asociado (Parte 4): RF — Realizar depósitos a una cuenta

---

## 1. Contexto

Bankify es una startup fintech en etapa de MVP que necesita permitir el ingreso de dinero a las cuentas de la plataforma de forma controlada. El depósito es una operación de escritura sobre el saldo, por lo que requiere validaciones estrictas de la cuenta destino y del monto, así como trazabilidad de cada movimiento.

Una particularidad del caso Bankify es que el depósito puede ser realizado tanto por el cliente propietario de la cuenta como por otros usuarios, lo que obliga a contemplar dos flujos: depósito a cuenta propia y depósito a cuenta de terceros.

Este documento estructura el trabajo de desarrollo usando la jerarquía ágil Épica → Historias de Usuario → Tareas. En esta etapa no se definen estimaciones; eso se realizará en la Parte 7 (Planning Poker). Aquí solo se define la prioridad de cada historia (Alto / Medio / Bajo) con su justificación.

### Reglas de negocio relevantes para esta épica

* Un número de cuenta tiene exactamente 10 dígitos, solo numéricos, sin caracteres especiales.
* Los dos primeros dígitos identifican el banco (`01` → Bancolombia, `02` → Davivienda).
* Una cuenta solo es válida si pertenece a un banco registrado en el sistema.
* El depósito puede hacerlo el cliente propietario u otros usuarios autorizados.
* El depósito debe ser controlado: monto válido, cuenta destino válida y activa, y registro de la transacción.

---

## 2. Épica

| Campo                | Valor                                                                                                                                                                                                                                                                                                                                                                   |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ID                   | EPIC-DEPOSITO-01                                                                                                                                                                                                                                                                                                                                                        |
| Título               | Depósitos controlados a cuentas bancarias                                                                                                                                                                                                                                                                                                                               |
| Descripción          | Como plataforma, Bankify debe permitir que un usuario autenticado deposite dinero en una cuenta —propia o de un tercero— de forma controlada, validando que la cuenta destino sea válida y esté activa, que el monto sea correcto, aplicando el incremento de saldo de manera transaccional y dejando registro auditable de la operación con su respectivo comprobante. |
| Objetivo de negocio  | Habilitar el ingreso de fondos a la plataforma de manera segura y trazable, condición indispensable para que cualquier otra operación de dinero tenga sentido en el MVP.                                                                                                                                                                                                |
| Fecha de vencimiento | (definir en Jira — Parte 6)                                                                                                                                                                                                                                                                                                                                             |
| Rol principal        | Cliente propietario / otros usuarios                                                                                                                                                                                                                                                                                                                                    |

---

## 3. Historias de Usuario

> Formato: Como [rol], quiero [acción] para [beneficio].
> Cada historia incluye criterios de aceptación y prioridad justificada.

### HU-01 · Depositar dinero en una cuenta propia

Como cliente propietario autenticado, quiero depositar dinero en mi propia cuenta para aumentar el saldo del que dispongo.

Criterios de aceptación

* Dado que el cliente selecciona una cuenta propia y un monto válido, cuando confirma el depósito, entonces el saldo de la cuenta se incrementa exactamente en el monto depositado.
* La operación es transaccional: si falla cualquier paso, el saldo no se modifica parcialmente.
* El cliente recibe confirmación visual de que el depósito fue exitoso.
* La operación cumple el tiempo objetivo de la plataforma (< 2 segundos).

Prioridad: Alto

Justificación: Es el flujo base y más simple de la épica (el usuario opera sobre su propia cuenta). Entrega el valor central —ingresar dinero— y es prerequisito para el resto de historias. Indispensable en la primera iteración.

---

### HU-02 · Depositar dinero en la cuenta de un tercero

Como usuario autenticado, quiero depositar dinero en la cuenta de otra persona indicando su número de cuenta para transferirle fondos.

Criterios de aceptación

* Dado un número de cuenta destino válido y existente, cuando el usuario confirma el depósito, entonces el saldo de esa cuenta se incrementa en el monto indicado.
* El sistema confirma al usuario el banco destino (derivado de los 2 primeros dígitos) antes de procesar, para reducir errores.
* El usuario no necesita ser propietario de la cuenta destino para depositar.
* El depósito a un tercero genera el mismo registro y comprobante que un depósito propio.

Prioridad: Alto

Justificación: Es un flujo explícitamente requerido por el caso (otros usuarios pueden depositar). Tiene alto valor de negocio y comparte gran parte de la lógica con HU-01, por lo que conviene abordarlo en la misma iteración.

---

### HU-03 · Validar el monto y la cuenta destino antes de procesar el depósito

Como usuario, quiero que el sistema valide el número de cuenta destino y el monto antes de ejecutar el depósito para evitar operaciones inválidas o erróneas.

Criterios de aceptación

* El sistema valida que el número de cuenta tenga exactamente 10 dígitos numéricos y que los 2 primeros correspondan a un banco registrado.
* El sistema rechaza montos que no sean positivos, no numéricos o con formato inválido.
* Si la cuenta destino no existe o está inactiva, el depósito no se ejecuta y se informa con un mensaje claro.
* Ninguna validación deja el saldo en un estado intermedio o inconsistente.

Prioridad: Medio

Justificación: Es clave para que el depósito sea "controlado", pero se construye sobre los flujos de HU-01 y HU-02. Su valor depende de que el flujo base ya exista, por lo que su prioridad es media respecto a las historias núcleo.

---

### HU-04 · Generar comprobante del depósito realizado

Como usuario, quiero recibir un comprobante del depósito realizado para tener evidencia de la operación.

Criterios de aceptación

* Cada depósito exitoso genera un comprobante con identificador único, fecha y hora, cuenta destino, monto y usuario que depositó.
* El usuario puede visualizar el comprobante inmediatamente después de la operación.
* El comprobante queda registrado como parte del log de transacciones para auditoría.
* El comprobante es de solo lectura y no puede ser alterado.

Prioridad: Bajo

Justificación: Mejora la confianza y la trazabilidad, pero el depósito puede funcionar sin un comprobante formal en la primera iteración. Es una mejora de valor que puede entregarse después sin bloquear el MVP.

---

## 4. Tareas

> 3 tareas por historia. Cada tarea es una unidad de trabajo técnico asignable a un integrante. No se estiman horas en esta parte.

### Tareas de HU-01 · Depósito a cuenta propia

| ID      | Tarea                           | Descripción técnica                                                                                  |
| ------- | ------------------------------- | ---------------------------------------------------------------------------------------------------- |
| TASK-01 | Endpoint de depósito            | Diseñar e implementar POST /api/accounts/{numero}/deposit que reciba el monto a depositar.         |
| TASK-02 | Lógica transaccional de saldo   | Implementar en el dominio el incremento de saldo de forma atómica (rollback ante fallo).             |
| TASK-03 | Formulario de depósito (propio) | Construir el formulario UI para depositar en una cuenta propia con validación básica y confirmación. |

### Tareas de HU-02 · Depósito a cuenta de terceros

| ID      | Tarea                                     | Descripción técnica                                                                                       |
| ------- | ----------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| TASK-04 | Soporte de cuenta destino externa         | Adaptar el servicio de depósito para aceptar una cuenta destino que no pertenece al usuario que deposita. |
| TASK-05 | Búsqueda y verificación de cuenta destino | Implementar la consulta que verifica la existencia y el estado de la cuenta destino antes de depositar.   |
| TASK-06 | Flujo UI de depósito a terceros           | Construir la pantalla para ingresar número de cuenta destino, mostrar el banco confirmado y el monto.     |

### Tareas de HU-03 · Validación de monto y cuenta

| ID      | Tarea                          | Descripción técnica                                                                                            |
| ------- | ------------------------------ | -------------------------------------------------------------------------------------------------------------- |
| TASK-07 | Validación de número de cuenta | Implementar validador de formato (10 dígitos numéricos) y de banco registrado (prefijo de 2 dígitos).          |
| TASK-08 | Validación de monto            | Implementar la validación del monto: positivo, numérico y dentro de límites permitidos.                        |
| TASK-09 | Manejo de errores en UI        | Definir y mostrar mensajes claros de error de validación y bloquear el envío hasta que los datos sean válidos. |

### Tareas de HU-04 · Comprobante de depósito

| ID      | Tarea                                 | Descripción técnica                                                                             |
| ------- | ------------------------------------- | ----------------------------------------------------------------------------------------------- |
| TASK-10 | Modelo de transacción/comprobante     | Crear la entidad/tabla transaccion_deposito con id único, timestamp, cuenta, monto y usuario. |
| TASK-11 | Servicio de generación de comprobante | Implementar el servicio que arma y devuelve el comprobante tras un depósito exitoso.            |
| TASK-12 | Pantalla de confirmación/comprobante  | Construir la vista UI que muestra el comprobante del depósito realizado.                        |

---

## 5. Resumen de prioridades

| Historia | Título                        | Prioridad |
| -------- | ----------------------------- | --------- |
| HU-01    | Depósito a cuenta propia      | Alto      |
| HU-02    | Depósito a cuenta de terceros | Alto      |
| HU-03    | Validación de monto y cuenta  | Medio     |
| HU-04    | Comprobante de depósito       | Bajo      |


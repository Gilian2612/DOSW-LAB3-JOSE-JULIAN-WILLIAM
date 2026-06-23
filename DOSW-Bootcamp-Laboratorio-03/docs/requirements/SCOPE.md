# Bankify — Sistema de Gestión Bancaria

## Sistema

**Bankify** es una plataforma fintech en etapa MVP desarrollada para la gestión básica de cuentas bancarias. El sistema conecta múltiples usuarios (naturales y jurídicos) con entidades financieras, permitiendo consultar información y realizar operaciones financieras simples desde un entorno digital centralizado.

El sistema está construido sobre **AWS** (Amazon Web Services) como plataforma de servicios en la nube, e integra con la **DIAN** (Dirección de Impuestos y Aduanas Nacionales) como sistema externo para el reporte tributario.

---

## Problema a resolver

Bankify no cuenta actualmente con ningún sistema digital de gestión bancaria. Las siguientes funcionalidades críticas están ausentes:


El objetivo del MVP es validar el modelo de negocio implementando estas funcionalidades esenciales antes de escalar la plataforma.

---

## Diagrama de contexto 

![alt text](<uml/DIAGRAMA_CONTEXTO_bankify .png>)



### Actores externos

| Actor | Descripción |
|---|---|
| **Cliente** | Usuario persona natural o jurídica que consulta saldos y realiza transacciones |
| **Asesor** | Personal encargado de atender los requerimientos de los clientes y gestionar cuentas |
| **Supervisor** | Responsable de aprobar operaciones, gestionar clientes y auditar actividad |
| **Gerente Financiero** | Líder de la institución que consulta reportes y envía información a la DIAN |
| **DIAN** | Sistema externo — Dirección de Impuestos y Aduanas Nacionales (receptor de reportes tributarios) |

### Sistemas externos

| Sistema | Rol |
|---|---|
| **DIAN** | Recibe reportes tributarios en formato JSON generados por el Gerente Financiero |
| **AWS** | Plataforma de servicios en la nube sobre la que corre la infraestructura de Bankify |

---

## Alcance del sistema

El MVP de Bankify cubre las siguientes funcionalidades confirmadas con el Gerente de Operaciones:

### Funcionalidades incluidas

| Funcionalidad | Rol autorizado |
|---|---|
| Autenticación con usuario y contraseña | Operadores y Clientes |
| Gestión de clientes: crear, activar, inactivar, actualizar | Supervisor |
| Gestión de cuentas: crear, activar, inactivar, actualizar | Asesor (todas) / Cliente (solo inactivar) |
| Consulta de saldo de cuenta | Cliente |
| Depósito a una cuenta | Cliente propietario u otros usuarios |
| Generar reporte tributario (declaración de renta) en PDF | Cliente |
| Generar reporte tributario de todas las cuentas para la DIAN | Gerente Financiero |
| Eliminar cliente y sus cuentas asociadas | Supervisor |

### Reglas de negocio confirmadas

- Los números de cuenta deben tener **exactamente 10 dígitos**, solo numéricos, sin caracteres especiales.
- Los dos primeros dígitos identifican el banco

- Una cuenta solo es válida si pertenece a un banco registrado en el sistema.

### Fuera del alcance del MVP

- Transferencias entre entidades bancarias externas
- Integración con redes de pago (PSE, ACH, Nequi, Dale, Daviplata, Stripe, Paypla,   Bre b, Nu, lulobank, google wallet, bitcoin, wise, )
- Aplicación móvil nativa
- Créditos, inversiones u otros productos financieros complejos

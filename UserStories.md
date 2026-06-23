## Historias de Usuario 

## Conclusiones Poker Planning: 

- El usuario puede tener las siguientes interacciones: 

    - Depositos de dinero 
    - Solicitar y recibir comprobante de pago 
    - Ver confirmación de entidad destinataria del dinero 

- El usuario NO puede tener las siguientes interacciones: 

    - Retirar dinero
    - Transferencias bancarias entre sus ropias cuentas 
    - Modificar comprobantes 
    - Eliminar comprobantes 
    - Depositar dinero en cuentas que no existan 
    - Depositar valores menores a 0 


## 1. Como cliente de Bankify, quiero depositar dinero en mi cuenta para disponer del mismo 

## 2. Como usuario de Bankify, quiero depositar dinero en la cuenta de un tercero sabiendo el número de cuenta y teniendo el saldo suficiente paara hacer pagos por diferentes conceptos 

## 3. Como usuario de Bankify, quiero tener un comprobante de la transacción realizada para poder tener evidencia de la operación bancaria 

## 4. Como usuario de Bankify, quiero validar cuanto saldo tengo en mi cuenta y mi número de cuenta, así como el número de cuenta destino y el monto que se va a transferir, para poder evitar operaciones incorrectas. 


## ESTIMACIONES DEL PLANNING POKER 

| Historia | Título | Prioridad | Estimación (puntos) | Justificación de la estimación |
| -------- | ----------------------------- | --------- | :-----------------: | --- |
| 1 | Depósito a cuenta propia | Alto | 8 | Involucra tres capas completas: endpoint REST, lógica transaccional en dominio y formulario UI con validación y confirmación. Es el flujo base de la épica y el más pesado ya que construye toda la infraestructura desde cero. |
| 2 | Depósito a cuenta de terceros | Alto | 3 | Usa gran parte de la lógica de la historia de usuario 1. Se debe adaptar el servicio para aceptar cuenta externa, implementar la verificación de cuenta destino y construir la pantalla con confirmación de banco. Menos esfuerzo que la historia de usuario 1 porque la base ya existe. |
| 3 | Validación de monto y cuenta | Medio | 3 | Son validaciones de formato (10 dígitos numéricos, prefijo de banco registrado) y de monto (positivo, numérico, dentro de límites). Hay que cubrir casos con tests para que ninguna validación deje el saldo inconsistente |
| 4 | Comprobante de depósito | Bajo | 2 | Es principalmente lectura y presentación. Crear la entidad con los campos del comprobante, armar el objeto con datos que ya existen del depósito y mostrarlo en una vista de solo lectura. Sin lógica pesada |

## REFLEXIÓN 

- ¿Cuál fue la mayor dificultad a la hora de estimar?
    - Separar el esfuerzo que realmente se necesitaba para las primeras 2 historias de uso, pues la historia de uso 2 depende de la primera, es un claro indicador de que la historia de uso debe ser la de mayor prioridad, 


- ¿Fue fácil llegar a un consenso?
    - Si, para las ultimas 2 historias de uso, las discrepancias se dieron en su mayor parte en la primera hsitoria de uso ya que la prioridad de la misma dependia no sólo de la necesidad de copmpletarla para la segunda historia, sino en que hay gran parte de complejidad algorítmica en la misma, pues es la base de la cadena de acciones de interacción del cliente con Bankify 

- ¿Cómo resolvieron las discrepancias grandes?
    - Por medio de votación, llegando a consensos gracias a discusiones y exposiciones del por qué de la valoración individual de cada una de las historias de usuario, posteriormente repitiendo votaciones y tratando de llegar a un punto medio en aquellos casos donde se mantuvieran las discrepancias (ej historia de uso 1, se le dió prioridad 11 y 5, durante varias votaciones se repetía, así que el consenso fue llegar a ujn puntaje de 8 para la misma)
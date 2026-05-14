# Casos de Uso - Pasarela de Pagos

## Actor: Pasarela de Pagos

La pasarela de pagos es el servicio externo encargado de procesar las transacciones realizadas por los visitantes durante el proceso de reserva.

En el MVP, All Roads no captura datos sensibles de tarjeta. El pago se realiza directamente en la pasarela, y el sistema actualiza la orden/reserva según el resultado recibido: aprobado, rechazado, pendiente, expirado o fallido.

---

## CU-PP-001 - Redirigir usuario a pasarela de pagos

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Visitante |
| **Actor secundario** | Pasarela de pagos |
| **Módulo** | Pagos |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Permitir que el visitante sea enviado a la pasarela de pagos para completar el pago de una reserva previamente creada.

### Precondiciones

- El visitante debe tener una reserva/orden creada.
- La reserva debe estar en estado pendiente de pago.
- Debe existir un intento de pago registrado en el sistema.
- La pasarela de pagos debe estar disponible.

### Flujo principal

1. El visitante completa el formulario de reserva.
2. El sistema crea la orden/reserva en estado pendiente.
3. El sistema crea el registro interno del intento de pago.
4. El sistema prepara la información requerida por la pasarela.
5. El sistema redirige al visitante a la pasarela de pagos.
6. El visitante continúa el proceso directamente en la pasarela.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | La pasarela no está disponible | El sistema informa que no es posible iniciar el pago y permite reintentar. |
| **FA-02** | No existe una reserva pendiente | El sistema bloquea la redirección y solicita revisar la reserva. |
| **FA-03** | Error al crear el intento de pago | El sistema no redirige al visitante y muestra un mensaje controlado. |

### Criterios de aceptación

- El visitante solo puede ir a la pasarela si existe una reserva pendiente.
- El sistema debe registrar el intento de pago antes de redirigir.
- El sistema no debe capturar datos sensibles de tarjeta.
- La redirección debe enviar la información necesaria para identificar la transacción.

---

## CU-PP-002 - Procesar pago aprobado

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Pasarela de pagos |
| **Actor secundario** | Sistema All Roads |
| **Módulo** | Pagos / Reservas |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Actualizar la reserva como pagada cuando la pasarela informe que la transacción fue aprobada.

### Precondiciones

- Debe existir una reserva pendiente.
- Debe existir un intento de pago asociado.
- La pasarela debe retornar o notificar un resultado aprobado.

### Flujo principal

1. La pasarela procesa el pago del visitante.
2. La pasarela retorna o notifica que el pago fue aprobado.
3. El sistema valida la referencia de la transacción.
4. El sistema actualiza el pago como aprobado.
5. El sistema actualiza la reserva como pagada.
6. El sistema habilita el envío del correo de confirmación.
7. El visitante visualiza el resultado exitoso del pago.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | La referencia de pago no existe | El sistema no actualiza la reserva y registra la inconsistencia. |
| **FA-02** | La reserva ya fue pagada | El sistema conserva el estado pagado y evita duplicar la confirmación. |
| **FA-03** | Error al enviar correo | La reserva permanece pagada y se registra el intento de envío. |

### Criterios de aceptación

- Un pago aprobado debe dejar la reserva en estado pagado.
- El sistema debe conservar la trazabilidad del pago.
- El correo de confirmación solo se envía cuando la reserva queda pagada.
- No se deben duplicar confirmaciones para la misma transacción.

---

## CU-PP-003 - Procesar pago rechazado

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Pasarela de pagos |
| **Actor secundario** | Sistema All Roads |
| **Módulo** | Pagos / Reservas |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Registrar que el pago fue rechazado y evitar que la reserva quede confirmada como pagada.

### Precondiciones

- Debe existir una reserva pendiente.
- Debe existir un intento de pago asociado.
- La pasarela debe retornar o notificar un resultado rechazado.

### Flujo principal

1. La pasarela procesa el pago del visitante.
2. La pasarela retorna o notifica que el pago fue rechazado.
3. El sistema valida la referencia de la transacción.
4. El sistema actualiza el intento de pago como rechazado.
5. La reserva no queda marcada como pagada.
6. El sistema muestra al visitante un resultado de pago rechazado.
7. El visitante podrá intentar nuevamente el proceso de pago si corresponde.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | La referencia de pago no existe | El sistema registra la inconsistencia y no actualiza la reserva. |
| **FA-02** | El visitante desea reintentar | El sistema permite iniciar un nuevo intento cuando el intento anterior finalice. |

### Criterios de aceptación

- Un pago rechazado no debe confirmar la reserva como pagada.
- El sistema debe mostrar un mensaje claro al visitante.
- El sistema debe conservar la trazabilidad del intento rechazado.
- El visitante debe poder volver a intentar el pago según el flujo definido.

---

## CU-PP-004 - Procesar pago pendiente, expirado o fallido

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Pasarela de pagos |
| **Actor secundario** | Sistema All Roads |
| **Módulo** | Pagos / Reservas |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Actualizar el estado del pago y de la reserva cuando la transacción no finaliza como aprobada o rechazada de forma inmediata.

### Precondiciones

- Debe existir una reserva pendiente.
- Debe existir un intento de pago asociado.
- La pasarela debe retornar o permitir identificar un estado pendiente, expirado o fallido.

### Flujo principal

1. El visitante inicia el pago en la pasarela.
2. La pasarela procesa la transacción.
3. La pasarela retorna o notifica un estado diferente a aprobado.
4. El sistema identifica el estado recibido.
5. El sistema actualiza el intento de pago según corresponda:
   - Pendiente.
   - Expirado.
   - Fallido.
6. La reserva no queda marcada como pagada.
7. El sistema muestra al visitante el resultado correspondiente.

### Estados esperados

| Estado | Comportamiento |
| :--- | :--- |
| **Pendiente** | La transacción aún no tiene confirmación definitiva. |
| **Expirado** | El tiempo disponible para completar el pago venció. |
| **Fallido** | Ocurrió un error técnico durante el proceso de pago. |

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | El pago queda pendiente | El sistema informa que la transacción aún no ha sido confirmada. |
| **FA-02** | El pago expira | El sistema informa que el tiempo de pago venció. |
| **FA-03** | El pago falla por error técnico | El sistema informa que no fue posible completar el pago. |

### Criterios de aceptación

- El sistema debe diferenciar entre pago pendiente, expirado y fallido.
- La reserva no debe quedar pagada si el pago no fue aprobado.
- El sistema debe mostrar un resultado comprensible para el visitante.
- El sistema debe conservar el registro del intento de pago.

---

## CU-PP-005 - Gestionar transacción no confirmada

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Sistema All Roads |
| **Actor secundario** | Pasarela de pagos |
| **Módulo** | Pagos / Trazabilidad |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Conservar la trazabilidad de una transacción cuando no se recibe confirmación definitiva de la pasarela de pagos.

### Precondiciones

- Debe existir una reserva pendiente.
- Debe existir un intento de pago creado.
- El usuario debió haber iniciado el proceso en la pasarela.

### Flujo principal

1. El visitante inicia el pago desde All Roads.
2. El sistema registra el intento de pago.
3. El visitante es redirigido a la pasarela.
4. La transacción no retorna confirmación definitiva.
5. El sistema mantiene la trazabilidad del intento.
6. La reserva no queda marcada como pagada.
7. Una vez finalizado o vencido el intento anterior, el visitante debe volver a intentar el proceso de pago.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | Falla el retorno desde la pasarela | El sistema conserva el intento registrado y no confirma la reserva como pagada. |
| **FA-02** | No llega confirmación de la pasarela | El sistema mantiene el pago sin confirmación definitiva. |
| **FA-03** | Existe una inconsistencia en la transacción | El sistema conserva trazabilidad y evita confirmar la reserva automáticamente. |

### Criterios de aceptación

- El sistema debe conservar trazabilidad del intento de pago.
- La reserva no debe quedar pagada sin confirmación.
- En el MVP no se contempla reconciliación automática.
- El usuario deberá volver a intentar el pago cuando el intento anterior finalice o venza.

---

## CU-PP-006 - Controlar vigencia del intento de pago

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Sistema All Roads |
| **Actor secundario** | Pasarela de pagos |
| **Módulo** | Pagos |
| **Prioridad** | Media |
| **Estado MVP** | Incluido |

### Objetivo

Controlar el tiempo disponible para que el visitante complete el pago de una reserva pendiente.

### Precondiciones

- Debe existir una reserva pendiente.
- Debe existir un intento de pago activo.
- La pasarela debe tener definido un tiempo de vigencia.

### Flujo principal

1. El sistema crea la reserva pendiente.
2. El sistema crea el intento de pago.
3. El visitante es redirigido a la pasarela.
4. El tiempo de vigencia del pago comienza a contar según lo definido por la pasarela.
5. Si el visitante completa el pago dentro del tiempo permitido, se procesa el resultado.
6. Si el tiempo vence, el intento de pago queda expirado.
7. El visitante deberá iniciar un nuevo intento de pago si desea continuar.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | El pago se completa dentro del tiempo | El sistema procesa el resultado recibido. |
| **FA-02** | El tiempo de pago vence | El sistema marca o interpreta el intento como expirado. |

### Criterios de aceptación

- El tiempo de vigencia debe corresponder al estipulado por la pasarela.
- Para el MVP se contempla una vigencia de 30 minutos.
- Un pago vencido no debe confirmar la reserva como pagada.
- Después del vencimiento, el visitante debe volver a intentar el pago.

---

## Reglas generales de la pasarela de pagos

| Regla | Descripción |
| :--- | :--- |
| **RN-PP-001** | Antes de enviar al visitante a la pasarela, debe existir una reserva/orden pendiente. |
| **RN-PP-002** | El sistema debe registrar un intento de pago antes de la redirección. |
| **RN-PP-003** | All Roads no captura datos sensibles de tarjeta. |
| **RN-PP-004** | El pago ocurre directamente en la pasarela de pagos. |
| **RN-PP-005** | Un pago aprobado deja la reserva en estado pagado. |
| **RN-PP-006** | Un pago rechazado no confirma la reserva como pagada. |
| **RN-PP-007** | Un pago fallido, expirado o pendiente no debe marcar la reserva como pagada. |
| **RN-PP-008** | Si no llega confirmación definitiva, el sistema conserva trazabilidad del intento. |
| **RN-PP-009** | En el MVP no se contempla reconciliación automática. |
| **RN-PP-010** | Si el intento finaliza o vence sin confirmación aprobada, el visitante debe volver a intentar el pago. |
| **RN-PP-011** | El tiempo de vigencia del pago será el definido por la pasarela de pagos, estimado en 30 minutos para el MVP. |

---

## Estados de pago contemplados

| Estado | Descripción | Efecto sobre la reserva |
| :--- | :--- | :--- |
| **Creado** | El sistema creó el intento de pago antes de redirigir a la pasarela. | Reserva pendiente. |
| **En proceso** | El visitante fue enviado a la pasarela y el pago está en curso. | Reserva pendiente. |
| **Aprobado** | La pasarela confirmó el pago exitoso. | Reserva pagada. |
| **Rechazado** | La pasarela rechazó la transacción. | Reserva no pagada. |
| **Pendiente** | No existe confirmación definitiva. | Reserva pendiente. |
| **Expirado** | Venció el tiempo para completar el pago. | Reserva no pagada. |
| **Fallido** | Ocurrió un error técnico en el proceso. | Reserva no pagada. |

---

## Restricciones del MVP

| Restricción | Descripción |
| :--- | :--- |
| **Sin captura de tarjeta** | All Roads no almacena ni procesa datos sensibles de pago. |
| **Sin reconciliación automática** | Las inconsistencias no se resuelven automáticamente en el MVP. |
| **Sin gestión manual desde backoffice** | El administrador no puede modificar pagos ni cambiar estados manualmente. |
| **Sin devoluciones desde el sistema** | Reversos, devoluciones o conciliaciones quedan fuera del alcance del MVP. |
| **Sin reglas avanzadas de pago** | No se contemplan cupones, descuentos ni tarifas dinámicas en esta fase. |

---

## Casos de uso relacionados

| Código | Nombre |
| :--- | :--- |
| **CU-VIS-006** | Diligenciar formulario de reserva |
| **CU-VIS-007** | Crear orden/reserva previa al pago |
| **CU-VIS-008** | Realizar pago en pasarela |
| **CU-VIS-009** | Visualizar resultado del pago |
| **CU-VIS-010** | Recibir confirmación de reserva |
| **CU-SC-001** | Enviar correo de confirmación de reserva |
| **CU-ADM-003** | Consultar listado de reservas |
| **CU-ADM-004** | Consultar detalle de reserva |
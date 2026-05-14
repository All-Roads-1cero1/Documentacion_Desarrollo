# Casos de Uso - Servicio de Correo

## Actor: Servicio de Correo

El servicio de correo es el sistema externo o componente de mensajería encargado de enviar correos transaccionales relacionados con el flujo del MVP de All Roads.

En esta fase, el servicio de correo se utiliza principalmente para:

- Enviar la confirmación de reserva cuando el pago sea aprobado.
- Enviar el código de verificación para recuperación de contraseña del administrador.

No se contempla en el MVP la administración avanzada de plantillas, reenvíos manuales, reportes de notificaciones ni gestión centralizada de eventos de correo.

---

## CU-SC-001 - Enviar correo de confirmación de reserva

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Sistema All Roads |
| **Actor secundario** | Servicio de correo |
| **Módulo** | Confirmación / Notificaciones |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Enviar un correo de confirmación al comprador cuando el pago sea aprobado y la reserva quede registrada como pagada.

### Precondiciones

- Debe existir una reserva creada.
- La reserva debe estar asociada a un comprador.
- El comprador debe tener un correo electrónico registrado.
- El pago debe estar aprobado.
- La reserva debe quedar en estado pagado.
- El servicio de correo debe estar disponible.

### Flujo principal

1. La pasarela de pagos confirma que el pago fue aprobado.
2. El sistema actualiza el intento de pago como aprobado.
3. El sistema actualiza la reserva como pagada.
4. El sistema prepara la información básica de la reserva.
5. El sistema solicita al servicio de correo el envío de la confirmación.
6. El servicio de correo envía el mensaje al comprador.
7. El comprador recibe el correo de confirmación de la reserva.

### Información mínima del correo

| Dato | Descripción |
| :--- | :--- |
| **Nombre del comprador** | Nombre de la persona que realizó la reserva. |
| **Correo del comprador** | Dirección a la que se enviará la confirmación. |
| **Tours reservados** | Tours incluidos en la compra. |
| **Cantidad de personas** | Cantidad definida por cada tour. |
| **Valor total** | Total pagado por la reserva. |
| **Estado de la reserva** | Reserva pagada o confirmada. |
| **Información básica de contacto** | Datos generales definidos por All Roads, si aplica. |

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | El correo del comprador está vacío | El sistema no envía el correo y registra el evento como no procesado. |
| **FA-02** | El correo tiene formato inválido | El sistema evita el envío y conserva la reserva como pagada. |
| **FA-03** | El servicio de correo no está disponible | El sistema conserva la reserva pagada y registra el intento fallido. |
| **FA-04** | Error durante el envío | El sistema registra el error sin afectar el estado de la reserva. |

### Criterios de aceptación

- El correo solo debe enviarse cuando el pago esté aprobado.
- La reserva debe quedar pagada antes de solicitar el envío del correo.
- El correo debe enviarse al comprador registrado en la reserva.
- Si el correo falla, la reserva no debe perder su estado pagado.
- El sistema debe conservar trazabilidad del intento de envío.
- El mensaje no debe incluir información sensible de pago.

---

## CU-SC-002 - Enviar código de recuperación de contraseña

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Sistema All Roads |
| **Actor secundario** | Servicio de correo |
| **Módulo** | Autenticación / Recuperación de contraseña |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Enviar un código de verificación al correo registrado del administrador para validar su identidad antes de permitir el cambio de contraseña.

### Precondiciones

- El administrador debe estar registrado en el sistema.
- El administrador debe ingresar un correo válido.
- El correo debe estar asociado a una cuenta administrativa.
- El sistema debe generar un código de verificación.
- El servicio de correo debe estar disponible.

### Flujo principal

1. El administrador selecciona la opción de recuperar contraseña.
2. El administrador ingresa su correo electrónico.
3. El sistema valida que el correo esté registrado.
4. El sistema genera un código de verificación.
5. El sistema solicita al servicio de correo el envío del código.
6. El servicio de correo envía el código al correo del administrador.
7. El administrador recibe el código.
8. El administrador continúa con la validación del código en el sistema.

### Información mínima del correo

| Dato | Descripción |
| :--- | :--- |
| **Correo del administrador** | Dirección registrada para la cuenta administrativa. |
| **Código de verificación** | Código generado para validar la recuperación. |
| **Mensaje de seguridad** | Indicación de que el código se usa para cambio de contraseña. |
| **Tiempo de vigencia** | Tiempo durante el cual el código será válido, si aplica. |

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | El correo no está registrado | El sistema muestra un mensaje controlado y no envía código. |
| **FA-02** | El correo tiene formato inválido | El sistema solicita corregir el correo. |
| **FA-03** | No se puede generar el código | El sistema informa que no fue posible iniciar la recuperación. |
| **FA-04** | El servicio de correo falla | El sistema informa que no fue posible enviar el código y permite reintentar. |

### Criterios de aceptación

- El código solo debe enviarse a correos administrativos registrados.
- El sistema debe generar el código antes de solicitar el envío.
- El correo debe permitir al administrador continuar el flujo de recuperación.
- El sistema no debe cambiar la contraseña solo por enviar el código.
- Si el envío falla, el administrador debe poder intentarlo nuevamente.
- El código debe ser validado antes de permitir registrar una nueva contraseña.

---

## CU-SC-003 - Registrar resultado del envío de correo

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Sistema All Roads |
| **Actor secundario** | Servicio de correo |
| **Módulo** | Notificaciones / Trazabilidad |
| **Prioridad** | Media |
| **Estado MVP** | Incluido parcialmente |

### Objetivo

Conservar trazabilidad básica del intento de envío de correos transaccionales del MVP.

### Precondiciones

- El sistema debe haber solicitado el envío de un correo.
- El servicio de correo debe retornar una respuesta o error del intento.
- El correo debe corresponder a un flujo incluido en el MVP.

### Flujo principal

1. El sistema solicita el envío de un correo transaccional.
2. El servicio de correo procesa la solicitud.
3. El servicio de correo retorna una respuesta de éxito o error.
4. El sistema registra el resultado del intento.
5. El sistema conserva la trazabilidad básica del envío.

### Tipos de correo contemplados

| Tipo | Uso |
| :--- | :--- |
| **Confirmación de reserva** | Se envía cuando el pago queda aprobado. |
| **Código de recuperación** | Se envía cuando el administrador solicita recuperar contraseña. |

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | Envío exitoso | El sistema registra el intento como enviado. |
| **FA-02** | Envío fallido | El sistema registra el error del intento. |
| **FA-03** | Respuesta no disponible | El sistema conserva el intento como no confirmado o pendiente de validación técnica. |

### Criterios de aceptación

- El sistema debe registrar si el correo fue solicitado.
- El sistema debe conservar el resultado básico del intento.
- Un error de correo no debe modificar el estado de una reserva pagada.
- La trazabilidad debe servir para revisión técnica.
- No se contempla en el MVP un panel administrativo para gestionar estos eventos.

---

## Reglas generales del servicio de correo

| Regla | Descripción |
| :--- | :--- |
| **RN-SC-001** | El correo de confirmación hace parte del MVP. |
| **RN-SC-002** | El correo de confirmación solo se envía cuando el pago está aprobado y la reserva queda pagada. |
| **RN-SC-003** | El sistema no debe enviar confirmaciones de reserva para pagos rechazados, pendientes, expirados o fallidos. |
| **RN-SC-004** | El código de recuperación solo se envía a correos administrativos registrados. |
| **RN-SC-005** | El envío del código no cambia la contraseña del administrador. |
| **RN-SC-006** | La contraseña solo podrá cambiarse después de validar correctamente el código. |
| **RN-SC-007** | Si falla el envío de correo, el sistema debe mostrar un mensaje controlado o registrar el intento fallido. |
| **RN-SC-008** | El sistema no debe incluir datos sensibles de pago en los correos. |
| **RN-SC-009** | La gestión avanzada de plantillas, reenvíos y eventos queda fuera del MVP. |

---

## Restricciones del MVP

| Restricción | Descripción |
| :--- | :--- |
| **Sin administración de plantillas** | Las plantillas de correo no se gestionan desde el backoffice en esta fase. |
| **Sin reenvíos manuales** | El administrador no podrá reenviar correos desde el panel. |
| **Sin dashboard de notificaciones** | No habrá vista administrativa para métricas o eventos de correo. |
| **Sin edición de contenido desde panel** | El contenido de los correos no será editable desde el backoffice. |
| **Sin envío de campañas** | Solo se contemplan correos transaccionales del MVP. |

---

## Casos de uso relacionados

| Código | Nombre |
| :--- | :--- |
| **CU-VIS-008** | Realizar pago en pasarela |
| **CU-VIS-009** | Visualizar resultado del pago |
| **CU-VIS-010** | Recibir confirmación de reserva |
| **CU-PP-002** | Procesar pago aprobado |
| **CU-ADM-005** | Recuperar contraseña |
| **CU-ADM-006** | Validar código de recuperación |
| **CU-ADM-007** | Registrar nueva contraseña |
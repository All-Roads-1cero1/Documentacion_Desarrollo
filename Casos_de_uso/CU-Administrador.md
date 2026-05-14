# Casos de Uso - Administrador

## Actor: Administrador

El administrador es el usuario interno autorizado para ingresar al backoffice de All Roads.  
En el MVP, su alcance está limitado a iniciar sesión, recuperar contraseña y consultar reservas generadas desde el portal en modo solo lectura.

El administrador no podrá crear, editar o eliminar tours, modificar reservas, cambiar estados, gestionar pagos, aplicar descuentos, consultar dashboards, generar reportes ni administrar notificaciones.

---

## CU-ADM-001 - Iniciar sesión en backoffice

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Administrador |
| **Módulo** | Autenticación / Backoffice |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Permitir que el administrador acceda al backoffice de All Roads mediante usuario y contraseña.

### Precondiciones

- El administrador debe estar registrado en el sistema.
- El backoffice debe estar disponible.
- El administrador debe contar con usuario y contraseña válidos.

### Flujo principal

1. El administrador ingresa al portal de All Roads.
2. El administrador selecciona el botón de **Login** ubicado en la parte superior derecha.
3. El sistema muestra la pantalla de inicio de sesión.
4. El administrador ingresa usuario y contraseña.
5. El sistema valida las credenciales.
6. Si las credenciales son correctas, el sistema autentica al administrador.
7. El sistema redirige al administrador al módulo de **Reservas**.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | Credenciales incorrectas | El sistema muestra un mensaje indicando que los datos no son válidos. |
| **FA-02** | Campos vacíos | El sistema solicita completar usuario y contraseña. |
| **FA-03** | Usuario no autorizado | El sistema bloquea el acceso al backoffice. |

### Criterios de aceptación

- El administrador puede acceder al login desde el portal.
- El sistema valida usuario y contraseña.
- Si la autenticación es correcta, el administrador entra al módulo de Reservas.
- Si la autenticación falla, el sistema no permite el acceso.

---

## CU-ADM-002 - Proteger rutas administrativas

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Administrador |
| **Módulo** | Seguridad / Backoffice |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Garantizar que solo usuarios administrativos autenticados puedan acceder a las rutas del backoffice.

### Precondiciones

- El backoffice debe tener rutas protegidas.
- El sistema debe poder validar si existe una sesión activa.

### Flujo principal

1. El administrador intenta acceder a una ruta del backoffice.
2. El sistema verifica si existe una sesión activa.
3. Si el administrador está autenticado, el sistema permite el acceso.
4. Si no está autenticado, el sistema redirige al login.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | Sesión expirada | El sistema redirige al login. |
| **FA-02** | Usuario intenta acceder por URL directa | El sistema valida autenticación antes de mostrar la vista. |

### Criterios de aceptación

- Ninguna ruta administrativa debe estar disponible sin autenticación.
- El sistema debe redirigir al login cuando no exista sesión válida.
- El administrador autenticado puede acceder únicamente a las vistas permitidas del MVP.

---

## CU-ADM-003 - Consultar listado de reservas

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Administrador |
| **Módulo** | Reservas |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Permitir que el administrador consulte las reservas generadas desde el portal público.

### Precondiciones

- El administrador debe estar autenticado.
- Deben existir reservas registradas o el sistema debe manejar el estado vacío.
- El módulo de Reservas debe estar disponible.

### Flujo principal

1. El administrador inicia sesión correctamente.
2. El sistema lo redirige al módulo de **Reservas**.
3. El sistema muestra el listado de reservas generadas desde el portal.
4. Por cada reserva, el sistema muestra información básica para identificarla.
5. El administrador revisa la información disponible.
6. El administrador puede seleccionar una reserva para consultar su detalle.

### Información mínima a visualizar

| Dato | Descripción |
| :--- | :--- |
| **Nombre del comprador** | Persona que realizó la reserva. |
| **Datos de contacto** | Correo, teléfono u otros datos registrados. |
| **Fecha de creación** | Fecha en la que se generó la reserva. |
| **Tours seleccionados** | Tours incluidos en la compra. |
| **Cantidades** | Cantidad de personas por tour. |
| **Valor total** | Total calculado de la reserva. |
| **Estado de la orden** | Estado general de la reserva. |
| **Estado del pago** | Estado asociado al pago. |

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | No existen reservas | El sistema muestra un mensaje indicando que no hay reservas registradas. |
| **FA-02** | Error al cargar reservas | El sistema muestra un mensaje controlado y permite reintentar. |

### Criterios de aceptación

- El administrador autenticado puede visualizar el listado de reservas.
- El sistema muestra información básica de cada reserva.
- El administrador no puede editar ni eliminar reservas desde el listado.
- El listado debe funcionar correctamente en escritorio y resoluciones menores.

---

## CU-ADM-004 - Consultar detalle de reserva

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Administrador |
| **Módulo** | Reservas |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Permitir que el administrador consulte en modo lectura la información completa de una reserva.

### Precondiciones

- El administrador debe estar autenticado.
- La reserva debe existir.
- El administrador debe acceder desde el listado de reservas.

### Flujo principal

1. El administrador ingresa al módulo de Reservas.
2. El administrador selecciona una reserva del listado.
3. El sistema muestra el detalle de la reserva.
4. El administrador consulta los datos registrados por el visitante.
5. El sistema muestra la información de compra, tours, cantidades, acompañantes si aplica, estados y observaciones.
6. El administrador regresa al listado de reservas si lo requiere.

### Información a consultar

| Dato | Descripción |
| :--- | :--- |
| **Datos del comprador** | Nombre y datos personales registrados. |
| **Información de contacto** | Correo, teléfono u otros datos capturados. |
| **Fechas relacionadas** | Fecha de creación o fechas asociadas a la reserva. |
| **Tours adquiridos** | Tours incluidos en la compra. |
| **Cantidad de personas** | Cantidad registrada por cada tour. |
| **Acompañantes** | Información de acompañantes si aplica. |
| **Observaciones** | Datos adicionales suministrados en el formulario. |
| **Estado de orden** | Estado actual de la reserva. |
| **Estado de pago** | Estado actual del pago. |

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | La reserva no existe | El sistema muestra mensaje de no encontrado. |
| **FA-02** | Error al cargar el detalle | El sistema muestra mensaje controlado y permite volver al listado. |

### Criterios de aceptación

- El administrador puede consultar el detalle de una reserva.
- La información se muestra en modo solo lectura.
- El administrador no puede modificar datos de comprador, tours, cantidades, acompañantes, estados ni pagos.
- El administrador puede regresar al listado de reservas.

---

## CU-ADM-005 - Recuperar contraseña

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Administrador |
| **Actor secundario** | Servicio de correo |
| **Módulo** | Autenticación |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Permitir que el administrador inicie el proceso de recuperación de contraseña desde la pantalla de login.

### Precondiciones

- El administrador debe tener un correo registrado.
- El servicio de correo debe estar disponible.
- El administrador debe encontrarse en la pantalla de login.

### Flujo principal

1. El administrador selecciona la opción de recuperar contraseña.
2. El sistema muestra un formulario para ingresar el correo electrónico.
3. El administrador ingresa su correo registrado.
4. El sistema valida que el correo exista.
5. El sistema genera un código de verificación.
6. El sistema envía el código al correo del administrador.
7. El sistema permite continuar a la pantalla de validación del código.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | Correo vacío | El sistema solicita ingresar el correo. |
| **FA-02** | Correo con formato inválido | El sistema solicita corregir el correo. |
| **FA-03** | Correo no registrado | El sistema muestra un mensaje controlado sin permitir continuar. |
| **FA-04** | Error al enviar código | El sistema informa que no fue posible enviar el código y permite reintentar. |

### Criterios de aceptación

- El administrador puede solicitar recuperación desde el login.
- El sistema valida el correo ingresado.
- Si el correo es válido, se envía un código de verificación.
- El sistema no cambia la contraseña en este paso.

---

## CU-ADM-006 - Validar código de recuperación

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Administrador |
| **Módulo** | Autenticación |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Validar el código enviado al correo del administrador antes de permitir el cambio de contraseña.

### Precondiciones

- El administrador debe haber solicitado recuperación de contraseña.
- El sistema debe haber generado y enviado un código.
- El código debe estar vigente.

### Flujo principal

1. El administrador recibe el código de verificación en su correo.
2. El administrador ingresa el código en la pantalla correspondiente.
3. El sistema valida el código.
4. Si el código es correcto, el sistema permite continuar al registro de nueva contraseña.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | Código incorrecto | El sistema informa que el código no es válido. |
| **FA-02** | Código vencido | El sistema solicita iniciar nuevamente la recuperación. |
| **FA-03** | Código vacío | El sistema solicita ingresar el código. |

### Criterios de aceptación

- El administrador solo puede continuar si el código es válido.
- El sistema no permite cambiar contraseña con código incorrecto o vencido.
- El sistema debe mostrar mensajes claros y controlados.

---

## CU-ADM-007 - Registrar nueva contraseña

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Administrador |
| **Módulo** | Autenticación |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Permitir que el administrador registre una nueva contraseña después de validar correctamente el código de recuperación.

### Precondiciones

- El código de recuperación debe haber sido validado correctamente.
- El administrador debe estar en la pantalla de nueva contraseña.

### Flujo principal

1. El sistema muestra el formulario de nueva contraseña.
2. El administrador ingresa la nueva contraseña.
3. El administrador confirma la nueva contraseña.
4. El sistema valida que las contraseñas coincidan.
5. El sistema actualiza la contraseña del administrador.
6. El sistema redirige al administrador nuevamente al login.
7. El administrador puede iniciar sesión con su nueva contraseña.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | Las contraseñas no coinciden | El sistema solicita corregir la confirmación. |
| **FA-02** | Contraseña vacía | El sistema solicita ingresar una contraseña válida. |
| **FA-03** | Error al actualizar contraseña | El sistema muestra mensaje controlado y permite reintentar. |

### Criterios de aceptación

- El administrador puede registrar una nueva contraseña después de validar el código.
- El sistema valida que la contraseña y su confirmación coincidan.
- Después del cambio exitoso, el sistema redirige al login.
- El administrador debe autenticarse nuevamente con la nueva contraseña.

---

## Reglas generales del actor Administrador

| Regla | Descripción |
| :--- | :--- |
| **RN-ADM-001** | El administrador debe autenticarse para acceder al backoffice. |
| **RN-ADM-002** | El backoffice debe tener rutas protegidas. |
| **RN-ADM-003** | En el MVP, el menú administrativo solo tendrá disponible la vista de Reservas. |
| **RN-ADM-004** | El administrador solo puede consultar reservas en modo lectura. |
| **RN-ADM-005** | El administrador no puede editar, eliminar, cambiar estados ni gestionar reservas. |
| **RN-ADM-006** | El administrador no puede modificar pagos desde el backoffice. |
| **RN-ADM-007** | La administración de tours queda fuera del MVP. |
| **RN-ADM-008** | Dashboard, reportes, logs, cupones y notificaciones quedan fuera del MVP. |
| **RN-ADM-009** | La recuperación de contraseña se realiza mediante correo, código de verificación y nueva contraseña. |

---

## Restricciones del MVP

Las siguientes acciones no estarán disponibles para el administrador en esta fase:

| Acción | Estado en MVP |
| :--- | :--- |
| Crear tours | No incluido |
| Editar tours | No incluido |
| Activar o desactivar tours | No incluido |
| Editar reservas | No incluido |
| Eliminar reservas | No incluido |
| Cambiar estados de reservas | No incluido |
| Modificar pagos | No incluido |
| Agregar acompañantes manualmente | No incluido |
| Aplicar descuentos | No incluido |
| Consultar dashboard ejecutivo | No incluido |
| Exportar reportes | No incluido |
| Ver logs de auditoría | No incluido |
| Administrar notificaciones | No incluido |

---

## Casos de uso relacionados

| Código | Nombre |
| :--- | :--- |
| **CU-VIS-007** | Crear orden/reserva previa al pago |
| **CU-VIS-008** | Realizar pago en pasarela |
| **CU-VIS-009** | Visualizar resultado del pago |
| **CU-VIS-010** | Recibir confirmación de reserva |
| **CU-SC-002** | Enviar código de recuperación de contraseña |
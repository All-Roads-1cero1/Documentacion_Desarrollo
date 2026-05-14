# Casos de Uso - Visitante

## Actor: Visitante

El visitante es el usuario público que ingresa al portal de All Roads para consultar tours, revisar detalles, agregar experiencias al carrito, diligenciar una reserva y realizar el pago mediante la pasarela de pagos.

En el MVP, el visitante no requiere registro ni inicio de sesión para navegar el portal o iniciar una reserva.

---

## CU-VIS-001 - Consultar home del portal

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Visitante |
| **Módulo** | Portal público |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Permitir que el visitante ingrese al portal de All Roads y visualice la información principal de la marca, el video inicial, la presentación de la entidad, tours o parches destacados, aliados y footer.

### Precondiciones

- El portal debe estar disponible.
- La información del home debe estar cargada o definida de forma estática.
- El visitante debe contar con conexión a internet.

### Flujo principal

1. El visitante ingresa a la URL principal del portal.
2. El sistema carga el home público.
3. El sistema muestra el video principal o recurso visual destacado.
4. El sistema muestra información general de All Roads.
5. El sistema presenta tours, parches destacados o accesos hacia la oferta disponible.
6. El sistema muestra aliados y footer.
7. El visitante puede continuar hacia la sección de tours o “Nuestros Parches”.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | El video principal no carga | El sistema mantiene visible el home y puede mostrar una imagen o espacio alternativo. |
| **FA-02** | No hay tours destacados disponibles | El sistema oculta la sección o muestra un mensaje controlado sin afectar la navegación. |

### Criterios de aceptación

- El visitante puede acceder al home sin autenticarse.
- El home muestra la información principal definida para el MVP.
- El visitante puede navegar hacia el listado de tours.
- El diseño debe funcionar correctamente en escritorio, tablet y móvil.

---

## CU-VIS-002 - Consultar listado de tours

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Visitante |
| **Módulo** | Portal público / Tours |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Permitir que el visitante consulte los tours o parches disponibles en el portal.

### Precondiciones

- El portal debe estar disponible.
- Debe existir información precargada o estática de los tours.
- El visitante debe haber ingresado al portal.

### Flujo principal

1. El visitante selecciona la opción “Nuestros Parches” o accede al listado de tours.
2. El sistema muestra una introducción de la sección.
3. El sistema lista los tours disponibles.
4. Cada tour muestra información básica como imagen, nombre, descripción corta y acción para ver detalle.
5. El visitante revisa la oferta disponible.
6. El visitante selecciona un tour para consultar más información.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | No hay tours disponibles | El sistema muestra un mensaje informativo. |
| **FA-02** | Una imagen no carga | El sistema muestra una imagen alternativa o conserva la tarjeta sin romper el diseño. |

### Criterios de aceptación

- El visitante puede ver el listado sin iniciar sesión.
- Cada tour debe mostrar información básica.
- El visitante puede acceder al detalle de un tour.
- El listado debe ser responsive.

---

## CU-VIS-003 - Consultar detalle de tour

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Visitante |
| **Módulo** | Portal público / Detalle de tour |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Permitir que el visitante consulte la información completa de un tour antes de agregarlo al carrito.

### Precondiciones

- El tour debe existir dentro de la información precargada del MVP.
- El visitante debe acceder desde el listado o desde un enlace válido.

### Flujo principal

1. El visitante selecciona un tour desde el listado.
2. El sistema abre la vista de detalle del tour.
3. El sistema muestra nombre, descripción, imágenes relacionadas, lugares a recorrer, qué incluye y precio.
4. El sistema puede mostrar tours similares si están definidos.
5. El visitante revisa la información.
6. El visitante puede agregar el tour al carrito.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | El tour no existe o la ruta es inválida | El sistema muestra una pantalla o mensaje de no encontrado. |
| **FA-02** | No hay tours similares | El sistema oculta esa sección o muestra solo el detalle principal. |

### Criterios de aceptación

- El detalle muestra la información principal del tour.
- El visitante puede regresar al listado.
- El visitante puede agregar el tour al carrito.
- El sistema no debe validar cupos reales en el MVP.

---

## CU-VIS-004 - Agregar tour al carrito

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Visitante |
| **Módulo** | Carrito |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Permitir que el visitante agregue uno o varios tours al carrito y defina la cantidad de personas por cada tour.

### Precondiciones

- El visitante debe estar en el detalle de un tour.
- El tour debe tener precio definido.
- El carrito debe estar disponible.

### Flujo principal

1. El visitante selecciona la opción para agregar el tour al carrito.
2. El sistema agrega el tour seleccionado.
3. El sistema permite definir o modificar la cantidad de personas para ese tour.
4. El sistema calcula el subtotal del tour.
5. El visitante puede continuar explorando o ir al carrito.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | El tour ya está en el carrito | El sistema puede actualizar la cantidad o informar que ya fue agregado. |
| **FA-02** | La cantidad ingresada no es válida | El sistema solicita una cantidad válida mayor a cero. |

### Criterios de aceptación

- El visitante puede agregar uno o varios tours.
- La cantidad de personas se define por cada tour.
- El subtotal se calcula según precio por cantidad.
- No se valida disponibilidad real de cupos en el MVP.

---

## CU-VIS-005 - Revisar y modificar carrito

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Visitante |
| **Módulo** | Carrito |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Permitir que el visitante revise los tours seleccionados, modifique cantidades, elimine tours y consulte el valor total antes de continuar con la reserva.

### Precondiciones

- El visitante debe tener al menos un tour agregado al carrito.

### Flujo principal

1. El visitante ingresa al carrito.
2. El sistema muestra los tours seleccionados.
3. El sistema muestra cantidad de personas por tour.
4. El sistema muestra subtotales y valor total.
5. El visitante puede modificar cantidades.
6. El visitante puede eliminar tours.
7. El sistema actualiza los valores.
8. El visitante continúa al formulario de reserva.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | El carrito está vacío | El sistema muestra un mensaje e invita a consultar tours. |
| **FA-02** | El visitante elimina todos los tours | El sistema deja el carrito vacío y bloquea la continuación a reserva. |

### Criterios de aceptación

- El visitante puede revisar el detalle de su compra.
- El total se actualiza al modificar cantidades.
- El visitante no puede continuar sin tours en el carrito.
- El carrito permite más de un tour en la misma compra.

---

## CU-VIS-006 - Diligenciar formulario de reserva

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Visitante |
| **Módulo** | Reserva |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Capturar la información necesaria del comprador para crear la reserva u orden antes de iniciar el pago.

### Precondiciones

- El visitante debe tener tours en el carrito.
- El valor total debe estar calculado.
- El formulario de reserva debe estar disponible.

### Flujo principal

1. El visitante continúa desde el carrito al formulario de reserva.
2. El sistema muestra los campos requeridos.
3. El visitante diligencia sus datos personales y de contacto.
4. El visitante completa la información adicional solicitada.
5. El sistema valida los campos obligatorios.
6. El visitante acepta términos y condiciones.
7. El sistema habilita la acción para continuar al pago.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | Faltan campos obligatorios | El sistema indica los campos pendientes. |
| **FA-02** | El correo tiene formato inválido | El sistema solicita corregir el correo. |
| **FA-03** | No acepta términos y condiciones | El sistema mantiene deshabilitado el botón de pago. |

### Criterios de aceptación

- El visitante no puede continuar sin completar los campos obligatorios.
- El botón de pago solo se habilita al aceptar términos y condiciones.
- La información diligenciada queda asociada a la reserva.
- No se requiere cuenta de usuario para reservar.

---

## CU-VIS-007 - Crear orden/reserva previa al pago

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Visitante |
| **Actor secundario** | Sistema All Roads |
| **Módulo** | Reserva / Pago |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Crear una orden o reserva previa en estado pendiente antes de redirigir al visitante a la pasarela de pagos.

### Precondiciones

- El carrito debe tener al menos un tour.
- El formulario de reserva debe estar completo.
- El visitante debe haber aceptado términos y condiciones.

### Flujo principal

1. El visitante selecciona la opción para continuar al pago.
2. El sistema valida la información de reserva.
3. El sistema crea una orden/reserva en estado pendiente.
4. El sistema registra el intento de pago interno como creado o pendiente.
5. El sistema prepara la redirección hacia la pasarela de pagos.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | Error al crear la reserva | El sistema informa que no fue posible continuar y permite reintentar. |
| **FA-02** | El carrito cambió o está vacío | El sistema bloquea la creación y solicita revisar el carrito. |

### Criterios de aceptación

- La reserva se crea antes de iniciar el pago.
- La reserva queda en estado pendiente.
- El intento de pago queda registrado para trazabilidad.
- El visitante solo puede continuar si la información es válida.

---

## CU-VIS-008 - Realizar pago en pasarela

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Visitante |
| **Actor secundario** | Pasarela de pagos |
| **Módulo** | Pagos |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Permitir que el visitante sea redirigido a la pasarela de pagos para completar el pago de la reserva.

### Precondiciones

- Debe existir una orden/reserva pendiente.
- Debe existir un intento de pago registrado.
- La pasarela de pagos debe estar disponible.

### Flujo principal

1. El sistema redirige al visitante a la pasarela de pagos.
2. El visitante completa el proceso de pago en la pasarela.
3. La pasarela procesa la transacción.
4. La pasarela retorna o notifica el resultado.
5. El sistema actualiza el estado del pago y de la reserva según corresponda.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | Pago aprobado | La reserva queda pagada y se habilita confirmación. |
| **FA-02** | Pago rechazado | La reserva no queda confirmada como pagada. |
| **FA-03** | Error técnico | El pago queda fallido. |
| **FA-04** | El tiempo vence | El pago queda expirado. |
| **FA-05** | No llega confirmación | El sistema conserva trazabilidad y el usuario deberá reintentar cuando el intento finalice o venza. |

### Criterios de aceptación

- El sistema no captura datos sensibles de tarjeta.
- El pago ocurre en la pasarela de pagos.
- La reserva se actualiza según el resultado recibido.
- El tiempo de vigencia del pago corresponde al definido por la pasarela.

---

## CU-VIS-009 - Visualizar resultado del pago

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Visitante |
| **Módulo** | Resultado de pago |
| **Prioridad** | Alta |
| **Estado MVP** | Incluido |

### Objetivo

Mostrar al visitante el resultado del proceso de pago después del retorno o respuesta de la pasarela.

### Precondiciones

- El visitante debe haber iniciado un proceso de pago.
- El sistema debe recibir o consultar el resultado disponible de la transacción.

### Flujo principal

1. El visitante finaliza el proceso en la pasarela.
2. El sistema recibe el retorno o resultado del pago.
3. El sistema identifica el estado de la transacción.
4. El sistema muestra una pantalla de resultado.
5. El visitante visualiza si el pago fue exitoso, rechazado, pendiente, expirado o fallido.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | Resultado aprobado | El sistema informa que la reserva fue pagada correctamente. |
| **FA-02** | Resultado rechazado | El sistema informa que el pago fue rechazado. |
| **FA-03** | Resultado pendiente | El sistema informa que la transacción está pendiente. |
| **FA-04** | Resultado fallido o error | El sistema informa que no fue posible completar el pago. |

### Criterios de aceptación

- El visitante recibe una respuesta clara del estado del pago.
- El sistema no muestra información técnica interna.
- Si el pago es aprobado, la reserva queda marcada como pagada.
- Si el pago no se confirma, el sistema conserva trazabilidad del intento.

---

## CU-VIS-010 - Recibir confirmación de reserva

| Campo | Descripción |
| :--- | :--- |
| **Actor principal** | Visitante |
| **Actor secundario** | Servicio de correo |
| **Módulo** | Confirmación |
| **Prioridad** | Media |
| **Estado MVP** | Incluido |

### Objetivo

Enviar al visitante un correo de confirmación cuando el pago sea aprobado y la reserva quede en estado pagado.

### Precondiciones

- La reserva debe existir.
- El pago debe estar aprobado.
- El correo del comprador debe estar registrado correctamente.
- El servicio de correo debe estar disponible.

### Flujo principal

1. El sistema confirma que el pago fue aprobado.
2. El sistema actualiza la reserva como pagada.
3. El sistema solicita el envío del correo de confirmación.
4. El servicio de correo envía la confirmación al comprador.
5. El visitante recibe el correo con la información básica de la reserva.

### Flujos alternos

| Código | Situación | Resultado |
| :--- | :--- | :--- |
| **FA-01** | El correo no puede enviarse | El sistema conserva la reserva pagada y registra el intento de envío. |
| **FA-02** | El correo del visitante es inválido | El sistema no puede entregar la confirmación, pero la reserva conserva su estado. |

### Criterios de aceptación

- El correo solo se envía cuando el pago está aprobado.
- El correo contiene información básica de la reserva.
- La reserva no depende del envío del correo para quedar pagada.
- El sistema debe conservar trazabilidad del intento de envío.

---

## Reglas generales del actor Visitante

| Regla | Descripción |
| :--- | :--- |
| **RN-VIS-001** | El visitante puede navegar el portal sin iniciar sesión. |
| **RN-VIS-002** | Una compra puede contener uno o varios tours. |
| **RN-VIS-003** | La cantidad de personas se define por cada tour. |
| **RN-VIS-004** | El total se calcula con base en precio del tour por cantidad de personas. |
| **RN-VIS-005** | El pago solo se habilita cuando el visitante acepta términos y condiciones. |
| **RN-VIS-006** | Antes de iniciar el pago se crea una orden/reserva pendiente. |
| **RN-VIS-007** | El sistema no captura datos sensibles de tarjeta. |
| **RN-VIS-008** | Si el pago no se confirma, se conserva trazabilidad y el visitante deberá reintentar una vez finalizado o vencido el intento anterior. |
| **RN-VIS-009** | El correo de confirmación se envía cuando el pago queda aprobado. |
| **RN-VIS-010** | El MVP no contempla validación real de cupos, cupones ni disponibilidad por fecha. |

---

## Casos de uso relacionados

| Código | Nombre |
| :--- | :--- |
| **CU-PP-001** | Redirigir usuario a pasarela de pagos |
| **CU-PP-002** | Procesar resultado de pago |
| **CU-SC-001** | Enviar correo de confirmación |
| **CU-ADM-005** | Consultar listado de reservas |
| **CU-ADM-006** | Consultar detalle de reserva |
# All Roads | Desarrollo Fase 1 - MVP

Bienvenido al repositorio de documentación técnica y funcional de **All Roads** en su fase de desarrollo MVP.

Este espacio centraliza la información necesaria para entender el alcance del proyecto, los flujos principales, actores del sistema, reglas de negocio, casos de uso, diagramas y lineamientos definidos para la primera entrega.

---

## Información general del MVP

| Dato | Valor |
| :--- | :--- |
| **Proyecto** | All Roads |
| **Fase** | Desarrollo Fase 1 - MVP |
| **Inicio del MVP** | 11 de mayo de 2026 |
| **Entrega del MVP** | 15 de julio de 2026 |
| **Pruebas QA final** | 13 al 15 de julio de 2026 |
| **Pasarela** | Pasarela de pagos |
| **Stack técnico** | Portal Vue, Backoffice Vue, Backend NestJS y PostgreSQL |

---

## Resumen del producto

All Roads es un portal web orientado a la consulta, selección, reserva y pago de tours o experiencias turísticas.

En el MVP, el visitante podrá navegar el portal, consultar tours disponibles, agregar uno o varios tours al carrito, indicar la cantidad de personas por tour, diligenciar sus datos de reserva, aceptar términos y condiciones, realizar el pago mediante una pasarela de pagos y visualizar el resultado del proceso.

El administrador contará con un backoffice básico para ingresar con credenciales, recuperar contraseña y consultar reservas en modo solo lectura.

---

## Principio de gestión del MVP

Toda funcionalidad que no sea necesaria para completar el flujo de:

**consulta → carrito → reserva → pago → confirmación → consulta administrativa de reservas**

debe mantenerse fuera del MVP o clasificarse como parte de una fase posterior de desarrollo.

---

## Alcance del MVP

### Portal público

| Elemento | Detalle |
| :--- | :--- |
| **Home** | Video principal, información de la entidad, recuento de tours destacados o más consultados, aliados y footer. |
| **Listado de tours** | Visualización de tours disponibles con información precargada o estática. |
| **Detalle de tour** | Nombre, descripción, imágenes relacionadas, lugares a recorrer, qué incluye, precio, tours similares y acción para agregar al carrito. |
| **Carrito** | Permite agregar uno o varios tours en la misma compra y definir cantidad de personas por tour. |
| **Formulario de reserva** | Captura los datos requeridos para crear la reserva u orden. |
| **Términos y condiciones** | El botón de pago solo se habilita cuando el usuario acepta términos y condiciones. |
| **Pago** | Redirección a la pasarela de pagos y procesamiento de la respuesta del pago. |
| **Resultado** | Pantalla de aprobación, rechazo, pendiente, expirado o error según la respuesta del sistema. |
| **Correo de confirmación** | Envío de correo al comprador cuando el pago/reserva alcance un estado definido. |

---

### Backoffice administrativo

| Elemento | Detalle |
| :--- | :--- |
| **Login** | Acceso al panel administrativo mediante usuario y contraseña. |
| **Recuperación de contraseña** | Flujo de recuperación para usuarios administradores mediante correo, código de verificación y nueva contraseña. |
| **Layout administrativo** | Estructura base del panel con header, menú y componentes estáticos. |
| **Protección de rutas** | Acceso restringido únicamente a usuarios autenticados. |
| **Reservas solo lectura** | Listado y detalle básico de reservas. No permite edición, eliminación, cambio de estado ni gestión operativa. |

---

## Qué no incluye el MVP

| Frente | Fuera del MVP |
| :--- | :--- |
| **Portal** | Contenido dinámico administrable desde backoffice. |
| **Portal** | Creación, edición, activación o desactivación de tours desde el panel administrativo. |
| **Portal** | Galería de imágenes avanzada o administración dinámica de imágenes. |
| **Portal** | Control real de cupos, inventario o disponibilidad por fecha. |
| **Portal** | Cupones, tarifas por temporada, descuentos configurables o reglas comerciales avanzadas. |
| **Backoffice** | Dashboard ejecutivo, gráficas, métricas, tours populares y actividad reciente. |
| **Backoffice** | Apartado de edición de tours. |
| **Backoffice** | Gestión o edición de reservas, cambios de estado, observaciones, reagendamientos o eliminación. |
| **Backoffice** | Logs de auditoría visibles, exportaciones, notificaciones administrables y reportes. |

---

## Fase de desarrollo 2

Las siguientes funcionalidades quedan proyectadas para una fase posterior:

| Módulo | Alcance fase 2 |
| :--- | :--- |
| **Edición de tours** | Crear, editar, activar, desactivar y administrar tours publicados en el portal, incluyendo imágenes, precios y contenido. |
| **Disponibilidad y cupos** | Configurar fechas, cupos reales por tour y reglas de disponibilidad. |
| **Gestión avanzada de reservas** | Editar campos permitidos, cambiar estados, reagendar, agregar observaciones y reenviar comprobantes. |
| **Galería de imágenes** | Creación y administración dinámica de galería de imágenes. |
| **Dashboard** | Resumen ejecutivo, métricas, gráficos, tours populares, recaudo y actividad reciente. |
| **Logs y auditoría** | Registro de acciones sobre portal y backoffice. |
| **Cupones** | Creación, personalización, activación/desactivación y aplicación de descuentos por valor fijo o porcentaje. |
| **Reportes** | Exportaciones, filtros avanzados y reportes administrativos. |
| **Notificaciones** | Gestión centralizada de plantillas, reenvíos y eventos. |

---

## Flujo principal del visitante

1. El visitante ingresa al home de All Roads.
2. Explora la sección de tours o “Nuestros Parches”.
3. Consulta el detalle de uno o varios tours.
4. Agrega tours al carrito.
5. Define la cantidad de personas por cada tour.
6. Revisa el carrito, subtotales y valor total.
7. Diligencia los datos requeridos para la reserva.
8. Acepta términos y condiciones.
9. El sistema crea una orden/reserva previa en estado pendiente.
10. El usuario es redirigido a la pasarela de pagos.
11. El sistema actualiza los estados según la respuesta del pago.
12. El visitante visualiza el resultado: exitoso, rechazado, pendiente, expirado o fallido.
13. Si el pago es aprobado, se envía correo de confirmación.
14. La reserva queda disponible para consulta administrativa en el backoffice.

---

## Flujo del administrador

1. El administrador accede desde el botón de Login ubicado en la parte superior derecha del portal.
2. Ingresa usuario y contraseña.
3. El sistema valida las credenciales.
4. Si son correctas, el administrador accede al módulo de Reservas.
5. El backoffice tendrá rutas protegidas para usuarios autenticados.
6. En el MVP, el menú solo tendrá disponible la vista de **Reservas**.
7. El administrador podrá consultar el listado de reservas generadas desde el portal.
8. El administrador podrá ingresar al detalle de una reserva.
9. La información será únicamente de consulta.
10. No se permite editar datos, eliminar reservas, cambiar estados, modificar pagos, agregar acompañantes, aplicar descuentos ni realizar acciones operativas.
11. Si olvida su contraseña, podrá recuperarla mediante correo, código de verificación y registro de nueva contraseña.

---

## Reglas de negocio

| Regla | Definición |
| :--- | :--- |
| **Tours en compra** | Una compra puede contener uno o varios tours. |
| **Cantidad de personas** | La cantidad se define por cada tour dentro del carrito. |
| **Precio total** | El total se calcula por precio de tour multiplicado por cantidad de personas y acumulado por todos los tours. |
| **Términos y condiciones** | El pago solo se habilita con aceptación de términos y condiciones. |
| **Orden previa al pago** | Antes de iniciar la pasarela se crea una orden/reserva válida en estado pendiente. |
| **Pago** | El sistema no captura datos sensibles de tarjeta; el proceso ocurre en la pasarela de pagos. |
| **Confirmación** | El estado definitivo se actualiza según respuesta o retorno de la pasarela de pagos. |
| **Transacción no confirmada** | Si la transacción no funciona, queda pendiente, falla el retorno, no llega la confirmación de la pasarela o existe alguna inconsistencia, el sistema conservará trazabilidad del intento de pago. En el alcance del MVP no se contempla reconciliación automática; por lo tanto, una vez finalizado o vencido el intento anterior, se debe volver a intentar el proceso de pago. |
| **Correo** | El correo de confirmación hace parte del MVP. |
| **Backoffice** | El administrador solo visualiza reservas. La gestión queda para fase 2. |

---

## Estados del pago y reserva

| Evento | Resultado esperado |
| :--- | :--- |
| **Pago aprobado** | Reserva pagada y envío de correo de confirmación. |
| **Pago rechazado** | Pago rechazado sin confirmación de reserva pagada. |
| **Error técnico** | Pago fallido. |
| **Tiempo vencido** | Pago expirado. |
| **Transacción sin confirmación** | Permanece pendiente hasta finalizar o vencer el intento. Luego se debe volver a intentar el proceso de pago. |

---

## Tiempo de vigencia del pago

El tiempo disponible para completar el pago y mantener la orden/reserva pendiente será el estipulado por la pasarela de pagos:

**30 minutos**

---


## Casos de uso

En esta sección se listan los documentos de casos de uso del sistema.

| Actor | Documentación |
| :--- | :--- |
| **Administrador** | [Casos de Uso - Administrador](https://github.com/All-Roads-1cero1/Documentacion_Desarrollo/blob/main/Casos_de_uso/Casos-de-Uso-Administrador.pdf) |
| **Visitante** | [Casos de Uso - Visitante](https://github.com/All-Roads-1cero1/Documentacion_Desarrollo/blob/main/Casos_de_uso/Casos-de-Uso-Visitante.pdf) |
| **Pasarela de Pago** | [Casos de Uso - Pasarela Pago](https://github.com/All-Roads-1cero1/Documentacion_Desarrollo/blob/main/Casos_de_uso/Casos-de-Uso-Pasarela-Pago.pdf) |
| **Servicio de Correo** | [Casos de Uso - Servicio Correo](https://github.com/All-Roads-1cero1/Documentacion_Desarrollo/blob/main/Casos_de_uso/Casos-de-Uso-Servicio-Correo.pdf) |

---

## Diagramas

### Modelo de base de datos

Esta sección presenta el modelo de tablas de la base de datos del proyecto.

![Modelo DB](https://github.com/All-Roads-1cero1/Documentacion_Desarrollo/blob/main/model_db.svg)

Puedes acceder a la imagen en alta resolución aquí:

[Ver modelo de base de datos](https://github.com/All-Roads-1cero1/Documentacion_Desarrollo/blob/main/model_db.svg)

---

## Actores clave del sistema

### Visitante

| Aspecto | Descripción |
| :--- | :--- |
| **Rol principal** | Usuario público que navega el portal para explorar, reservar y pagar tours sin requerir cuenta. |
| **Responsabilidades** | Explorar tours, revisar detalles, agregar tours al carrito, definir cantidades, diligenciar datos de reserva, aceptar términos y completar el pago. |
| **Nivel de acceso** | Público sin autenticación. |
| **Interacciones externas** | Pasarela de pagos y servicio de correo. |

---

### Administrador

| Aspecto | Descripción |
| :--- | :--- |
| **Rol principal** | Usuario interno que accede al backoffice para consultar reservas generadas desde el portal. |
| **Responsabilidades** | Iniciar sesión, recuperar contraseña y consultar listado/detalle de reservas en modo solo lectura. |
| **Nivel de acceso** | Autenticado mediante credenciales administrativas. |
| **Restricción MVP** | No puede editar reservas, cambiar estados, gestionar pagos, administrar tours, aplicar descuentos ni acceder a módulos avanzados. |

---

### Pasarela de pagos

| Aspecto | Descripción |
| :--- | :--- |
| **Rol principal** | Servicio externo encargado de procesar el pago de las reservas. |
| **Responsabilidades** | Recibir al usuario para completar el pago, procesar la transacción y retornar/notificar el resultado. |
| **Nivel de acceso** | Integración mediante redirección, API o webhook según implementación. |
| **Restricción MVP** | No se capturan datos sensibles de tarjeta dentro del sistema All Roads. |

---

### Servicio de correo

| Aspecto | Descripción |
| :--- | :--- |
| **Rol principal** | Servicio encargado de enviar correos transaccionales al comprador. |
| **Responsabilidades** | Enviar correo de confirmación cuando el pago/reserva alcance el estado definido. |
| **Nivel de acceso** | Integración SMTP/API con credenciales seguras. |
| **Interacción principal** | Backend de All Roads y comprador final. |

---

## Nota de control

Este repositorio documenta el alcance del MVP de All Roads.  
Cualquier cambio funcional o técnico debe pasar por priorización, control de alcance y validación del equipo responsable.
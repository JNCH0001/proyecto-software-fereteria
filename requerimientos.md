# Especificación de requerimientos de software

## Sistema de gestión de inventario y pedidos anticipados - Ferretería KateRey

Basado en IEEE 830-1998  
Versión 1.0 · 24 de noviembre de 2026  

---

## 1. Introducción

### 1.1 Propósito
El presente documento establece la especificación formal de los requerimientos funcionales y no funcionales para el desarrollo del sistema web de gestión de inventario y pedidos anticipados de la Ferretería KateRey. Su finalidad es definir con precisión los criterios contractuales y de ingeniería de software que permitirán verificar y evaluar objetivamente la conformidad del producto final previo a su despliegue en producción.

### 1.2 Alcance
El sistema comprende el registro y actualización de productos, la consulta rápida de existencias disponibles en mostrador, el registro de ventas directas con descuento automático de stock, el control y seguimiento de pedidos anticipados asegurados mediante adelanto económico (Bs 100 de referencia), la bandeja cronológica de compromisos pendientes y la generación de respaldos periódicos de la base de datos en volcado SQL.

Conforme a las delimitaciones establecidas en la propuesta aprobada, quedan explícitamente excluidos del alcance:
- Facturación electrónica computarizada con el Servicio de Impuestos Nacionales (SIN), dado que el negocio opera bajo el Régimen Tributario Simplificado.
- Módulo de compras a proveedores y cuentas por pagar.
- Integración con pasarelas de pago digitales o servicios de mensajería API de pago (WhatsApp Business API o SMS masivos).
- Sincronización multi-sucursal distribuida (la ferretería opera en una sede comercial única).

### 1.3 Definiciones

| Término | Significado unívoco en este documento |
|---|---|
| **Existencia / Stock** | Cantidad física real de un artículo registrada en el sistema y disponible para venta inmediata en mostrador sin compromiso previo. |
| **Pedido anticipado** | Compromiso formal de reserva de materiales acordado entre el dependiente y el comprador, respaldado por un adelanto monetario y una fecha pactada de recojo. |
| **Adelanto** | Monto económico parcial entregado por el cliente en el momento del encargo para asegurar la separación de los materiales. |
| **Saldo** | Importe monetario restante que el comprador debe cancelar al momento de la entrega efectiva del material (*Saldo = Precio total - Adelanto*). |
| **Pendiente** | Estado de un pedido anticipado cuya fecha comprometida está vigente o por cumplirse, y cuyos materiales aún no han sido retirados del establecimiento. |
| **Entregado** | Estado final de un pedido anticipado cuando el cliente recoge la totalidad de la mercadería, cancela el saldo restante y se da por cerrada la transacción. |
| **Operador** | Usuario con credenciales de acceso que atiende en el mostrador de la ferretería (propietario o dependiente familiar). |

### 1.4 Referencias
- Propuesta formal de proyecto integrador: [propuesta.md](file:///c:/Users/LENOVO%20AMD%20Ryzen%203/OneDrive/Escritorio/PS_FERETERIA/propuesta.md).
- Instrumento de recolección de información y trabajo de campo: [instrumento.md](file:///c:/Users/LENOVO%20AMD%20Ryzen%203/OneDrive/Escritorio/PS_FERETERIA/instrumento.md).
- Marco teórico y estado del arte: [marco_teorico.md](file:///c:/Users/LENOVO%20AMD%20Ryzen%203/OneDrive/Escritorio/PS_FERETERIA/marco_teorico.md).
- IEEE Std 830-1998: *IEEE Recommended Practice for Software Requirements Specifications*.

---

## 2. Requerimientos funcionales

| Id | Declaración del requerimiento | Prioridad | Origen / Trazabilidad |
|---|---|:---:|---|
| **RF-01** | El sistema **debe** permitir consultar el catálogo de productos y existencias disponibles mediante un buscador por nombre o código con respuesta inmediata. | Alta | Problema central y Observación 18/11 (demoras de 3 a 5 min al patio). |
| **RF-02** | El sistema **debe** permitir registrar ventas directas de mostrador deduciendo de forma automática la cantidad vendida del stock disponible. | Alta | Objetivo específico 2 y Alcance 2 de la propuesta. |
| **RF-03** | El sistema **debe** impedir el registro de una venta directa si la cantidad solicitada supera las existencias físicas registradas. | Alta | Diagnóstico de campo (evitar comprometer stock inexistente). |
| **RF-04** | El sistema **debe** permitir registrar pedidos anticipados capturando: cliente, celular, producto, cantidad, adelanto recibido y fecha convenida de entrega. | Alta | Problema central y Objetivo específico 2. |
| **RF-05** | El sistema **debe** calcular y registrar automáticamente el saldo restante por cobrar al momento de asentar el anticipo económico. | Alta | Observación 18/11 (errores aritméticos en anotaciones del cuaderno). |
| **RF-06** | El sistema **debe** rechazar el registro de un pedido si falta el nombre del cliente, el celular de contacto, la fecha de entrega o si el adelanto es menor o igual a cero. | Alta | Revisión documental 18/11 (42% de pedidos sin celular y sin fecha límite). |
| **RF-07** | El sistema **debe** listar los pedidos pendientes ordenados cronológicamente por la fecha de entrega más próxima. | Alta | Observación 18/11 (búsqueda reactiva hojeando 3 a 4 páginas atrás). |
| **RF-08** | El sistema **debe** permitir marcar un pedido como entregado, registrando la fecha de despacho y confirmando la cancelación del saldo pendiente. | Alta | Ciclo de vida del pedido y Objetivo específico 3. |
| **RF-09** | El sistema **debe** generar y descargar una copia de respaldo completa de la base de datos en formato de volcado SQL (.sql) desde el panel administrativo. | Alta | Causa raíz 4 y Objetivo específico 4 (riesgo de pérdida física del cuaderno). |
| **RF-10** | El sistema **debe** presentar en la pantalla principal un resumen numérico de los pedidos comprometidos para entrega en la fecha en curso. | Media | Entrevista 18/11 (necesidad de conocer al inicio del día los pedidos a despachar). |
| **RF-11** | El sistema **debería** permitir filtrar el historial de pedidos completados por rango de fechas para arqueo de entregas. | Baja | Solicitud complementaria de administración en mostrador. |

---

## 3. Requerimientos no funcionales

| Id | Requerimiento / Métrica | Criterio de verificación objetiva (Pasa / Falla) |
|---|---|---|
| **RNF-01** | **Tiempo de registro operativo:** El asentamiento de un pedido anticipado **debe** completarse en un tiempo no mayor a **45 segundos** por un operador previamente capacitado. | Cronometrar tres registros consecutivos en mostrador; pasa si el promedio es ≤ 45 segundos. |
| **RNF-02** | **Simplicidad de interfaz:** El formulario web de pedido anticipado **debe** contener a lo sumo **cinco campos de entrada obligatorios**. | Contar los campos con atributo `required` en el formulario HTML; pasa si son ≤ 5. |
| **RNF-03** | **Adaptabilidad móvil responsiva:** El sistema **debe** ser plenamente legible y operable en pantallas de teléfonos móviles desde un ancho de **360 px** sin desplazamiento horizontal. | Inspeccionar en emulador de navegador a 360 px de ancho; pasa si no genera barra de scroll horizontal. |
| **RNF-04** | **Ergonomía táctil para mostrador:** Los botones de comando y áreas de toque táctil **deben** tener una dimensión mínima de **44 × 44 píxeles** con alto contraste visual. | Medir las propiedades CSS (`min-width`, `min-height`) en el inspector de elementos del navegador; pasa si todas son ≥ 44 px. |
| **RNF-05** | **Rendimiento de consulta:** El buscador de existencias del catálogo **debe** desplegar los resultados coincidentes en menos de **2 segundos** bajo red local. | Medir el tiempo de respuesta en la pestaña de red (*Network*) del navegador; pasa si la respuesta es < 2000 ms. |
| **RNF-06** | **Persistencia transaccional:** Los registros de inventario y pedidos **deben** persistir íntegramente en la base de datos relacional ante cierres forzados de la ventana del navegador. | Registrar una transacción, forzar el cierre del navegador y verificar la integridad del registro en la tabla MySQL correspondiente. |
| **RNF-07** | **Seguridad y autenticación:** El acceso a los módulos operativos de registro y descarga de respaldos **debe** requerir inicio de sesión con usuario y contraseña con cifrado hash. | Intentar ingresar directamente a la URL de pedidos o respaldo sin sesión activa; pasa si redirige al formulario de inicio de sesión. |
| **RNF-08** | **Disponibilidad contingente local:** El sistema **debe** ser capaz de operar en red local Wi-Fi mediante servidor local contingente ante cortes del servicio público de Internet. | Desconectar el enlace externo de Internet y comprobar que el sistema procesa búsquedas y registros desde el celular conectado a la red local Wi-Fi. |

---

## 4. Requerimientos omitidos de la norma IEEE 830

En estricta concordancia con la norma IEEE 830-1998, se declaran explícitamente las secciones y tipos de requerimientos que no aplican a la escala y naturaleza del proyecto:

1. **Interfaces de hardware dedicadas:**  
   El sistema opera sobre hardware comercial genérico (smartphones y computadoras personales). No requiere interactuar con lectores industriales de tarjetas magnéticas, balanzas de pesaje digital continuo ni controladores embebidos.
2. **Requisitos de rendimiento en tiempo real estricto (*Hard Real-Time*):**  
   El dominio del problema corresponde a operaciones comerciales de mostrador ferretero, donde las restricciones temporales son de usabilidad humana (RNF-01 y RNF-05) y no de procesamiento en milisegundos críticos para el control de procesos industriales.
3. **Portabilidad a nivel de sistema operativo de cliente:**  
   Al implementarse como una aplicación web basada en estándares internacionales (HTML5, CSS3 y JavaScript), la compatibilidad multiplataforma queda delegada al motor del navegador web (Google Chrome, Firefox o Edge en Android o Windows), eliminando la necesidad de empaquetados binarios nativos.
4. **Facturación tributaria computarizada con firma digital:**  
   Omitida formalmente por pertenecer el comercio al Régimen Tributario Simplificado (RTS), el cual no emite facturas con valor de crédito fiscal y no requiere integración con los servicios web del Servicio de Impuestos Nacionales.

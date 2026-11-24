# Sistema de gestión de inventario y pedidos anticipados para Ferretería KateRey

**Propuesta de Proyecto Integrador**  
Programa Académico Desconcentrado "Técnico Superior en Informática"  
UMSA, Sede Colquencha  

**Autor:** Jhamil Najum Chino Huarachi  
**Fecha:** 18 de noviembre de 2026  

---

## Resumen

La Ferretería KateRey, negocio familiar fundado en 2024 y ubicado sobre la Avenida Panamericana en la Zona San Roque (Distrito 7 de la ciudad de El Alto, sobre la ruta troncal hacia Río Seco y Copacabana), registra sus ventas, pedidos por encargo y existencias en un único cuaderno físico sobre el mostrador. Cada día se pierden entre 5 y 10 clientes porque no es posible confirmar la disponibilidad inmediata de mercadería ni verificar si los encargos con adelanto de Bs 100 están listos en la fecha acordada, exponiendo además toda la información a pérdidas por deterioro físico o lluvias. Para solucionar esta problemática sin incrementar los costos fijos, el presente proyecto integrador desarrolla un sistema web liviano con PHP 8 y base de datos relacional MySQL, adaptando la interfaz responsiva desarrollada en el módulo previo. El sistema permite consultar existencias al instante desde el celular del mostrador, listar pedidos pendientes por fecha de entrega y generar respaldos de seguridad. La solución es técnicamente viable y su inversión inicial junto al costo operativo anual se amortizan en apenas dos jornadas al recuperar ventas no concretadas.

---

## Introducción

El presente documento expone la propuesta formal del proyecto integrador para la carrera Técnico Superior en Informática de la Universidad Mayor de San Andrés, desarrollada en la Sede Universitaria Local Colquencha. El propósito central es fundamentar técnica, operativa y económicamente la solución de software requerida por la Ferretería KateRey, un comercio real que necesita superar la gestión manual en papel para asegurar sus ventas diarias y el resguardo de su información comercial.

Se organiza en seis partes fundamentales: la primera presenta el tipo de proyecto y el perfil del cliente; la segunda expone la formulación del problema mediante causas, efectos y árbol de problemas; la tercera define el objetivo general y los objetivos específicos con criterios verificables; la cuarta sustenta la justificación práctica, técnica y social; la quinta analiza la factibilidad con sus riesgos declarados y delimita los alcances y límites del sistema; y la sexta establece la estructura de desglose del trabajo y el cronograma general de ejecución de las cuatro semanas del módulo.

---

## 1. Tipo de proyecto y cliente

### Tipo de proyecto
El presente trabajo corresponde a la modalidad de **Proyecto Integrador**. Se enfoca en resolver una necesidad operativa concreta de un cliente real mediante el diseño, construcción, prueba y documentación formal de un producto de software funcional.

No constituye una monografía académica porque no se limita a compilar el estado del arte de los inventarios comerciales, sino que implementa una solución práctica en código. Tampoco corresponde a un proyecto de investigación teórica porque no plantea una hipótesis sobre una pregunta científica abierta, sino que aplica ingeniería de software para solucionar un problema comercial plenamente delimitado.

### Antecedentes y punto de partida
El proyecto da continuidad técnica al trabajo desarrollado en la asignatura de Programación Web, donde se construyó la interfaz de usuario funcional (frontend responsivo), publicada y probada con un catálogo de productos almacenado en un archivo estático en formato JSON.

El presente módulo completa la solución a través de los siguientes componentes de ingeniería:

| Ya existe (Programación Web) | Se construye en este módulo |
|---|---|
| Interfaz visual publicada y funcional | Propuesta formal y especificación de requerimientos |
| Catálogo de datos en archivo plano JSON | Base de datos relacional persistente y normalizada |
| Ejecución en entorno local aislado | Control de stock en mostrador, respaldo y despliegue |

### El cliente real
El cliente del proyecto es la **Ferretería KateRey**, un emprendimiento familiar de dos personas en funcionamiento continuo desde el año 2024. Se dedica al comercio mayorista y minorista de materiales de construcción y artículos de ferretería en general.

**Ubicación comercial:**  
El establecimiento se encuentra ubicado sobre la **Avenida Panamericana**, en la **Zona San Roque**, perteneciente al **Distrito 7 de la ciudad de El Alto** (Departamento de La Paz), sobre la carretera troncal de alto tránsito comercial que conecta hacia Río Seco y Copacabana.

**Modalidad de trabajo actual:**  
Toda la operación comercial se concentra en un único cuaderno físico colocado sobre el mostrador. Quien atiende anota las ventas del día, las cotizaciones y, de manera particular, los pedidos anticipados y encargos de material que los clientes confirman mediante un adelanto económico de Bs 100, fijando una fecha de recojo. No existe un inventario kardex en estantes, notas duplicadas ni copias de respaldo de estas anotaciones.

**Fuente de la información:**  
Entrevista estructurada con el propietario en el propio establecimiento el 16 de noviembre de 2026, con validación de datos en visita de confirmación el 17 de noviembre de 2026.

---

## 2. Formulación del problema

### Situación problemática en el contexto del cliente
La dependencia exclusiva del cuaderno físico genera tres dificultades documentadas durante el trabajo de campo:

1. **Pérdida de clientes por falta de confirmación de existencias:** El encargado estima la pérdida recurrente de entre 5 y 10 clientes por día. Al momento de la consulta en mostrador, no es posible asegurar con rapidez si el producto solicitado está disponible o si ya fue comprometido para otro encargo. El cliente que acude a comprar se retira sin concretar la venta cuando no se le brinda una respuesta inmediata.
2. **Pérdida de clientes por pedidos anticipados sin seguimiento oportuno:** Los clientes entregan un adelanto de Bs 100 para asegurar materiales especiales o por volumen, pero el seguimiento de las fechas de entrega depende de que el personal recuerde revisar el cuaderno hoja por hoja. Cuando el encargo no se revisa con anticipación, el comprador asiste en la fecha pactada y encuentra que su mercadería no fue apartada o no llegó de almacén, lo que provoca cancelaciones, devolución del adelanto y pérdida del cliente.
3. **Riesgo crítico de pérdida total de información:** El cuaderno es el único registro de cobros, ventas y compromisos de mercadería. Durante los meses de lluvia se expone a filtraciones de agua y humedad en el mostrador, sumado al desgaste por la manipulación de cemento y yeso. Su extravío o destrucción anularía todo el historial contable y los anticipos pendientes.

### Árbol de problemas

```text
                 [ EFECTOS ]
                 
  Pérdida de entre 5 y 10 clientes al día en mostrador
  Pérdida de ingresos comerciales (Bs 500 a Bs 1000 por jornada)
  Reclamos y desconfianza por pedidos no preparados a tiempo
  Riesgo de pérdida irrecuperable de datos ante deterioro del cuaderno
                            ^
                            |
                 [ PROBLEMA CENTRAL ]
                 
  El registro manual en un cuaderno único de mostrador no permite
  confirmar la disponibilidad de productos ni hacer seguimiento de
  los pedidos anticipados con adelanto, y carece de respaldo.
                            ^
                            |
                 [ CAUSAS RAÍZ ]
                 
  Registro desordenado de ventas, consultas y encargos en un mismo espacio
  Inexistencia de un mecanismo de consulta inmediata de stock disponible
  Control de fechas de entrega dependiente de revisión manual hoja por hoja
  Inexistencia de copias de seguridad de la información del negocio
```

### Declaración del problema central
El registro manual en un cuaderno único de mostrador de la Ferretería KateRey no permite confirmar la disponibilidad de productos en tiempo real ni hacer seguimiento a los pedidos anticipados con adelanto, careciendo de respaldo de seguridad, lo que ocasiona la pérdida estimada de 5 a 10 clientes por día y expone al negocio al riesgo de perder la totalidad de su información comercial.

---

## 3. Objetivos

### Objetivo general
Desarrollar un sistema web de gestión de inventario y pedidos anticipados para la Ferretería KateRey, que permita consultar la disponibilidad de productos, hacer seguimiento a los pedidos con adelanto y conservar el registro comercial con respaldo de seguridad.

### Objetivos específicos
Cada objetivo específico se plantea como un resultado de ingeniería evaluable con criterio pasa o falla:

1. **Diseñar el esquema de base de datos relacional normalizada** en MySQL para almacenar entidades de productos, existencias, ventas y pedidos anticipados con adelantos. (Pasa si el script DDL ejecuta sin errores y cumple con tercera forma normal).
2. **Implementar los módulos de registro web para ventas y pedidos anticipados** con validación estricta de campos obligatorios, montos numéricos y fechas de entrega válidas. (Pasa si el formulario rechaza datos incompletos o erróneos y almacena transacciones válidas).
3. **Implementar la consulta rápida de existencias y el listado de pedidos pendientes** con filtros por nombre de producto y por fecha de entrega, incorporando el marcado de estado a entregado. (Pasa si la búsqueda responde en menos de dos segundos y actualiza el saldo y estado del pedido).
4. **Implementar la función de respaldo y exportación de la base de datos** para descarga directa de un archivo de volcado SQL desde la interfaz administrativa. (Pasa si el archivo descargado restaura íntegramente las tablas y registros en el motor MySQL).
5. **Verificar el funcionamiento del sistema mediante una matriz de casos de prueba** que evalúe transacciones normales, límites y casos de error en el 100% de los módulos desarrollados. (Pasa si la totalidad de casos de prueba diseñados arrojan resultado conforme).

---

## 4. Justificación

### Justificación práctica
La disponibilidad de un registro digital consultable en mostrador soluciona de forma directa la fuga de clientes. Quien atiende puede responder sobre existencias en segundos directamente desde la pantalla de su celular, sin abandonar al comprador ni hojear el cuaderno. Asimismo, el listado ordenado de pedidos por fecha de retiro asegura que la mercadería encargada esté lista en el local antes de que el cliente se apersone a recogerla.

### Justificación técnica
Se adopta una aplicación web responsiva porque aprovecha la interfaz ya aprobada del módulo anterior y evita la instalación o configuración de software en los teléfonos de los operadores. La combinación de PHP y MySQL representa una solución probada, de consumo mínimo de recursos y compatible con servicios de alojamiento compartido económicos, facilitando el mantenimiento y la portabilidad técnica.

### Justificación social y económica
La sistematización protege los activos informativos de un emprendimiento familiar alteño, permitiéndole competir en igualdad de condiciones con ferreterías de mayor tamaño comercial en la zona de San Roque y Río Seco. Se garantiza un trato formal y confiable a los vecinos que dejan dinero de adelanto, asegurando el cumplimiento de sus compromisos comerciales.

---

## 5. Factibilidad, alcances y límites

### Factibilidad

#### Factibilidad técnica
El sistema opera sobre la pila de software estándar Apache, PHP y MySQL/MariaDB bajo XAMPP en fase de desarrollo y sobre cualquier servidor web comercial compartido en producción.
* **Riesgo técnico declarado:** Caídas temporales del servicio de Internet en el sector del local comercial durante las horas de atención.
* **Mitigación:** Capacidad de ejecución contingente sobre red local Wi-Fi en el mostrador mediante un servidor local portátil si la conectividad externa se interrumpe.

#### Factibilidad operativa
El sistema será utilizado por el propietario y su colaborador, quienes operan teléfonos inteligentes en su vida cotidiana. Las funciones clave se resuelven en interfaces intuitivas de una sola vista.
* **Riesgo operativo declarado:** Resistencia al cambio o persistencia en el uso del cuaderno en horas de alta concurrencia de clientes.
* **Mitigación:** Formulario de registro ultra simplificado que demanda un máximo de cuatro datos esenciales, permitiendo asentar una venta o un encargo en menos de treinta segundos desde el teléfono.

#### Factibilidad económica
El desarrollo del software no implica costo de mano de obra por desarrollarse en el marco de la formación académica. Los costos reales del proyecto diferencian la inversión única en hardware de contingencia y los costos de operación anual:

| Concepto | Tipo de costo | Costo estimado (Bs) |
|---|---|:---:|
| Hardware para servidor local contingente (Mini PC / equipo local Wi-Fi) | Inversión inicial (pago único) | 450 |
| Alojamiento web compartido (PHP 8 y MySQL) | Operación anual recurrente | 350 |
| Dominio territorial boliviano (.bo) | Operación anual recurrente | 250 |
| **Total Inversión Inicial y Primer Año** | | **1.050** |
| *(Costo operativo anual a partir del 2.° año)* | *(Renovación web y dominio)* | *(600)* |

* **Riesgo económico declarado:** Que el propietario considere que la inversión en hardware contingente y el costo operativo anual de Bs 600 son prescindibles frente al costo mínimo de un cuaderno de papel.
* **Mitigación:** Análisis de retorno de inversión: con un ticket promedio de venta de Bs 100, la pérdida estimada de 5 a 10 clientes al día significa entre Bs 500 y Bs 1.000 perdidos cada jornada. La recuperación de las ventas no concretadas en apenas dos jornadas de atención amortiza por completo tanto el servidor local contingente como el servicio web del primer año.

---

### Alcances y límites

#### Alcances (Lo que sí incluye el sistema)
1. Registro y actualización de productos con código, nombre, categoría, precio y existencia disponible.
2. Registro de ventas directas con deducción inmediata del stock disponible.
3. Registro de pedidos anticipados con nombre del cliente, producto, cantidad, adelanto recibido (Bs 100 referencial), saldo por cobrar y fecha comprometida de entrega.
4. Consulta rápida de existencias mediante buscador interactivo de productos.
5. Listado de pedidos anticipados pendientes ordenados cronológicamente por fecha de entrega.
6. Módulo administrativo para exportar y descargar el respaldo de la base de datos en formato SQL.

#### Límites explícitos (Lo que no incluye el sistema y su justificación)
1. **Facturación electrónica con el SIN:** El negocio pertenece al régimen tributario simplificado y utiliza talonario de notas manuales. La integración con los servicios web del Servicio de Impuestos Nacionales requiere certificados digitales que exceden los tiempos del presente módulo.
2. **Gestión de compras a proveedores y cuentas por pagar:** El problema central del negocio radica en la atención y disponibilidad en mostrador. Incluir compras aumentaría la complejidad del sistema sin atacar la causa principal de pérdida de ventas.
3. **Notificaciones automáticas por mensajería (SMS o WhatsApp Business API):** Requiere suscripciones mensuales pagadas en moneda extranjera que el cliente no requiere en esta fase.
4. **Múltiples sucursales:** El comercio opera en un único establecimiento sobre la Avenida Panamericana, por lo que no se requiere sincronización entre sucursales distribuidas.

---

## 6. Estructura de desglose del trabajo y cronograma

### Estructura de desglose del trabajo (WBS)
La planificación del trabajo se organiza mediante paquetes de productos identificados con sustantivos:

```text
1. Propuesta de proyecto y diagnóstico
   1.1 Diagnóstico de campo y levantamiento de requerimientos
   1.2 Documento de propuesta formal de proyecto
2. Marco teórico y especificación de requerimientos
   2.1 Fundamentación teórica y aplicación de instrumentos de recolección
   2.2 Especificación formal de requerimientos de software (IEEE 830)
   2.3 Modelo conceptual y lógico de base de datos relacional
3. Construcción del sistema web
   3.1 Módulo de gestión de inventario y existencias
   3.2 Módulo de ventas y pedidos anticipados con adelanto
   3.3 Módulo de respaldo y utilidades administrativas
4. Pruebas, despliegue y entrega final
   4.1 Matriz de pruebas funcionales y validación
   4.2 Despliegue en servidor de producción y capacitación
   4.3 Documento final de ingeniería y defensa
```

### Cronograma de ejecución

| Periodo y fecha | Paquetes de trabajo (WBS) | Entregable verificable formal |
|---|---|---|
| **Semana 1** (16 al 20 de noviembre de 2026) | 1.1 Diagnóstico en local y 1.2 Propuesta formal | Documento de propuesta formal de proyecto aprobado |
| **Semana 2** (23 al 27 de noviembre de 2026) | 2.1 Marco teórico y 2.2 Requerimientos IEEE 830 | Marco teórico, estado del arte y especificación formal de requerimientos |
| **Semana 3** (30 de noviembre al 04 de diciembre de 2026) | 3.1 Inventario, 3.2 Pedidos y 3.3 Respaldo | Prototipo del sistema web funcional con base de datos relacional |
| **Semana 4** (07 al 11 de diciembre de 2026) | 4.1 Pruebas, 4.2 Despliegue y 4.3 Documento final | Sistema web desplegado en producción, informe final y defensa académica |

# Marco teórico

## Sistema de gestión de inventario y pedidos anticipados para Ferretería KateRey

---

## Introducción

La gestión de inventarios, ventas en mostrador y control de pedidos anticipados por encargo es un problema ampliamente abordado en la industria del software. Existen en el mercado desde soluciones informales basadas en papel u hojas de cálculo compartidas hasta complejos paquetes comerciales de Planificación de Recursos Empresariales (ERP) y sistemas de Punto de Venta (POS) específicos para el rubro ferretero y de materiales de construcción.

Sin embargo, el trabajo de campo realizado el 16, 17 y 18 de noviembre de 2026 en la Ferretería KateRey (Zona San Roque, El Alto) reveló que la realidad de un comercio familiar atendido por dos personas sobre una carretera troncal impone restricciones operativas muy estrictas: atención simultánea y rápida a clientes de paso, manos impregnadas de polvo de materiales (cemento, estuco, yeso), consultas de stock en menos de 30 segundos para evitar la fuga de ventas, cobro de anticipos de Bs 100 con fecha comprometida de entrega y un presupuesto operativo que no tolera costos fijos mensuales en moneda extranjera.

Este documento analiza el estado del arte a través de cuatro alternativas tecnológicas existentes, contrastándolas mediante una matriz de decisión técnica y económica frente a la solución propuesta, justificando así el desarrollo a medida del sistema web.

---

## Estado del arte

### Alternativas existentes en el mercado

A continuación se evalúan las principales alternativas utilizadas por micro y pequeñas empresas del sector comercial:

| Solución | Costo estimado | Consulta rápida de stock | Control de pedidos por fecha | Operabilidad en celular | Operación sin internet |
|---|---|:---:|:---:|:---:|:---:|
| **Cuaderno físico de mostrador** *(situación actual)* | Bs 0 (costo directo) | **No** *(demora de 3 a 5 min)* | **No** *(hojeo manual reactivo)* | No aplica *(soporte de papel físico)* | **Sí** *(totalmente autónomo)* |
| **Planilla compartida** *(Google Sheets / Excel Móvil)* | Bs 0 (gratuito) | **Lenta / Difícil** *(zoom y búsqueda incómoda)* | **Parcial** *(filtros complejos en pantalla chica)* | **Deficiente** *(celdas pequeñas, riesgo de borrado accidental)* | **No** *(requiere sincronización en nube)* |
| **Software POS comercial** *(ej. Alegra, Siigo, ClassicGes)* | Desde Bs 200 a 350 / mes (recurrente) | **Sí**, pero compleja *(pantallas saturadas de menús)* | **Parcial** *(orientado a facturación, no a encargos)* | **Regular** *(optimizado para monitor de PC y teclado físico)* | **Limitada** *(la mayoría son SaaS dependientes de la nube)* |
| **Desarrollo comercial a medida** | Desde USD 500 a 800 (pago inicial) | **Sí** | **Sí** | **Sí** *(según especificación)* | **Sí** *(si se diseña local)* |
| **Solución propuesta** *(Sistema Web PHP/MySQL + contingencia)* | **Bs 450 inicial + Bs 600/año** | **Sí** *(buscador en < 2 segundos)* | **Sí** *(bandeja ordenada cronológicamente)* | **Alta** *(diseño táctil de 4 campos y botones grandes)* | **Sí** *(red local Wi-Fi contingente)* |

---

### Análisis comparativo de alternativas

#### 1. Cuaderno físico sobre el mostrador (Situación actual)
El cuaderno no requiere energía eléctrica, su costo directo es insignificante y no presenta curva de aprendizaje tecnológico. No obstante, representa la causa raíz de la crisis comercial del cliente: insume de 3 a 5 minutos por consulta al obligar al dependiente a trasladarse al patio para verificar existencias, carece de alertas cronológicas para preparar los encargos con adelanto y se degrada físicamente por la humedad y el polvo cotidiano de yeso y cemento, exponiendo a la ferretería a la pérdida irrecuperable de su historial de cobros.

#### 2. Planillas de cálculo en la nube (Google Sheets / Microsoft Excel)
Aunque eliminan el costo de licencias y permiten centralizar datos, resultan inviables en el mostrador de una ferretería. La observación directa constató que el personal atiende clientes de pie y con prisa: manipular filas, columnas y celdas diminutas desde la pantalla de un teléfono inteligente con dedos cubiertos de guantes o polvo provoca continuos errores de digitación, demoras en la búsqueda y riesgo crítico de sobreescritura accidental de fórmulas o existencias.

#### 3. Sistemas POS y ERP comerciales genéricos (Software como Servicio - SaaS)
Sistemas comerciales como Alegra, Siigo o ClassicGes resuelven con solidez la contabilidad y el kardex de inventarios en medianas y grandes empresas. Sin embargo, su adopción en Ferretería KateRey es técnica y financieramente desaconsejable:
- **Sobrediseño funcional:** Incorporan módulos de facturación electrónica compleja, compras internacionales, cuentas contables y retenciones impositivas que el régimen tributario simplificado del cliente no utiliza.
- **Incompatibilidad de hardware y uso:** Están diseñados prioritariamente para estaciones fijas de escritorio con monitor grande, lector láser de códigos de barra y teclado completo, no para un teléfono móvil en mostrador rústico.
- **Costo insostenible:** Un abono mensual de Bs 200 a Bs 350 genera un costo fijo anual de hasta Bs 4.200, cifra prohibitiva para un negocio familiar de dos personas.

#### 4. Desarrollo a medida comercial por empresa externa
Un software por encargo profesional resolvería con exactitud los requerimientos del cliente. No obstante, las cotizaciones en el mercado de software boliviano para este tipo de desarrollos oscilan entre USD 500 y USD 800 (aproximadamente Bs 3.500 a Bs 5.500), monto que excede por completo la capacidad de inversión de la microempresa y comprometería los ingresos operativos de varios meses.

---

### Conclusión del estado del arte y justificación de la solución propuesta

Ninguna de las alternativas disponibles en el mercado satisface simultáneamente las restricciones del caso: bajo costo de mantenimiento, interfaz móvil ultra simplificada para entorno ferretero, consulta de existencias en menos de dos segundos y ordenamiento cronológico de pedidos anticipados con adelanto de Bs 100.

La **solución propuesta** sintetiza las ventajas de las distintas opciones:
1. **Accesibilidad económica:** Costo operativo anual de solo Bs 600 (hosting y dominio .bo) y Bs 450 de inversión inicial en hardware para el servidor local de contingencia, monto que se amortiza en apenas dos jornadas al evitar la fuga de clientes.
2. **Usabilidad contextualizada:** Interfaz web táctil desarrollada con botones grandes, alto contraste y formularios de registro de máximo 4 campos, operable con rapidez desde un celular en mostrador.
3. **Reconocimiento explícito de limitaciones y mitigación:** A diferencia del cuaderno, un sistema web depende de conectividad; por ello, la arquitectura contempla una mitigación técnica declarada mediante ejecución en red local Wi-Fi ante eventuales caídas del servicio de Internet en la zona.

---

## Metodología de desarrollo

Para el desarrollo del sistema se selecciona una **metodología ágil con enfoque iterativo e incremental**, adaptada a las características del proyecto integrador (cuatro semanas de duración, desarrollo individual y cliente real directamente accesible).

### Justificación del enfoque frente a marcos tradicionales y pesados
No se adoptan metodologías tradicionales en cascada (*Waterfall*) debido a su rigidez documental y tardía verificación de software funcional. Tampoco se aplica el marco *Scrum* en su formalidad estricta, dado que este exige un equipo multidisciplinario con roles diferenciados (*Product Owner*, *Scrum Master*, equipo de desarrollo) y ceremonias (planificaciones de sprint, daily meetings, retrospectivas) que carecen de aplicabilidad en un proyecto de autoría individual.

En su lugar, se adoptan los principios centrales del manifiesto ágil y las prácticas operativas de desarrollo incremental:
- Construcción y entrega de software funcional al finalizar cada ciclo semanal.
- Validación continua y directa con el propietario en mostrador mediante prototipos funcionales.
- Capacidad de ajuste inmediato ante desviaciones en los requerimientos levantados.

---

## Métodos, técnicas y herramientas de software

La selección del conjunto de herramientas responde estrictamente a criterios de viabilidad técnica, interoperabilidad y consumo eficiente de recursos:

| Herramienta / Tecnología | Rol en el proyecto | Criterio de selección y justificación técnica |
|---|---|---|
| **Git y GitHub** | Control de versiones y trazabilidad | Gestión de ramas de desarrollo, respaldo histórico del código fuente y continuidad con el repositorio iniciado en Programación Web. |
| **XAMPP (Apache, PHP 8, MariaDB)** | Entorno de desarrollo y contingencia | Pila de software robusta, ampliamente documentada y capaz de operar sin conexión a Internet en el entorno local del aula y del mostrador. |
| **PHP 8 nativo** | Backend y lógica de transacciones | Lenguaje estándar de la web del lado servidor, con excelente rendimiento en servidores compartidos económicos y compatibilidad nativa con bases de datos relacionales sin requerir frameworks pesados. |
| **MySQL / MariaDB** | Base de datos relacional persistente | Cumplimiento estricto de propiedades ACID (Atomicidad, Consistencia, Aislamiento y Durabilidad), esencial para el manejo de saldos de adelantos monetarios y existencias de productos. |
| **HTML5 semántico, CSS3 y JavaScript** | Interfaz de usuario (Frontend móvil) | Aprovecha la base visual aprobada en el módulo anterior, asegurando carga instantánea, diseño responsivo para pantallas móviles y ergonomía táctil en mostrador. |
| **Matriz de casos de prueba formal** | Control de calidad y verificación | Técnica de ingeniería de software para validar transacciones estándar, límites de stock y manejo de excepciones con criterio verificable de pasa/falla. |

---

## Referencias bibliográficas

Apache Software Foundation. (2024). *Apache HTTP Server Documentation (Version 2.4)*. https://httpd.apache.org/docs/2.4/

IEEE Computer Society. (1998). *IEEE Recommended Practice for Software Requirements Specifications* (IEEE Std 830-1998). Institute of Electrical and Electronics Engineers. https://doi.org/10.1109/IEEESTD.1998.88286

Oracle Corporation. (2024). *MySQL 8.0 Reference Manual*. Oracle. https://dev.mysql.com/doc/refman/8.0/en/

Pressman, R. S., & Maxim, B. R. (2021). *Ingeniería del software: Un enfoque práctico* (9.ª ed.). McGraw-Hill Interamericana.

Sommerville, I. (2011). *Ingeniería de software* (9.ª ed.). Pearson Educación.

The PHP Group. (2024). *PHP Manual: Hypertext Preprocessor (Version 8)*. https://www.php.net/manual/es/

---

## Fuentes no bibliográficas

Propietario de Ferretería KateRey. (16 y 17 de noviembre de 2026). *Entrevista semiestructurada sobre procesos de mostrador, control de existencias y pedidos anticipados con adelanto* [Entrevista en profundidad]. Ferretería KateRey, Zona San Roque, El Alto. (Comunicación personal).

Chino Huarachi, J. N. (18 de noviembre de 2026). *Registro de observación directa de atención en mostrador y revisión documental de 30 páginas del cuaderno de ventas y encargos* [Notas de trabajo de campo]. Ferretería KateRey, Zona San Roque, El Alto.

# Sistema de gestión de inventario y pedidos anticipados para Ferretería KateRey

**Propuesta de Proyecto Integrador**
Programa Académico Desconcentrado "Técnico Superior en Informática"
UMSA · Sede Colquencha

Autor: [Jhamil Najum Chino Huarachi]
Fecha: noviembre de 2026

---

## Tipo de proyecto

**Proyecto integrador.** Se resuelve un problema concreto de un cliente real
construyendo un producto de software funcional, acompañado de la documentación
de ingeniería que respalda las decisiones tomadas.

No es una monografía: no se estudia el estado del arte de los sistemas de
inventario, se construye uno. No es una investigación: no se responde una
pregunta abierta, se resuelve un problema conocido.

---

## El punto de partida

Este proyecto continúa el trabajo del módulo de Programación Web, en el que se
construyó el frontend: una página funcional, publicada, con los datos del
cliente en un archivo JSON.

Para completar el proyecto falta lo siguiente:

| Ya existe | Se construye este módulo |
|---|---|
| el frontend funcionando y publicado | la propuesta que lo justifica |
| los datos en un archivo JSON | una base de datos real |
| "funciona en mi máquina" | requerimientos, pruebas, costos y *deploy* (puesta en producción) |

---

## El cliente

**Ferretería KateRey**, Camino a Río Seco, ciudad de La Paz. Negocio familiar de
dos personas, en funcionamiento desde 2024. Vende material de construcción al
por mayor y al por menor.

**Cómo trabaja hoy:** toda la operación se anota en un cuaderno único: las
ventas, los pedidos anticipados y los encargos de mercadería que el cliente deja
con un adelanto de Bs 100 para confirmar. No hay copia ni respaldo del cuaderno.

**Fuente de esta información:** entrevista con el propietario, 16 noviembre de
2026, en el local. Se registró en notas y se validó con él al día siguiente.

---

## Formulación del problema

La Ferretería KateRey registra las ventas, los pedidos anticipados y los
encargos en un cuaderno físico único que se lleva en el mostrador. Quien atiende
anota el nombre del cliente, el producto, la cantidad, el adelanto recibido y la
fecha en que el cliente espera retirar el pedido.

Este registro presenta tres dificultades documentadas durante la entrevista de
16 noviembre de 2026:

**Pérdida de clientes por falta de disponibilidad.** El propietario estima que
se pierden entre 5 y 10 clientes por día porque, al momento de la venta, no hay
forma de confirmar si el producto solicitado está disponible o si el pedido
anticipado ya llegó. El cliente que va con la intención de comprar se retira sin
comprar cuando no se le puede asegurar la disponibilidad.

**Pérdida de clientes por pedidos anticipados sin seguimiento.** Los clientes
dejan un adelanto de Bs 100 para confirmar un encargo, pero el seguimiento de
esos pedidos depende de que alguien revise el cuaderno. Cuando el pedido no se
revisa a tiempo, el cliente llega y el producto no está listo, y no vuelve.

**Riesgo de pérdida total de la información.** El cuaderno es el único registro
de ventas, pedidos y adelantos. En ocasiones se extravía dentro del local, y en
los meses de lluvia se moja por el manejo constante en el mostrador. Si se daña
o se pierde, no existe ningún respaldo de la información.

### Árbol de problemas
   EFECTOS      Pérdida de entre 5 y 10 clientes por día
                Pérdida de ingresos por ventas no concretadas
                Pérdida de adelantos y pedidos sin trazabilidad
                          ↑
   PROBLEMA     El registro manual en un cuaderno único no permite
   CENTRAL      confirmar la disponibilidad de productos ni hacer
                seguimiento de los pedidos anticipados, y no tiene respaldo
                          ↑
   CAUSAS       Las ventas, los pedidos y los adelantos se anotan juntos
                No hay forma de consultar si un producto está disponible
                El seguimiento de pedidos depende de revisar el cuaderno
                El cuaderno es el único registro y no tiene copia

### Problema central

> El registro manual en un cuaderno único de la Ferretería KateRey no permite
> confirmar la disponibilidad de productos ni hacer seguimiento de los pedidos
> anticipados, y carece de respaldo, lo que ocasiona la pérdida de entre 5 y 10
> clientes por día y el riesgo de perder toda la información.

---

## Objetivos

### Objetivo general

Desarrollar un sistema web de gestión de inventario y pedidos anticipados para
la Ferretería KateRey, que permita consultar la disponibilidad de productos,
hacer seguimiento de los pedidos con adelanto y conservar el registro con
respaldo.

### Objetivos específicos

1. Diseñar la base de datos relacional que registre productos, existencias,
   ventas y pedidos anticipados con su adelanto.
2. Implementar el registro de ventas y de pedidos anticipados desde el
   navegador, con validación de los datos obligatorios.
3. Implementar la consulta de disponibilidad de un producto y la consulta de
   pedidos anticipados pendientes por fecha de entrega.
4. Verificar el funcionamiento del sistema mediante una matriz de casos de
   prueba que cubra el registro, la consulta, el seguimiento y los casos de
   error.

---

## Justificación

**Práctica.** Las tres dificultades descritas en la formulación del problema
tienen solución directa con un registro consultable: la disponibilidad se
consulta en pantalla en lugar de depender de la memoria o del cuaderno, y los
pedidos con adelanto se listan por fecha de entrega en lugar de revisarse hoja
por hoja. Cada cliente que hoy se retira sin comprar por no poder confirmar la
disponibilidad es una venta que el sistema puede recuperar.

**Técnica.** Se elige una aplicación web y no una de escritorio porque el
negocio ya tiene el frontend construido y publicado, y porque debe consultarse
desde el celular del mostrador sin instalar nada. Se usa PHP y MySQL porque
funcionan sobre hosting compartido de bajo costo, que es lo accesible para un
negocio de este tamaño.

**Social.** El registro con respaldo elimina el riesgo de perder toda la
información si el cuaderno se moja o se extravía, situación que ya ocurrió en
los meses de lluvia y que hoy no tiene ninguna copia de seguridad.

---

## Factibilidad

**Técnica.** El sistema requiere un servidor con PHP 8 y MySQL, que es la
configuración estándar de cualquier hosting compartido. El desarrollo se hace
con XAMPP en local, que funciona sin conexión. El frontend ya está construido y
publicado. No se requiere ninguna tecnología que el equipo no haya usado antes.

**Operativa.** El sistema lo van a usar el propietario y su acompañante, ambos
con teléfono con navegador. La operación diaria se reduce a registrar una venta,
registrar un pedido anticipado con su adelanto y consultar la disponibilidad de
un producto, acciones que se resuelven en una pantalla cada una.

*Riesgo identificado:* el registro depende de que la venta o el pedido se cargue
en el momento. Si se sigue anotando en el cuaderno "para pasarlo después", el
sistema no resuelve nada. Se mitiga dejando el registro accesible desde el
celular del mostrador, sin instalar nada.

**Económica.** El desarrollo se realiza como parte del módulo, sin costo para el
cliente. La operación anual estimada es:

| Concepto | Costo anual (Bs) |
|---|---|
| Hosting compartido con PHP y MySQL | 350 |
| Dominio .bo | 250 |
| **Total** | **600** |

Frente a eso, la pérdida estimada de entre 5 y 10 clientes por día, a un ticket
promedio de Bs 100 según el propietario, representa entre Bs 500 y Bs 1.000 en
un solo día. El costo anual de operación se recupera con menos de un día de
ventas no perdidas.

---

## Alcances y límites

### Alcance

El sistema entregado incluye:

- registro de productos con su existencia disponible
- registro de una venta con cliente, producto y cantidad
- registro de un pedido anticipado con adelanto y fecha de entrega
- consulta de disponibilidad de un producto
- consulta de pedidos anticipados pendientes filtrados por fecha de entrega
- marcado de un pedido anticipado como entregado
- respaldo del registro mediante exportación de la base de datos

### Límites

El sistema **no** incluye, y en cada caso se indica por qué:

- **Cobros ni facturación.** La ferretería factura con talonario manual, y la
  facturación electrónica en Bolivia exige integración con el sistema de
  Impuestos Nacionales, que excede el alcance de un módulo de tres semanas.
- **Gestión de compras a proveedores ni cuentas por pagar.** El problema
  formulado es la disponibilidad y el seguimiento de pedidos, no la gestión de
  compras. Incluirlo duplicaría el tamaño del proyecto sin atacar el problema
  central.
- **Notificaciones automáticas al cliente.** Requiere integración con un
  servicio de mensajería de pago. Queda planteado como recomendación.
- **Múltiples sucursales.** El negocio tiene un solo local. El diseño de la
  base de datos no impide agregarlo después, pero no se implementa.

---

*(Este documento continúa el Día 5 con el cronograma, el resumen y la introducción.)*
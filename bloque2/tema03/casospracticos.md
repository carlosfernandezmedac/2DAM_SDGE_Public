# Casos Prácticos — Tema 3
# Los módulos de un ERP

---

## Caso Práctico 1 — La integración de los módulos

Un compañero que se ha incorporado hace poco a la empresa solo usa la aplicación de **Compra**. Sabe que nosotros conocemos más módulos y nos pregunta, durante el descanso, **cómo se relacionan Ventas, Compra y Contabilidad**. Nos pide un ejemplo.

**Plantea un ejemplo en el que intervengan estos módulos y explica qué ocurre en cada uno.**

<details>
<summary>Ver solución</summary>

Un ejemplo claro es el de una **empresa intermediaria**: vende un producto que no tiene en stock y se lo compra a un proveedor.

| Paso | Módulo | Qué ocurre |
|------|--------|------------|
| 1 | **Ventas** | El cliente hace el pedido de venta |
| 2 | **Compra** | Al no haber stock, se genera un pedido de compra al proveedor |
| 3 | **Inventario** | Llega la mercancía y se registra la entrada; después sale hacia el cliente |
| 4 | **Facturación / Contabilidad** | Se registran la **factura de compra** (lo que debemos al proveedor) y la **factura de venta** (lo que nos debe el cliente) |

```
CLIENTE ──► Ventas ──► Compra ──► PROVEEDOR
              │          │
              └─► Facturación / Contabilidad ◄─┘
```

**Idea clave:** el usuario de compras no tiene que avisar a nadie. Como todos los módulos comparten la misma base de datos, la venta provoca la compra y ambas aparecen en contabilidad.

</details>

---

## Caso Práctico 2 — El restaurante 2.0

Eres propietario de un restaurante con mucho éxito y varios socios quieren abrir más locales. Hoy no usáis ningún ERP y hay fallos puntuales: productos que caducan, descuadres en la caja y falta ocasional de stock. En la reunión del miércoles debes proponer una solución con **Odoo**.

**¿Qué módulos recomendarías instalar y por qué?**

<details>
<summary>Ver solución</summary>

| Prioridad | Módulos | Justificación |
|-----------|---------|---------------|
| **Imprescindibles** | **Punto de venta** + **Inventario** + **Facturación** | El TPV controla la caja y, según la web de Odoo, necesita Inventario y Facturación. Resuelve el descuadre de caja y el control de stock |
| **Control económico** | **Contabilidad** y **Gastos** | Para llevar las cuentas del negocio y de cada local |
| **Recomendable** | **Compra** | Automatiza pedidos cuando un artículo baja de un stock mínimo y centraliza los contactos con proveedores |
| **Cuando crezca** | **Empleados** | Si la plantilla aumenta mucho al abrir nuevos locales |
| **Presencia online** | **Sitio web** + **Citas** | Web del restaurante y reservas online |

Cada problema del enunciado tiene su módulo:

| Problema | Módulo que lo resuelve |
|----------|------------------------|
| Descuadres en la caja | Punto de venta |
| Falta de stock / productos caducados | Inventario + Compra |
| Cuentas poco claras al crecer | Contabilidad + Gastos |

</details>

---

## Caso Práctico 3 — Una tienda de informática que quiere vender por Internet

Una pequeña tienda de informática, con 4 empleados, quiere vender también online sin gastar mucho dinero. Hoy lleva el stock en una hoja de cálculo y factura a mano.

1. Propón los módulos de Odoo para **empezar** y justifica la elección.
2. ¿Qué módulos dejarías para una **segunda fase**?

<details>
<summary>Ver solución</summary>

**Fase 1 — empezar:**

| Módulo | Motivo |
|--------|--------|
| **Sitio web** + **Comercio electrónico** | Es el objetivo principal: vender online con pagos y envíos |
| **Inventario** | Sustituye la hoja de cálculo; el stock de la web y el de la tienda es el mismo |
| **Facturación** | Deja de facturarse a mano |

**Fase 2 — cuando lo necesite:**

| Módulo | Motivo |
|--------|--------|
| **CRM** | Seguimiento de clientes y captación de nuevos |
| **Compra** | Pedidos a proveedores automáticos al bajar el stock |
| **Contabilidad** | Cuando quieran llevar la contabilidad completa dentro del ERP |
| **Punto de venta** | Si deciden cobrar en la tienda física con el mismo sistema |

**Idea clave:** al ser una pyme con poco presupuesto, se empieza por lo mínimo que cumple el objetivo y se añaden módulos que se conectan con los anteriores.

</details>

---

## Caso Práctico 4 — ¿Qué aplicación de Odoo uso?

Indica qué aplicación de Odoo usarías para cada tarea:

| Tarea | Aplicación |
|-------|-----------|
| Registrar las vacaciones de un empleado | ? |
| Enviar un presupuesto a un cliente | ? |
| Controlar cuántas unidades quedan de un producto | ? |
| Planificar órdenes de fabricación | ? |
| Hacer seguimiento de un cliente potencial | ? |
| Cobrar con tarjeta en una tienda física | ? |

<details>
<summary>Ver solución</summary>

| Tarea | Aplicación |
|-------|-----------|
| Registrar las vacaciones de un empleado | **Empleados** (o Ausencias) |
| Enviar un presupuesto a un cliente | **Ventas** |
| Controlar cuántas unidades quedan de un producto | **Inventario** |
| Planificar órdenes de fabricación | **MRP (Fabricación)** |
| Hacer seguimiento de un cliente potencial | **CRM** |
| Cobrar con tarjeta en una tienda física | **Punto de venta** |

</details>

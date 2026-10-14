# Tema 3 — Los módulos de un ERP

---

## Índice

1. [Introducción: qué es un módulo](#1-introducción-qué-es-un-módulo)
2. [Las aplicaciones de Odoo](#2-las-aplicaciones-de-odoo)
3. [La integración de los módulos](#3-la-integración-de-los-módulos)
4. [Dependencias entre módulos](#4-dependencias-entre-módulos)
5. [Community y Enterprise: no todo está en tu instalación](#5-community-y-enterprise-no-todo-está-en-tu-instalación)
6. [¿Qué módulos instalo?](#6-qué-módulos-instalo)
7. [Resumen visual del tema](#resumen-visual-del-tema)

---

## 1. Introducción: qué es un módulo

Un ERP no es un único programa, sino un conjunto de **módulos**: cada uno cubre un área de la empresa (ventas, compras, almacén, contabilidad, RR. HH.…). Todos comparten **la misma base de datos**, y por eso se comunican entre sí.

Piensa en los módulos como **las piezas de un puzle**: eliges las que necesitas y, si más adelante la empresa crece, encajas otras sin tener que cambiar de sistema.

```
        ┌───────────┐   ┌───────────┐   ┌───────────┐
        │  Ventas   │   │  Compra   │   │ Inventario│
        └─────┬─────┘   └─────┬─────┘   └─────┬─────┘
              │               │               │
        ┌─────┴───────────────┴───────────────┴─────┐
        │       BASE DE DATOS ÚNICA (PostgreSQL)    │
        └─────┬───────────────┬───────────────┬─────┘
              │               │               │
        ┌─────┴─────┐   ┌─────┴─────┐   ┌─────┴─────┐
        │Contabilidad│  │ Empleados │   │    MRP    │
        └───────────┘   └───────────┘   └───────────┘
```

> 💡 Un dato (por ejemplo, un producto) se **crea una sola vez** y lo ven todos los módulos que lo necesitan.

En Odoo los módulos se llaman **aplicaciones** (*apps*) y se instalan desde el menú **Aplicaciones**. Es el ERP que usaremos en todas las prácticas del curso.

> 📝 Otros ERP, como SAP, organizan sus módulos de la misma forma (con siglas como FI, MM o SD). El concepto es el mismo; aquí nos centramos en Odoo.

---

## 2. Las aplicaciones de Odoo

Las aplicaciones se agrupan por categorías.

### 2.1. Finanzas

| Aplicación | Para qué sirve |
|-----------|----------------|
| **Contabilidad** | Registrar facturas y controlar los pagos |
| **Facturación** | Emitir facturas de cliente y proveedor, enviarlas y registrar los pagos |
| **Gastos** | Monitorizar gastos y refacturarlos por lotes si hace falta |

### 2.2. Operaciones

| Aplicación | Para qué sirve |
|-----------|----------------|
| **Compra** | Automatizar flujos de compra, precios y disponibilidad en proveedores, estadísticas |
| **Inventario** | Trazabilidad total del stock |
| **Proyecto** | Gestión de proyectos (incluso con metodología Agile) |
| Otras | Hojas de horas, Servicio de asistencia, Documentos, Servicio de campo |

### 2.3. Ventas

| Aplicación | Para qué sirve |
|-----------|----------------|
| **CRM** | Contacto con clientes y captación de clientes potenciales |
| **Ventas** | Presupuestos, estrategias de precios, reglas de precio por cliente |
| **Punto de venta** | Tiendas y restaurantes: cobro en efectivo o tarjeta, tickets, facturas. Compatible con casi cualquier hardware |
| Otras | Suscripciones, Alquiler |

### 2.4. Fabricación

| Aplicación | Para qué sirve |
|-----------|----------------|
| **MRP** | Planificar automáticamente las órdenes de fabricación |
| **PLM** | Ciclo de vida del producto: del diseño a la producción |
| **Mantenimiento** | Mantenimiento preventivo, órdenes de mantenimiento, estadísticas |
| **Calidad** | Planes de control de calidad y alertas |

### 2.5. Recursos humanos

| Aplicación | Para qué sirve |
|-----------|----------------|
| **Empleados** | Ficha del empleado, vacaciones, asistencias, bajas, evaluación |
| **Contratación** | Vacantes, ofertas de empleo y procesos de selección |
| **Recomendación de empleados** | Programa de referidos con recompensas |
| **Aprobaciones** | Solicitudes de empleados (viajes, dietas…) |
| Otras | Flota, Ausencias, Valoración |

### 2.6. Sitios web

| Aplicación | Para qué sirve |
|-----------|----------------|
| **Sitio web** | Crear páginas web sin programar |
| **Comercio electrónico** | Tienda online con pagos y envíos integrados |
| **Chat en directo** | Chatear con los visitantes de la web |
| **Citas** | Gestionar citas online |
| Otras | Blogs, Foro, Aprendizaje en línea, Eventos |

### 2.7. Comunicación, marketing y personalización

| Categoría | Aplicaciones |
|-----------|--------------|
| **Comunicación** | Hablar (chat interno), Firma electrónica, Encuestas |
| **Marketing** | Automatización, E-mail, SMS, Social (redes sociales y notificaciones) |
| **Personalización** | **Studio**: crea aplicaciones personalizadas |

### 2.8. Las más usadas en el curso

| Aplicación | Dónde la trabajaremos |
|-----------|------------------------|
| Ventas, Compra, Inventario, Facturación | Bloque 3 — flujo de compra-venta |
| MRP, Punto de venta | Bloque 3 — fabricación y punto de venta |
| Empleados | Prácticas de adecuación del ERP a una empresa |
| *Cualquier app* | Bloque 6 — crearemos nuestro **propio módulo** |

---

## 3. La integración de los módulos

La clave de un ERP es que los módulos **se disparan unos a otros**. Ejemplo clásico: nuestra empresa **actúa de intermediaria**. Vende un producto que no tiene en stock y se lo compra a un proveedor.

```
  CLIENTE ──pedido──►  Ventas ─────────────────┐
                          │                    │
                          │ no hay stock       │ factura de venta
                          ▼                    ▼
                       Compra ───────────►  Facturación
                          │                    ▲  / Contabilidad
                          │ pedido             │
                          ▼                    │ factura de compra
                      PROVEEDOR ───────────────┘
                          │
                          ▼ mercancía recibida
                      Inventario
```

1. El cliente compra (**Ventas**).
2. Se genera una compra al proveedor (**Compra**).
3. Llega la mercancía y se registra la entrada (**Inventario**).
4. Las facturas de compra y de venta quedan registradas (**Facturación / Contabilidad**).

> 💡 El usuario de compras no tiene que avisar a nadie: como todos los módulos comparten la misma base de datos, lo que pasa en uno aparece en los demás. El flujo completo lo veremos en el Bloque 3.

---

## 4. Dependencias entre módulos

Un módulo de Odoo puede **necesitar otros** para funcionar. Por ejemplo, el **Punto de venta** necesita Inventario y Facturación. Cuando instalas uno, Odoo instala **automáticamente** los que necesita.

```
   Punto de venta ──necesita──► Inventario
         │
         └──────────necesita──► Facturación
```

Esa información está escrita en el propio código del módulo, en el fichero `__manifest__.py` de su carpeta, dentro de la clave `depends`:

```python
{
    'name': 'Ventas',
    'depends': ['sales_team', 'account', 'utm', ...],
    ...
}
```

> 💡 Cada carpeta de la carpeta `addons/` del código fuente es un módulo. Lo que ves en el menú Aplicaciones es la lista de esas carpetas. Lo comprobarás en la práctica.

> ⚠️ Por esto **desinstalar** un módulo puede afectar a otros que dependan de él.

---

## 5. Community y Enterprise: no todo está en tu instalación

Odoo se distribuye en dos ediciones (ya lo vimos en el Tema 6):

| Edición | Licencia | Contenido |
|---------|----------|-----------|
| **Community** | Libre y gratuita | Núcleo del ERP: las aplicaciones básicas |
| **Enterprise** | De pago | Todo lo anterior + aplicaciones y funciones adicionales |

Algunas aplicaciones del catálogo de la web (por ejemplo **Studio**, **PLM**, **Calidad** o **Firma electrónica**) son de la edición Enterprise, y **no aparecerán** en la instalación Community que haces con Docker.

> ✅ Para el aula nos basta con Community: tiene los módulos necesarios para casi todas las prácticas.

---

## 6. ¿Qué módulos instalo?

No hay una lista universal: depende del **objetivo**, el **tamaño** de la empresa y el **presupuesto**. Un método sencillo:

```
 1. ¿Qué hace mi negocio?        (vender, fabricar, dar servicios…)
 2. ¿Qué procesos dan problemas? (stock, caja, facturación…)
 3. Elijo los módulos IMPRESCINDIBLES y empiezo por ellos
 4. Más adelante añado otros que se conectan con los anteriores
```

**Ejemplo — "El restaurante 2.0":** un restaurante con éxito quiere abrir más locales y evitar productos caducados, descuadres de caja y falta de stock.

| Prioridad | Módulos | Por qué |
|-----------|---------|---------|
| **Imprescindibles** | Punto de venta, Inventario, Facturación | El TPV necesita inventario y facturación |
| **Control económico** | Contabilidad, Gastos | Cuentas claras y control de caja |
| **Recomendable** | Compra | Compras automáticas al bajar el stock y contacto con proveedores |
| **Cuando crezca** | Empleados | Si la plantilla aumenta mucho |
| **Presencia online** | Sitio web, Citas | Web propia y reservas online |

> 💡 **Empezar por poco** es una ventaja de Odoo: una pyme que solo quiere vender online puede empezar con las aplicaciones web y añadir CRM, Inventario, etc. a medida que lo necesite.

---

## Resumen visual del tema

```
                  LOS MÓDULOS DE ODOO
                          │
     ┌────────────────────┼────────────────────┐
     │                    │                    │
 ¿Qué son?          Categorías de apps     Dependencias
 Piezas que         Finanzas · Operaciones  Instalar una app
 comparten la       Ventas · Fabricación    instala las que
 misma base         RR. HH. · Web           necesita
 de datos           Marketing · Studio      (__manifest__.py)
     │                    │                    │
     └────────────────────┴────────────────────┘
                          │
        INTEGRACIÓN: una venta dispara una compra,
        un movimiento de stock y facturas
                          │
        Community (gratis) vs Enterprise (de pago)
                          │
      ¿Qué instalo? → empezar por lo imprescindible
```

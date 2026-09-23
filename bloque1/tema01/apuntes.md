# Tema 1 — La gestión empresarial

---

## Índice

1. [Introducción](#1-introducción)
2. [Historia y evolución de la informática de gestión](#2-historia-y-evolución-de-la-informática-de-gestión)
3. [Organización estándar de una empresa](#3-organización-estándar-de-una-empresa)
4. [Concepto y características de un ERP](#4-concepto-y-características-de-un-erp)
5. [Concepto y características de un CRM](#5-concepto-y-características-de-un-crm)
6. [Arquitectura de sistemas ERP-CRM](#6-arquitectura-de-sistemas-erp-crm)
7. [Resumen visual del tema](#resumen-visual-del-tema)

---

## 1. Introducción

Este tema es introductorio: sitúa históricamente el nacimiento de la informática de gestión, presenta la organización estándar de una empresa y define qué es un **ERP** y qué es un **CRM**, para terminar con la arquitectura que hace posible que ambos se comuniquen con el resto del mundo digital: **SOA**.

> 💡 **Idea clave:** un ERP organiza la empresa "hacia dentro" (Back Office) y un CRM la organiza "hacia el cliente" (Front Office). Juntos forman el binomio **ERP-CRM**, la combinación más habitual en el mercado.

---

## 2. Historia y evolución de la informática de gestión

Los ERP, como internet, tienen origen militar: en los años 50, tras la Segunda Guerra Mundial, EE. UU. usaba programas de gestión logística (recursos, producción, ejército). Esos programas son los precursores de los ERP actuales.

```
1950s          1960s              1970s        1980s         1990s          2000+
Gestión    ──► Software de   ──►  MRP      ──► MRP II    ──►  ERP       ──►  ERP + CRM
logística      inventarios        (IBM)        (logística     (Gartner      (e-business,
militar        (stock mínimo)                  completa)      bautiza       pymes,
                                                                el término)   SOA)
```

### 2.1. Los 60's — los primeros softwares de gestión

Aparecen las primeras computadoras comerciales y, con ellas, los primeros programas de **gestión y control de inventarios**. Su objetivo: mantener las existencias al mínimo garantizando siempre disponibilidad.

### 2.2. Los 70's — el MRP

Aparece el **MRP** (*Material Requirement Planning* — Sistemas de Planificación de Requerimientos de Material), de IBM. Se considera el antecesor directo del ERP: automatiza la gestión de materiales y permite prever stock, inventario y materias primas.

> 🔗 **Dato curioso:** el 1 de abril de 1972, **SAP** fue fundada en Alemania por cinco exempleados de IBM. Hoy su ERP (del mismo nombre) es uno de los más usados del mundo.

### 2.3. Los 80's — el MRP II

El MRP evoluciona a **MRP II** (*Manufacturing Resource Planning*), que ya no solo controla materiales: abarca todo el proceso logístico de producción (almacén, compras, ventas, planificación de producción) y añade la **administración de recursos económicos**.

### 2.4. Los 90's — el ERP

El grupo **Gartner** bautiza al MRP evolucionado como **ERP**. La clave de su éxito: integrar en un mismo software varios módulos que funcionan de forma independiente pero interconectada.

### 2.5. El ERP en la actualidad

A partir del año 2000 los ERP incorporan nuevas funcionalidades, entre ellas la gestión de relaciones con clientes (**CRM**), dando lugar al binomio **ERP-CRM**. Estos sistemas, antes solo al alcance de grandes empresas, se han hecho progresivamente accesibles también a las **pymes**.

---

## 3. Organización estándar de una empresa

Una gran empresa suele estar dirigida por un **director general** y organizada en **departamentos**, cada uno con una función delimitada y un responsable:

```
                    DIRECCIÓN GENERAL
                          │
   ┌──────────┬───────────┼───────────┬──────────┐
   │          │           │           │          │
Administración Compras  Almacén   Logística   Finanzas
   │          │           │           │          │
 Ventas   Recursos   Marketing
          Humanos
```

- Dirección
- Administración
- Compras
- Almacén
- Logística
- Finanzas
- Ventas
- Recursos humanos
- Marketing

Un ERP-CRM se diseña precisamente para dar cobertura, de forma **modular**, a cada uno de estos departamentos.

---

## 4. Concepto y características de un ERP

**ERP** = *Enterprise Resource Planning* → Sistemas de Planificación de Recursos Empresariales.

### 4.1. Concepto — qué dicen los autores

| Autor | Definición |
|-------|-----------|
| Laudon y Laudon (2001) | Sistemas de información que integran los procesos clave del negocio para que la información fluya libremente entre las partes de la organización, mejorando coordinación, eficiencia y toma de decisiones. |
| Lee (2003) | Paquete de software integrado de uso empresarial: finanzas, RRHH y distribución conviven en un único sistema con una base de datos compartida. |
| Mejía (2004) | Sistemas que integran todos los aspectos funcionales de la empresa (comercial, financiera, producción...) maximizando el ahorro de tiempo y minimizando errores. |
| McGaughey y Gunasekaran (2009) | Sistema de información que integra procesos de negocio para crear valor y reducir costes, haciendo llegar la información correcta a la persona adecuada en el momento adecuado. |

### 4.2. Características

- **Integrado**
- **Modular**
- **Base de datos centralizada**
- **Estándar**
- **Adaptable o configurable**

> 💡 **Definición de síntesis:** un ERP es un software **integrado**, con procesos **estándar** pero **configurable**, que engloba todos los procesos de negocio de forma **modular** sobre una **base de datos centralizada**, con el objetivo de crear valor, ayudar a la toma de decisiones, ahorrar tiempo y minimizar errores.

---

## 5. Concepto y características de un CRM

**CRM** = *Customer Relationship Management* → Sistemas de Administración de la Relación con Clientes.

### 5.1. Concepto

Según Laudon & Laudon (2004), el CRM es una disciplina empresarial y tecnológica para gestionar las relaciones con el cliente con el objetivo de incrementar **facturación, rentabilidad, satisfacción y retención**.

Está orientado a gestión comercial, marketing y atención al cliente: analiza datos históricos de clientes para mejorar (o iniciar) relaciones comerciales, anticiparse a sus necesidades y aumentar ventas.

> Si el ERP centra la estrategia de negocio **en la empresa**, el CRM la centra **en el cliente**.

Normalmente el CRM se asocia a un ERP (formando el binomio ERP-CRM), aunque también puede usarse de forma independiente.

### 5.2. Back Office vs. Front Office

| | Back Office (ERP) | Front Office (CRM) |
|--|---|---|
| **Qué es** | Gestión interna: contabilidad, RRHH, logística... | Cara al cliente: genera ingresos directos |
| **Analogía panadería** | La trastienda, donde se fabrica el pan | El mostrador, donde se vende |

### 5.3. Características del CRM

Análisis de datos de clientes, orientación comercial y de marketing, atención al cliente, retención y captación de clientes.


---

## 6. Arquitectura de sistemas ERP-CRM

Los ERP nacieron con **arquitectura cliente-servidor**: un servidor central atiende a varios clientes simultáneamente.

La evolución de internet impulsó el **e-business** (comercio electrónico) y con él nuevos flujos de comunicación:

| Flujo | Significado |
|-------|-------------|
| **B2B** | *Business to business* — de negocio a negocio |
| **B2C** | *Business to consumer* — de negocio a consumidor |
| **B2E** | *Business to employee* — de negocio a empleado |

```
        B2B                B2C                B2E
  Empresa ⇄ Empresa   Empresa ⇄ Cliente   Empresa ⇄ Empleado
                    │
                    ▼
         Aplicaciones empresariales de terceros
         (procesos colaborativos multi-empresa)
```

Para dar soporte a estas relaciones multi-empresa aparece la **arquitectura orientada a servicios (SOA — Service Oriented Architecture)**: una plataforma abierta y flexible donde distintas aplicaciones empresariales (incluido el ERP) se integran mediante **Servicios Web**.

> 💡 **SOA facilita:** los procesos entre empresas, compartir información relevante entre agentes y el trabajo colaborativo.

### 6.1. Ejemplos sencillos de cada flujo

| Flujo | Ejemplo sencillo |
|-------|-------------------|
| **B2B** | Una panadería pide harina a su proveedor de harinas a través del ERP: empresa que compra a otra empresa. |
| **B2C** | Tú entras en una tienda online y compras unas zapatillas: empresa que vende directamente al consumidor final. |
| **B2E** | Un empleado consulta su nómina o pide vacaciones desde la intranet de su empresa: empresa que da servicio a su propio personal. |

### 6.2. Ejemplo combinado: B2B + SOA

Un caso muy habitual mezcla varios flujos a la vez. Piensa en una tienda online que, al vender un producto, necesita avisar automáticamente a una empresa de transporte (por ejemplo SEUR) para que recoja el paquete:

```
   Cliente compra en tu tienda (B2C)
              │
              ▼
        Tu ERP registra el pedido
              │
              ▼  ── llamada a Servicio Web (SOA) ──►  API de SEUR (B2B)
                                                          │
                                                          ▼
                                              Se genera la recogida del paquete
```

- Es **B2B** porque tu empresa se comunica con otra empresa (el transportista), no con el consumidor final.
- Es **SOA** porque esa comunicación no se programa "a mano": el transportista expone un **Servicio Web** (una API) al que tu ERP llama automáticamente cada vez que se genera una venta.

> 💡 En la práctica, casi nunca hay un flujo "puro": una sola venta puede encadenar B2C (con el cliente), B2B (con el transportista) y SOA como la tecnología que permite que ambas empresas se hablen sin integración manual.


---

## Resumen visual del tema

```
TEMA 1 — LA GESTIÓN EMPRESARIAL

  HISTORIA
  50s Militar → 60s Inventarios → 70s MRP → 80s MRP II → 90s ERP → 2000s ERP-CRM/SOA

                    │
                    ▼
         ORGANIZACIÓN DE LA EMPRESA
     Dirección · Administración · Compras · Almacén
     Logística · Finanzas · Ventas · RRHH · Marketing

                    │
                    ▼
        ┌───────────────────────┐
        │  ERP (Back Office)    │   Integrado · Modular
        │  Gestión interna      │   BD centralizada
        └───────────┬───────────┘   Estándar · Configurable
                    +
        ┌───────────────────────┐
        │  CRM (Front Office)   │   Gestión comercial
        │  Relación con clientes│   Marketing · Atención al cliente
        └───────────┬───────────┘
                    │
                    ▼
         ARQUITECTURA ERP-CRM
     Cliente-Servidor  ──►  SOA (Servicios Web)
                             B2B · B2C · B2E
```

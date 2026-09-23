# Tema 2 — ERP-CRM actuales libres y propietarios

---

## Índice

1. [Introducción](#1-introducción)
2. [Software ERP-CRM libre o propietario](#2-software-erp-crm-libre-o-propietario)
3. [Ventajas y desventajas del código libre](#3-ventajas-y-desventajas-del-código-libre)
4. [Ventajas y desventajas del código propietario](#4-ventajas-y-desventajas-del-código-propietario)
5. [ERP libre](#5-erp-libre)
6. [ERP propietario](#6-erp-propietario)
7. [CRM libre](#7-crm-libre)
8. [CRM propietario](#8-crm-propietario)
9. [Resumen visual del tema](#resumen-visual-del-tema)

---

## 1. Introducción

En el tema anterior vimos qué es un ERP-CRM. En este los clasificamos según su **tipo de licencia**: libres (código abierto) y propietarios (código privado). Veremos ventajas, desventajas y ejemplos reales de cada categoría, tanto para ERP como para CRM.

---

## 2. Software ERP-CRM libre o propietario

> ⚠️ **Puntualización importante:** "libre" y "código abierto" no son exactamente sinónimos, pero a efectos prácticos de este tema los trataremos de forma equivalente: lo relevante es si el **código fuente** es consultable, modificable y distribuible o no.

### 2.1. Código abierto

Modelo de desarrollo basado en la **colaboración abierta**: el código fuente puede ser consultado, modificado y distribuido por cualquier persona.

> 💡 **Ojo con el mito:** código abierto **no significa gratuito**. El código fuente sí lo es, pero puede servir de base a productos con coste (la "reprogramación" comercial de software libre es habitual).


### 2.2. Código propietario

Exige el **pago de una licencia de uso**. Suele cuidar más la interfaz gráfica, el rendimiento y la personalización, porque hay una empresa que vive de ello. Incluye soporte técnico oficial.

El código fuente **no es accesible**: solo lo tiene el desarrollador. Según la Free Software Foundation (FSF), un código es propietario (o privado) si no es libre, ni siquiera parcialmente (semilibre).

| | Código abierto | Código propietario |
|--|-----------------|---------------------|
| Código fuente | Consultable, modificable, distribuible | Solo accesible por el desarrollador |
| Coste | Normalmente más económico (no siempre gratis) | Requiere licencia de pago |
| Evolución | La marca la comunidad | La marca el fabricante |
| Soporte | Limitado / de terceros | Oficial y especializado |

---

## 3. Ventajas y desventajas del código libre

**Ventajas:**
- Sin coste de licencia → menor coste total de propiedad e implantación; su uso o manipulación no es delito.
- La evolución no depende de un proveedor, sino de la **comunidad** → suele traducirse en estabilidad.
- Si la comunidad es activa, evoluciona rápido con actualizaciones frecuentes.
- Tecnologías más actuales, más herramientas y posibilidades de personalización.

**Desventajas:**
- Garantía limitada (si la hay, del distribuidor/implantador, no del *core* del ERP-CRM).
- La evolución es genérica, depende de la comunidad y no de las necesidades de tu empresa.
- Algunas versiones gratuitas están limitadas; hay que pagar para desbloquear funciones.

---

## 4. Ventajas y desventajas del código propietario

**Ventajas:**
- Desarrollado por grandes fabricantes → garantías, cobertura de errores, soporte y servicio postventa especializado.
- Muy fiable: años de experiencia con muchos clientes usándolo a diario, en constante evolución.
- Muy especializado, puede evolucionar en áreas específicas del negocio.

**Desventajas:**
- Coste elevado (aunque la competencia lo está moderando).
- **Dependencia:** la implantación y personalización con un proveedor concreto dificulta un futuro cambio de ERP.

---

## 5. ERP libre

| ERP | Módulo servidor | Base de datos | Licencia | Repositorio |
|-----|-----------------|----------------|----------|--------------|
| **ERPNext** | Python | MariaDB | LGPLv3 (código abierto puro, sin extensiones privadas) | GitHub |
| **Odoo** | Python (≥ 3.10) | PostgreSQL | LGPLv3 (comunitaria) + licencia comercial (empresarial) | GitHub |

- **ERPNext**: defiende usar solo software libre (sin extensiones privadas de pago). Incluye módulos principales (stock, CRM, RRHH, ventas, finanzas), industriales, personalización, webs y portales.
- **Odoo**: antes *TinyERP* → *OpenERP* → *Odoo*. Según su web, unos **42 módulos** organizados en ventas (incluye CRM), finanzas, operaciones, fabricación, RRHH, comunicación, marketing, webs y personalización. Tiene versión "comunitaria" (LGPLv3) y versión "empresarial" (comercial), con app web y de escritorio.

> 💡 **Por qué importa para este módulo:** los dos ERP libres más relevantes del mercado están escritos en **Python**, el mismo lenguaje que trabajaremos en los bloques 5 y 6 para desarrollar componentes.

---

## 6. ERP propietario

Los tres ERP propietarios más extendidos —todos con opción de añadir CRM— son:

| ERP | Punto fuerte |
|-----|--------------|
| **SAP ERP** | Pionero del sector. Apuesta de futuro: SAP S/4HANA, con opción en la nube. |
| **Oracle ERP Cloud** | El más potente en la nube, según Parven y Maimani (2014). |
| **Microsoft Dynamics ERP** | Mejor flexibilidad comercial y el más económico de los tres. |

El coste de cada uno depende de consultoría, licencias por usuario, mantenimiento, etc.

---

## 7. CRM libre

Además del CRM integrado en Odoo/ERPNext, existen CRM independientes de código abierto:

- **SuiteCRM**: desarrollado por la misma comunidad que SugarCRM (que tiene versión *open source* limitada + versión de pago). Compatible con MySQL, MariaDB o SQL Server. Muy personalizable (gestión de contactos, seguimiento de clientes potenciales). Código en GitHub, licencia AGPL-3.0.
- **Fat Free CRM**: basado en **Ruby** (a diferencia de los demás). Seguimiento de oportunidades de venta y captación de usuarios. Muy personalizable vía plugins. Es el CRM mejor valorado en GitHub → comunidad activa que lo mantiene.

---

## 8. CRM propietario

- **Salesforce**: considerado líder del CRM en la nube. Muy completo (puede resultar complejo para pymes pequeñas). Datos de ventas, gestión de leads, automatización de marketing, apps móviles, fácil integración con otros softwares. Planes escalables.
- **Zoho CRM**: más de 15 años de experiencia, también en la nube. Agrega datos de clientes de múltiples fuentes (email, chat, llamadas, redes sociales). Automatiza procesos de ventas y permite portales personalizables para clientes. También con planes escalables.

---

## Resumen visual del tema

```
TEMA 2 — ERP-CRM LIBRES Y PROPIETARIOS

         SOFTWARE ERP-CRM
              │
   ┌──────────┴──────────┐
   ▼                      ▼
CÓDIGO ABIERTO       CÓDIGO PROPIETARIO
+ Barato/gratis      + Garantía y soporte oficial
+ Comunidad activa   + Muy fiable y especializado
- Garantía limitada  - Caro
- Evolución genérica - Dependencia del proveedor

   ERP LIBRE              ERP PROPIETARIO
   ERPNext (Python)       SAP ERP
   Odoo (Python)          Oracle ERP Cloud
                          Microsoft Dynamics ERP

   CRM LIBRE               CRM PROPIETARIO
   SuiteCRM (AGPL-3.0)     Salesforce
   Fat Free CRM (Ruby)     Zoho CRM
```

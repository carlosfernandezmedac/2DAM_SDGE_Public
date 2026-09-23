# Tema 5 — El entorno de instalación de ERP-CRM

---

## Índice

1. [Introducción](#1-introducción)
2. [Requisitos de instalación de SAP S/4 HANA](#2-requisitos-de-instalación-de-sap-s4-hana)
3. [Requisitos de instalación de Odoo](#3-requisitos-de-instalación-de-odoo)
4. [Resumen visual del tema](#resumen-visual-del-tema)

---

## 1. Introducción

Antes de instalar un ERP en serio (eso lo haremos en el Bloque 2), necesitamos saber **qué requisitos de hardware y software exige** cada opción, y **qué formas de instalación existen**. Este tema analiza los requisitos de dos ERP muy distintos entre sí: **SAP S/4 HANA** (propietario) y **Odoo** (libre) — es la primera toma de contacto real con la instalación.

---

## 2. Requisitos de instalación de SAP S/4 HANA

SAP dispone de una edición reducida pensada para pruebas y entornos pequeños: **SAP HANA 2.0 Express Edition**, instalable en local (*on-premise*) de tres formas:

```
        SAP HANA 2.0 Express Edition
                    │
      ┌─────────────┼─────────────┐
      ▼             ▼             ▼
  Instalable    Máquina virtual   Docker
  (Linux)       preconfigurada    (solo Linux)
```

### 2.1. Mediante instalable (Linux)

La opción más compleja: requiere conocimientos de Linux.

| Requisito | Mínimo |
|-----------|--------|
| RAM | 16 GB (recomendado 24 GB) — si usas 16 GB, sube el espacio de intercambio (*swap*) a 32 GB |
| Disco | 120 GB libres en SSD |
| CPU | 2 núcleos (recomendado 4) |
| Software | Java Runtime Environment (JRE) 8+ de 64 bits · SUSE Linux Enterprise Server for SAP Applications o Red Hat Enterprise Linux for SAP Applications |

### 2.2. Mediante máquina virtual preconfigurada

Se descarga una VM ya lista con SUSE Linux Enterprise Server (SLES) y SAP HANA preconfigurados.

| Requisito | Mínimo |
|-----------|--------|
| RAM | 8 GB solo para la VM + 16 GB para el servidor (recomendado 24 GB en total) |
| Disco | 120 GB libres en SSD |
| CPU | 2 núcleos (recomendado 4); si es Intel, comprobar soporte de **VT-x** (Virtualization Technology) |
| Software | JRE 8+ de 64 bits · un monitor de VM (se recomienda VMware) · SO anfitrión: Windows, OS X o Linux |

### 2.3. A través de Docker

Necesita conocimientos básicos de Docker. Solo disponible para Linux, y únicamente para unas pocas distribuciones concretas (Ubuntu 17.04, openSUSE Leap, CentOS 7, Debian 9, Fedora 28).

---

## 3. Requisitos de instalación de Odoo

Odoo se puede instalar de **cuatro formas**:

| Forma | Descripción |
|-------|-------------|
| **Online (SaaS)** | La más fácil: no se instala nada, se usa desde el navegador. A cambio, dependes de un proveedor y de su coste. |
| **Instalador** | Instala los módulos necesarios; permite mantenimiento a largo plazo (actualizaciones). |
| **Código fuente** | Máxima flexibilidad; ideal para desarrollar módulos propios o como base de un despliegue en producción. |
| **Docker** | A través de un contenedor; existe una imagen oficial de Odoo en Docker Hub. |

Existen además dos versiones: la **comunitaria** (libre, mantenida vía GitHub) y la **empresarial** (de pago, del proveedor oficial belga Odoo S.A.). Se puede migrar de comunitaria a empresarial, no al revés.

### 3.1. Requisitos hardware — fórmulas de cálculo

Odoo no da cifras fijas de RAM/CPU: da **fórmulas** para calcularlas según el número de usuarios.

```
Regla de oro: (nº CPUs × 2) + 1 (un trabajador extra dedicado a tareas programadas)
Los trabajadores de Cron necesitan CPU
1 trabajador ≈ 6 usuarios concurrentes (usuarios usando Odoo a la vez, no usuarios totales registrados).
```

Para calcular el tamaño de la memoria, Odoo nos **indica que solo el 20% de las solicitudes que se hacen en Odoo son pesadas, mientras que el 80% son más simples**. Estiman que un trabajador “pesado” puede llegar a consumir 1GB (1024MB) de RAM, mientras que uno “ligero” ronda los 150MB de RAM. 

RAM = nº trabajadores × (80% × 150MB + 20% × 1024MB)

| Tamaño de despliegue | CPUs     | Workers según fórmula `(CPU×2)+1` | RAM según fórmula (`workers × 325MB`) | ≈ Usuarios concurrentes (workers × 6) |
|-----------------------|----------|-------------------------------------|------------------------------------------|------------------------------------------|
| Pequeño                | 2        | (2×2)+1 = **5**                     | 5 × 325MB ≈ **1,6 GB**                    | ≈ 30                                       |
| Mediano                | 4        | (4×2)+1 = **9**                     | 9 × 325MB ≈ **2,9 GB**                    | ≈ 54                                       |
| Grande                 | 16 (2×8) | (16×2)+1 = **33**                   | 33 × 325MB ≈ **10,7 GB**                  | ≈ 198                                      |

### 3.2. Requisitos software según la forma de instalación

| Forma | Requisito principal |
|-------|----------------------|
| Online | Navegador web soportado, nada más |
| Instalador | SO Windows / basado en Debian (Ubuntu...) / basado en RPM (Fedora, CentOS...) + **PostgreSQL** instalado en el mismo host |
| Código fuente | PostgreSQL + descompresor (7zip...) o Git + **Python 3.6+** + compilador de C++ (Visual Studio Build Tools) |
| Docker | Tener Docker instalado y conocimientos básicos del mismo |

---

### 3.3. Docker como una de las opciones — qué es, en concepto

Docker es una de las formas de instalación que hemos visto tanto para SAP como para Odoo. En concepto: empaqueta una aplicación junto con todo lo que necesita para funcionar (dependencias, configuración) en una unidad aislada llamada **contenedor**, mucho más ligera que una máquina virtual porque no arrastra un sistema operativo completo propio.

| Concepto | Qué es |
|----------|--------|
| **Imagen** | Plantilla de solo lectura con todo lo necesario para ejecutar una app (p. ej. `odoo:17.0`) |
| **Contenedor** | Una instancia en ejecución de una imagen |
| **docker-compose** | Fichero que define varios contenedores relacionados (p. ej. Odoo + su base de datos PostgreSQL) y cómo se conectan |

---

## Resumen visual del tema

```
TEMA 5 — EL ENTORNO DE INSTALACIÓN DE ERP-CRM

    SAP S/4 HANA (propietario)          Odoo (libre)
    ┌─────────────────────┐          ┌─────────────────────┐
    │ Instalable (Linux)   │          │ Online (SaaS)        │
    │ Máquina virtual       │          │ Instalador            │
    │ Docker                │          │ Código fuente         │
    └─────────────────────┘          │ Docker                │
                                       └─────────────────────┘
              │                                 │
              └────────────────┬────────────────┘
                                ▼
                    ELECCIÓN SEGÚN REQUISITOS
              (hardware disponible, SO, conocimientos,
                presupuesto, escalabilidad futura)
```

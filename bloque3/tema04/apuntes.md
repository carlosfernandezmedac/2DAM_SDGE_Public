# Tema 4 — El proyecto de implantación de un ERP

**Objetivos:** distinguir las fases de la implantación · conocer la documentación de cada fase · saber qué rol predomina en cada una.

---

## 1. Introducción

Implantar un ERP no es solo "instalar un programa": es un **proyecto con fases**, cada una con sus funciones. Para pasar a la siguiente hay que **cerrar bien la anterior**. Todas persiguen el mismo objetivo: **el éxito de la implantación**.

---

## 2. Fases de la implantación

Antes de decidir, la empresa se pregunta: ¿es necesario?, ¿qué beneficio trae?, ¿resolverá problemas?

¿Quién se adapta a quién?

```
   EMPRESA ──adapta──► ERP        (difícil cambiar toda la empresa)
   ERP ──adapta──► EMPRESA        (caro y lento)
   MEZCLA de ambas      ✅ la recomendada
```

El proyecto tiene **8 fases**, cada una con tareas y documentación:

```
 ANTES                  DURANTE                        DESPUÉS
┌────────────┐  ┌──────────┐  ┌────────────┐  ┌────────┐
│1 Planifica-│─►│2 Análisis│─►│3 Parametri-│─►│4Pruebas│
│   ción     │  │consultor.│  │zación/dise.│  │        │
└────────────┘  └──────────┘  └────────────┘  └───┬────┘
┌────────────┐  ┌──────────┐  ┌────────────┐  ┌───▼────┐
│8 Manteni-  │◄─│7 Soporte │◄─│6 Migración │◄─│5 Forma-│
│   miento   │  │seguimient│  │  y arranque│  │  ción  │
└────────────┘  └──────────┘  └────────────┘  └────────┘
```


### Los roles: quién es quién


```
 PARTE CONTRATANTE (el cliente)          PARTE CONTRATADA (la implantadora)
 ┌────────────────────────────┐          ┌─────────────────────────────┐
 │ Gerente                    │          │ Jefe de proyecto            │
 │ Usuarios líderes           │◄────────►│ Consultor funcional         │
 │ Usuarios finales           │ contrato │ Consultor técnico           │
 │ Administrador del sistema  │          │ Programadores               │
 └────────────────────────────┘          │ Tester / analista de calidad│
                                         │ Formador                    │
                                         │ Soporte técnico             │
                                         └─────────────────────────────┘
```

| Parte | Rol | Qué hace |
|-------|-----|----------|
| **Contratante** | Gerente | Expone los requisitos y centra la planificación propuesta por la implantadora |
| | Usuarios líderes | Usuarios con experiencia que participan en definir los requisitos porque **conocen la empresa** (saben cómo adaptar ERP y empresa) |
| | Usuarios finales | Los que **usarán** el ERP |
| | Administrador del sistema | Prepara el sistema para implantar el ERP y las futuras adaptaciones |
| **Contratada** | Jefe de proyecto | Coordina todas las fases, asegura la comunicación entre equipos y que se cumpla la planificación |
| | Consultor funcional | Traduce los requisitos del cliente a especificaciones del ERP |
| | Consultor técnico | Adapta técnicamente el ERP a los requisitos de la empresa |
| | Programadores | Programan lo que el estándar no cubre |
| | Tester / analista de calidad | Pruebas exhaustivas del funcionamiento |
| | Formador | Capacita a los usuarios finales |
| | Soporte técnico | Atiende problemas y hace ajustes tras la implantación |

> 💡 **Truco para recordarlo:** *funcional = qué* (consultor funcional) · *técnico = cómo* (consultor técnico y programadores).

---

## 3. Planificación

Es la fase **más importante**: el punto de partida. **Sin prisas**: cuanto más tiempo se dedica, menos errores después.

```
  ┌─────────────────────────────────────┐
  │   CONTRATO cliente ⇄ implantadora   │
  │  · objetivos y requisitos           │
  │  · recursos (personas y materiales) │
  │  · presupuesto y fecha de entrega   │
  │  · criterios de éxito               │
  │  · equipo y ROLES                   │
  └─────────────────────────────────────┘
```

Se definen todos los integrantes con sus **roles** para que cada uno sepa sus responsabilidades.

---

## 4. Consultoría

- Se detallan los **alcances**, incluso con **diagramas de flujo** de procesos.
- Resultado: el **diseño funcional**, que describe **qué** hay que hacer. Lo hacen **consultores o analistas**.
- Traducen lo que dice el cliente (lenguaje coloquial) a **requisitos del ERP** (lenguaje de alto nivel, no técnico).
- El cliente **valida** el documento: un error aquí es barato; después, no.
- Se crea el **plan de pruebas**.

```
 Cliente: "necesito saber si un material es líquido"
              │   (consultor)
              ▼
 Diseño funcional: "en la ficha del material, un
                    checkbox «Líquido»"
```

---

## 5. Parametrización y diseño

Con el diseño funcional hecho, el **personal técnico** escribe el **diseño técnico**: **cómo** se hace.

```
 FUNCIONAL (qué)                 TÉCNICO (cómo)
 checkbox «Líquido»     ───►     campo  es_liquido  (booleano)
 en la ficha                     en la tabla de materiales
```

Después se implementa:
1. **Parametrización**: se configura el estándar del ERP para adaptarlo.
2. **Programación**: solo si el estándar no cubre un requisito.

---

## 6. Pruebas

Simulan los procesos **reales** de la empresa. No basta que un informe se imprima: los **datos** deben ser correctos. En proyectos grandes hay **testers**.

| Tipo | Qué prueba |
|------|-----------|
| **Unitarias** | Una funcionalidad concreta |
| **Integrales** | Varias partes juntas |
| **Finales o reales** | Todo el proceso, como en la realidad |

Todas se **documentan** (capturas, grabaciones o textos). Con resultado satisfactorio, los cambios pasan de **desarrollo a producción**.

---

## 7. Despliegue

### Formación
Se forma a los **usuarios finales y al administrador** **antes** de producción, en el entorno de pruebas, donde pueden **equivocarse sin miedo**. Su **implicación** es fundamental.

### Migración y arranque
Es **el gran paso**: el ERP funciona en producción. Fase **intensa y estresante**: los errores son críticos y hay que resolverlos rápido.

---

## 8. Post implantación

```
 PRODUCCIÓN ──► SOPORTE y SEGUIMIENTO ──► fin del contrato
                                     └──► MANTENIMIENTO (nuevo proyecto, opcional)
```

- **Soporte y seguimiento:** durante el tiempo del contrato se atienden los errores reales (se reportan cuanto antes y se **documentan**) y se comprueba que el cliente usa bien el ERP.
- **Mantenimiento:** nuevo proyecto para herramientas a medida, modificaciones o corrección de errores.

---

## 9. Resumen

```
 CONTRATO → DISEÑO FUNCIONAL → DISEÑO TÉCNICO → IMPLEMENTACIÓN
                                                     │
 MANTENIMIENTO ← SOPORTE ← PRODUCCIÓN ← FORMACIÓN ← PRUEBAS
```

| Fase | Objetivo | Documento | Roles predominantes |
|------|----------|-----------|---------------------|
| 1 Planificación | Objetivos, recursos, tiempos y criterios de éxito | Estimaciones, requisitos y **contrato** | 📖 **Jefe de proyecto** (coordina y es el enlace con el cliente) ·  **Cliente** (aporta los requisitos) |
| 2 Consultoría y análisis | Analizar los procesos y ver cómo el ERP se adapta | **Diseño funcional** + plan de pruebas | 📖 **Consultor / analista funcional** (traduce los requisitos del cliente a requisitos del ERP) |
| 3 Parametrización y diseño técnico | Adaptar el ERP; programar solo si hace falta | **Diseño técnico** (basado en el funcional) | 📖 **Técnico / programador** (traduce lo funcional a técnico y lo desarrolla) ·  **Consultor técnico** (vela por que cumpla los requisitos) |
| 4 Pruebas | Comprobar que funciona (unitarias, integrales, finales) | Resultados con capturas o grabaciones | 📖 **Tester** (prueba y detecta errores) |
| 5 Formación (despliegue) | Capacitar a los usuarios antes de producción | Material formativo |  **Formador / instructor** ·  **Administrador del sistema** |
| 6 Migración y arranque (despliegue) | Puesta en producción y uso real | Plan de puesta en marcha | **Administrador del sistema** (gestión técnica) |
| 7 Soporte y seguimiento (post-implantación) | Que funcione en el entorno real y solucionar problemas | **Registro de errores** |  **Soporte técnico** |
| 8 Mantenimiento (post-implantación) | Ajustes y modificaciones según las necesidades | Nuevo contrato | **Consultor de mantenimiento** |

El cliente y el responsable del proyecto se ayudan mutuamente para **adaptar el ERP a la empresa y viceversa**, todo **por contrato**.

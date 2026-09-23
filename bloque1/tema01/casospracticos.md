# Casos Prácticos — Tema 1
# La gestión empresarial

---

## Caso Práctico 1 — La importancia del ERP y el CRM

La empresa de reparto **"Veloz"** nació hace dos años. Poco a poco se ha hecho famosa por su puntualidad y atención al cliente, pero todavía no tiene ERP ni CRM porque tiene pocos clientes. En su lugar, los trabajadores usan Excel, Outlook, programas de finanzas sueltos, etc.

**¿Qué podría ocurrir si poco a poco aumentan sus clientes y siguen sin usar un ERP ni un CRM?**

<details>
<summary>Ver solución</summary>

Puede ocurrir que la empresa **"muera de éxito"**: aquello que la hizo famosa (puntualidad, atención al cliente) desaparece por haberse vuelto insostenible de gestionar, con la consiguiente pérdida de clientes.

**Síntomas esperables:**

- La gestión de pedidos con Excel se vuelve tediosa e inmanejable.
- La comunicación entre departamentos (finanzas, logística...) por email genera **retrasos y errores**.
- La atención al cliente pierde eficacia: los clientes repiten su problema a varios teleoperadores distintos porque no hay un histórico centralizado.

**Qué habría evitado el problema:**

- Un **ERP** habría permitido gestionar todos los departamentos desde una misma herramienta, eliminando errores y retrasos en las comunicaciones internas.
- Un **CRM** habría mejorado el departamento de atención al cliente al centralizar la comunicación tanto con clientes como con compañeros de la empresa.

**Conclusión:** cuantos más clientes y más departamentos coordinar, más crítico se vuelve disponer de un ERP-CRM: no es un capricho tecnológico, es lo que permite escalar sin que la calidad de servicio se resienta.

</details>

---

## Caso Práctico 2 — Elección de arquitectura

Una empresa de fabricación de muebles trabaja únicamente con su propio personal y sus propios almacenes: no comparte procesos con proveedores ni con otras empresas. Otra empresa del sector textil, en cambio, subcontrata la logística, comparte previsiones de stock con dos proveedores clave y vende a través de varios marketplaces externos.

**¿Qué arquitectura (cliente-servidor o SOA) recomendarías a cada una y por qué?**

<details>
<summary>Ver solución</summary>

| Empresa | Arquitectura recomendada | Por qué |
|---------|---------------------------|---------|
| Fabricante de muebles (todo interno) | **Cliente-servidor** | No necesita exponer procesos a terceros; le basta con que su servidor central atienda a los clientes (usuarios) internos de la empresa. Es más simple y económica de mantener. |
| Empresa textil (logística subcontratada, proveedores, marketplaces) | **SOA** | Necesita que sus procesos sean transparentes y coordinables con agentes externos (proveedores, logística, marketplaces) mediante Servicios Web. Es el escenario típico de ERP II / ERP extendido. |

La clave para decidir no es el tamaño de la empresa, sino **cuántos agentes externos necesitan intercambiar información de forma coordinada con sus procesos internos**.

</details>

---

## Caso Práctico 3 — Identifica el flujo (elaboración propia)

Para cada situación, indica qué flujo de comunicación representa (**B2B**, **B2C** o **B2E**) y si además interviene una arquitectura **SOA**:

1. Un cliente compra una camiseta en la web de una tienda de ropa.
2. El ERP de un fabricante de coches pide automáticamente 500 neumáticos al ERP de su proveedor cuando el stock baja de cierto nivel.
3. Un trabajador solicita sus vacaciones desde el portal interno de RRHH de su empresa.
4. Una tienda online, al confirmarse una venta, llama automáticamente a la API de una empresa de transporte para generar la recogida del paquete.
5. Un comercial consulta desde el móvil el historial de compras de un cliente antes de visitarlo.

<details>
<summary>Ver solución</summary>

| # | Situación | Flujo | ¿SOA? |
|---|-----------|-------|-------|
| 1 | Cliente compra en la web | **B2C** | No — es una venta directa, no una integración automática entre sistemas de empresas distintas. |
| 2 | ERP pide neumáticos al ERP del proveedor automáticamente | **B2B** | **Sí** — dos sistemas de dos empresas distintas se comunican automáticamente mediante un servicio, sin intervención manual. |
| 3 | Empleado pide vacaciones en la intranet | **B2E** | No — es una gestión interna dentro de la misma empresa. |
| 4 | Venta online → aviso automático al transportista | **B2B** | **Sí** — es el ejemplo típico: tu empresa (vendedor) se comunica con otra empresa (transportista) a través de un Servicio Web. |
| 5 | Comercial consulta el CRM desde el móvil | **B2E** | No — el empleado usa una herramienta interna de su propia empresa. |

**Idea para quedarte con la diferencia:** B2B/B2C/B2E describen **quién habla con quién** (empresa-empresa, empresa-cliente, empresa-empleado); SOA describe **cómo se hace esa comunicación** cuando es automática entre sistemas de distintas empresas (normalmente B2B), mediante Servicios Web. Por eso B2C y B2E casi nunca llevan SOA: no suele haber una integración automática entre sistemas de *empresas distintas* en esos casos, sino una interacción directa de una persona con "su" sistema.

</details>
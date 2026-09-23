# Casos Prácticos — Tema 5
# El entorno de instalación de ERP-CRM

---

## Caso Práctico 1 — La ampliación de personal

Tenemos la versión **comunitaria de Odoo** instalada en local, en un servidor físico de la empresa con 2 GB de RAM y 2 CPUs. Funciona bien con los 5 empleados actuales, pero la empresa va a expandirse y aumentará considerablemente el número de usuarios, con picos de uso muy desiguales (momentos con muchos usuarios a la vez y momentos con pocos).

Tendremos presupuesto disponible para pasar a una opción de pago si hace falta. Lo que más nos importa es la **escalabilidad futura** y la **tranquilidad de tener soporte con garantías**.

**¿Ampliamos el servidor actual o pasamos a Odoo Cloud con el proveedor oficial Odoo S.A.?**

<details>
<summary>Ver solución</summary>

La opción elegida es pasar a la versión **Cloud** de Odoo S.A. (versión empresarial en la nube).

- Lo que prima no es el coste, sino la **escalabilidad futura** y la garantía de soporte especializado — exactamente lo que ofrece la vía Cloud del proveedor oficial.
- Es técnicamente posible: se puede migrar de la versión comunitaria a la versión empresarial sin partir de cero.
- Ampliar solo el hardware del servidor local resolvería el problema a corto plazo, pero no da la tranquilidad de soporte ni la escalabilidad automática ante picos de uso desiguales que sí ofrece la nube.

</details>

---

## Caso Práctico 2 — ¿Cumplimos los requisitos? (elaboración propia)

Queremos instalar Odoo para que lo usen **20 personas** a la vez. Nuestro servidor actual tiene **2 CPUs y 8 GB de RAM**.

**Aplicando las fórmulas de Odoo, ¿cumplimos los requisitos mínimos? Si no, ¿qué opciones tenemos?**

<details>
<summary>Ver solución</summary>

Según la fórmula de Odoo:

```
Nº de trabajadores concurrentes = (nº CPUs × 2) + 1
```

Con 2 CPUs: `(2 × 2) + 1 = 5` workers = 30 trabajadores concurrentes.

RAM = 5 trabajadores × 325MB ≈ 1.625 MB ≈ 1,6 GB → con margen, 2 GB

| Requisito | Necesario | Disponible | ¿Cumple? |
|-----------|-----------|------------|----------|
| CPUs | 2 | 2 | ✅ Sí |
| RAM | ≈ 2 GB | 8 GB | ✅ Sí |

**Resultado:** siguiendo la cadena completa (personas → trabajadores → CPU/RAM), **el servidor actual es suficiente** para 20 personas conectadas a la vez, con bastante margen de RAM de sobra.

</details>


## Caso Práctico 3 — De trabajadores a CPU y RAM (elaboración propia)

Vamos a montar un servidor Odoo que necesita **9 trabajadores** (*workers*, procesos del servidor — no personas).

**¿Cuántas CPUs necesitamos como mínimo (regla de oro) y cuánta RAM?**

<details>
<summary>Ver solución</summary>

**CPUs** — despejando la regla de oro `trabajadores = (CPUs × 2) + 1`:

```
CPUs = (trabajadores − 1) ÷ 2 = (9 − 1) ÷ 2 = 4 CPUs
```

**RAM** — cada trabajador consume de media ≈ 325 MB (`80% × 150MB + 20% × 1024MB`):

```
RAM = 9 trabajadores × 325MB ≈ 2.925 MB ≈ 2,9 GB → redondeamos a 3-4 GB con margen
```

**Resultado:** con 9 trabajadores necesitamos, como mínimo, **4 CPUs** y aproximadamente **3 GB de RAM** (recomendable subir a 4 GB por margen de seguridad).

</details>

---

## Caso Práctico 4 — De clientes a trabajadores, CPU y RAM (elaboración propia)

Una empresa espera tener **36 clientes (usuarios humanos) conectados a la vez** a su Odoo en las horas punta.

**¿Cuántos trabajadores necesita el servidor? ¿Y cuántas CPUs y cuánta RAM, como mínimo?**

<details>
<summary>Ver solución</summary>

**Paso 1 — De clientes a trabajadores** (1 trabajador ≈ 6 clientes concurrentes):

```
trabajadores = 36 clientes ÷ 6 = 6 trabajadores
```

**Paso 2 — CPUs** (regla de oro despejada):

```
CPUs = (6 − 1) ÷ 2 = 2,5 → redondeamos hacia arriba → 3 CPUs
```

**Paso 3 — RAM:**

```
RAM = 6 trabajadores × 325MB ≈ 1.950 MB ≈ 1,9 GB → redondeamos a 2 GB con margen
```

**Resultado:** para 36 clientes concurrentes hacen falta **6 trabajadores**, **3 CPUs** y **≈ 2 GB de RAM** como mínimo.

</details>

---

## Caso Práctico 5 — Al revés: ¿a cuántos clientes doy servicio? (elaboración propia)

Tenemos un servidor con **8 CPUs** y **16 GB de RAM**.

**¿Cuántos trabajadores puede soportar? ¿Y a cuántos clientes concurrentes equivale eso, aproximadamente?**

<details>
<summary>Ver solución</summary>

**Paso 1 — De CPUs a trabajadores** (regla de oro):

```
trabajadores = (CPUs × 2) + 1 = (8 × 2) + 1 = 17 trabajadores
```

**Paso 2 — Comprobar que la RAM alcanza:**

```
RAM necesaria = 17 trabajadores × 325MB ≈ 5.525 MB ≈ 5,4 GB
```

Como tenemos 16 GB disponibles y solo hacen falta ≈ 5,4 GB, la **RAM no es el cuello de botella** — nos sobra de largo (podríamos incluso permitirnos algunos trabajadores más si quisiéramos, aunque la CPU seguiría siendo el límite real).

**Paso 3 — De trabajadores a clientes** (1 trabajador ≈ 6 clientes):

```
clientes ≈ 17 trabajadores × 6 = 102 clientes concurrentes
```

**Resultado:** este servidor podría dar servicio, de forma orientativa, a algo más de **100 clientes conectados a la vez**, y la CPU (no la RAM) sería el factor que marca ese límite.

</details>

---

## Caso Práctico 6 — Decide qué falta (elaboración propia)

Una asesoría quiere instalar Odoo para que lo usen **48 empleados a la vez** (clientes concurrentes). Disponen de un servidor con **3 CPUs y 4 GB de RAM**.

**¿El servidor actual es suficiente? Si no, ¿qué recurso hay que ampliar primero?**

<details>
<summary>Ver solución</summary>

**Paso 1 — Clientes → trabajadores:**

```
trabajadores = 48 ÷ 6 = 8 trabajadores
```

**Paso 2 — Trabajadores → CPUs necesarias:**

```
CPUs = (8 − 1) ÷ 2 = 3,5 → redondeamos hacia arriba → 4 CPUs
```

**Paso 3 — Trabajadores → RAM necesaria:**

```
RAM = 8 trabajadores × 325MB ≈ 2.600 MB ≈ 2,6 GB
```

**Comparación:**

| Requisito | Necesario | Disponible | ¿Cumple? |
|-----------|-----------|------------|----------|
| CPUs | 4 | 3 | ❌ No |
| RAM | ≈ 2,6 GB | 4 GB | ✅ Sí |

**Resultado:** la RAM sobra, pero **falta 1 CPU**. Hay que ampliar el servidor a 4 núcleos (o migrar a una opción en la nube) antes de dar servicio a los 48 empleados a la vez; no haría falta tocar la RAM.

</details>


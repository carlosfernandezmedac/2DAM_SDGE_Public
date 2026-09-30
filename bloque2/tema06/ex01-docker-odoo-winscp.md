# Ejercicio 1 — Instalar Odoo con Docker y transferir ficheros por WinSCP

> **Tipo:** ejercicio práctico — se realiza junto al Tema 6 (opciones de implantación en Odoo).
> **Requisito previo:** tener completado el Ejercicio 1 del Bloque 1 (Ubuntu Server + SSH funcionando).
> **Objetivo:** entender qué es Docker, fijar una IP estática al servidor, instalar Docker, desplegar Odoo mediante `docker-compose` y aprender a transferir ficheros a un servidor Linux con un cliente gráfico (WinSCP).

---

## Paso 0 — ¿Qué es Docker?


| Concepto | Qué es |
|----------|--------|
| **Imagen** | Plantilla de solo lectura con todo lo necesario para ejecutar una app (p. ej. `odoo:17.0`) |
| **Contenedor** | Una instancia en ejecución de una imagen |
| **docker-compose** | Fichero que define varios contenedores relacionados (p. ej. Odoo + su base de datos PostgreSQL) y cómo se conectan entre sí |

Cada aplicación va en **su propio contenedor**, separado del resto (Odoo en un contenedor, PostgreSQL en otro). No es que se pueda hacer de otra forma, es una buena práctica: cada pieza queda aislada, y eso trae ventajas muy concretas:

- **Si algo se rompe, no se lleva todo por delante.** Si el contenedor de la base de datos falla, reinicias solo ese, sin tocar Odoo.
- **Puedes actualizar una pieza sin tocar la otra.** Cambias la versión de PostgreSQL sin tener que reinstalar Odoo, y viceversa.
- **Funciona igual en cualquier sitio.** La imagen lleva todo empaquetado (versión exacta de cada dependencia), así que si funciona en tu VM, funciona igual en la de un compañero o en un servidor en la nube — sin el clásico "en mi máquina funcionaba".
- **Se monta y se destruye en segundos.** Si algo sale mal en clase, en vez de reinstalar el sistema entero, borras los contenedores (`docker-compose down`) y los vuelves a levantar (`docker-compose up -d`) limpios, en segundos.

En este ejercicio vamos a levantar **dos contenedores a la vez** (Odoo y PostgreSQL), conectados entre sí mediante `docker-compose`.

---

## Paso 1 — Fija una IP estática con Netplan

Hasta ahora tu servidor obtenía la IP por DHCP (podía cambiar en cada arranque). Vamos a fijarla, para que WinSCP y el navegador siempre apunten al mismo sitio. Tu profesor te indicará qué IP debes usar.

1. Identifica el nombre de tu interfaz de red:
```bash
ip a
```
Busca algo como `enp0s3` o `eth0` (el nombre exacto varía según la VM).

2. Localiza el fichero de configuración de Netplan:
```bash
ls /etc/netplan/
```

3. Edítalo (sustituye `nombre-del-fichero.yaml` por el que hayas visto):
```bash
sudo nano /etc/netplan/nombre-del-fichero.yaml
```

4. Deja un contenido parecido a este, con **la IP que te indique el profesor**:
```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: no
      addresses:
        x.x.x.x/24
      routes:
        - to: default
          via: x.x.x.x
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```

> ⚠️ Respeta la indentación exacta (los espacios importan en YAML) y sustituye `enp0s3` por el nombre real de tu interfaz.

5. Aplica los cambios:
```bash
sudo netplan apply
```

6. Comprueba que la IP ha cambiado:
```bash
ip a
```

A partir de ahora, usa siempre esta IP fija para conectarte por SSH y por WinSCP.

---

## Paso 2 — Instalar WinSCP en tu equipo

1. Descarga WinSCP desde su web oficial: <https://winscp.net/>
2. Instálalo con las opciones por defecto.
3. Ábrelo.

> 💡 Si usas Linux o macOS como sistema anfitrión, puedes usar **FileZilla** o el propio explorador de archivos con protocolo `sftp://` — el concepto es el mismo, solo cambia la herramienta.

---

## Paso 3 — Conectar por WinSCP a tu servidor

1. En WinSCP, crea una nueva conexión:
   - Protocolo de archivo: **SFTP**.
   - Servidor: la IP estática que acabas de fijar en el Paso 1.
   - Puerto: 22.
   - Usuario y contraseña: los mismos que usas para SSH.
2. Conecta. La primera vez te pedirá aceptar la huella del servidor — es el mismo mecanismo de seguridad que viste al conectarte por SSH.
3. Si todo va bien, verás **dos paneles**: a la izquierda tu equipo, a la derecha el contenido del servidor.

---

## Paso 4 — Consulta la documentación oficial antes de copiar nada

Antes de crear el fichero, entra en la página oficial de la imagen de Odoo en Docker Hub: <https://hub.docker.com/_/odoo> y busca el apartado **"Environment Variables"** y **"Docker Compose examples"**.

Fíjate en que las variables `HOST`, `USER` y `PASSWORD` que vamos a usar están documentadas ahí mismo por el propio fabricante de la imagen — no nos las inventamos, es la forma oficial de configurar el contenedor.

---

## Paso 5 — Preparar el fichero docker-compose.yml en tu equipo

En tu propio ordenador (no en el servidor), crea un fichero de texto llamado `docker-compose.yml` con este contenido:

```yaml
version: "3"
services:
  db:
    image: postgres:16
    environment:
      POSTGRES_DB: postgres
      POSTGRES_USER: odoo
      POSTGRES_PASSWORD: odoo
    volumes:
      - odoo-db-data:/var/lib/postgresql/data

  odoo:
    image: odoo:18.0
    depends_on:
      - db
    ports:
      - "8069:8069"
    environment:
      HOST: db
      USER: odoo
      PASSWORD: odoo
    volumes:
      - odoo-web-data:/var/lib/odoo

volumes:
  odoo-db-data:
  odoo-web-data:
```

---

## Paso 6 — Subir el fichero al servidor con WinSCP

1. En el panel derecho (servidor) de WinSCP, crea una carpeta llamada `odoo-docker` (botón derecho → *Nueva* → *Directorio*).
2. Entra en esa carpeta.
3. En el panel izquierdo (tu equipo), localiza tu `docker-compose.yml`.
4. **Arrástralo** del panel izquierdo al derecho para subirlo al servidor.

Comprueba que ha llegado correctamente: debería aparecer ya en el panel derecho, dentro de `odoo-docker`.

---

## Paso 7 — Instalar Docker en el servidor

Conéctate por **SSH** (usando ya tu IP fija) y ejecuta:

```bash
sudo apt update
sudo apt install docker.io docker-compose -y
sudo systemctl enable --now docker
sudo docker run hello-world
```

Si ves el mensaje de bienvenida de Docker, todo está correcto.

---

## Paso 8 — Levantar Odoo

Sigue en la conexión SSH:

```bash
cd ~/odoo-docker
sudo docker compose up -d
sudo docker ps
```

Deberías ver dos contenedores en marcha: uno de `postgres` y otro de `odoo`.

---

## Paso 9 — Acceder a Odoo desde el navegador

Desde tu equipo, abre un navegador y ve a la IP fija que configuraste:

```
http://X.X.X.X:8069
```

Debería aparecer el asistente de Odoo para crear tu primera base de datos.

---

## Paso 10 — Crear tu base de datos y comprobar los módulos

1. En el asistente inicial de Odoo, rellena:
   - **Nombre de la base de datos:** `bd_tunombre` (sustituye `tunombre` por tu nombre, ej. `bd_carlos`).
   - **Email:** el que quieras usar como administrador.
   - **Contraseña:** la del usuario administrador.
   - **Idioma y país:** España / Español.
2. Antes de crear la base de datos, busca el enlace **"Master Password"** (clave maestra).. Esta clave protege operaciones sensibles como duplicar o eliminar bases de datos, y es **distinta** de la contraseña del usuario administrador. **Guárdala aparte, no la pierdas.**
3. Pulsa **Create database** y espera a que Odoo termine de inicializarla.
4. Una vez dentro, ve al menú de **Aplicaciones** (icono de cuadrícula, arriba a la izquierda, o el módulo "Apps").
5. Comprueba que aparece el catálogo completo de módulos de Odoo (Ventas, CRM, Inventario, Contabilidad, Sitio Web, etc.), aunque todavía no tengas ninguno instalado — es la señal definitiva de que Odoo está funcionando correctamente, con conexión a su base de datos y sirviendo contenido normalmente.

---

## Entrega

Redacta un documento breve donde documentes todo el proceso seguido, paso a paso, hasta llegar a la instalación completa. El documento debe leerse como un tutorial propio, redactado por ti, no como una simple lista de capturas sin explicar.

---

## Checklist de autocomprobación

- [ ] Sé explicar qué es una imagen, un contenedor y docker-compose.
- [ ] He fijado una IP estática con Netplan y `ip a` la confirma.
- [ ] WinSCP conecta correctamente por SFTP a mi servidor usando la IP fija.
- [ ] He consultado la documentación oficial de Odoo en Docker Hub antes de copiar el fichero.
- [ ] He subido `docker-compose.yml` a `~/odoo-docker/` usando WinSCP.
- [ ] Docker y docker-compose están instalados y `docker run hello-world` funciona.
- [ ] `docker ps` muestra los contenedores `db` y `odoo` en marcha.
- [ ] Puedo acceder a Odoo desde el navegador en el puerto 8069, usando la IP fija.
- [ ] He creado mi base de datos `bd_tunombre` y guardado la clave maestra aparte.
- [ ] He comprobado que el catálogo de Aplicaciones/Módulos aparece correctamente.



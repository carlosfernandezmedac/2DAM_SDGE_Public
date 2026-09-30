# Tema 6 — Tipos de instalaciones de sistemas ERP-CRM

---

## Índice

1. [Introducción](#1-introducción)
2. [Tipos de instalación](#2-tipos-de-instalación)
3. [Tipos de licencias software](#3-tipos-de-licencias-software)
4. [Opciones de implantación en SAP](#4-opciones-de-implantación-en-sap)
5. [Opciones de implantación en Odoo](#5-opciones-de-implantación-en-odoo)
6. [Docker vs. instalador: ¿por qué usamos Docker en el aula?](#6-docker-vs-instalador-por-qué-usamos-docker-en-el-aula)
7. [Instalación práctica: Odoo con Docker en Ubuntu Server](#6-instalación-práctica-odoo-con-docker-en-ubuntu-server)
8. [Resumen visual del tema](#resumen-visual-del-tema)

---

## 1. Introducción

En el Tema 5 vimos los requisitos de hardware y software de SAP y Odoo. En este tema damos el paso siguiente: **cómo instalarlos realmente**, según el grado de independencia que se quiera tener respecto al proveedor del software.

---

## 2. Tipos de instalación

### 2.1. SaaS (Software as a Service)

La opción con **mayor dependencia** del proveedor: el ERP corre en un servidor que no es tuyo, se accede mediante pago, y es el propio proveedor quien gestiona las versiones.

> ✅ Ventaja: te despreocupas totalmente de instalación y mantenimiento de hardware. Basta con conectarse y usarlo.

### 2.2. Hosting

El ERP está alojado en un servidor (del proveedor oficial, propio, o de un tercero), pero **si el hosting no lo ofrece preinstalado, hay que instalarlo tú**. Dependiendo de quién sea el servidor y quién instale el software, habrá que preocuparse de hardware, de software, o de ambos.

> ✅ Ventaja: puedes instalar cualquier módulo y versión que necesites, más flexible que SaaS.

### 2.3. Servidor local

La opción con **mayor independencia** del proveedor: tú te haces cargo de todo (hardware y software). Pensada para empresas que no quieren o no pueden tener el ERP conectado a internet.

> ✅ Ventaja: la más económica y flexible.

```
             MENOS INDEPENDENCIA                    MÁS INDEPENDENCIA
                    │                                       │
   SaaS  ──────────────────►  Hosting  ──────────────────►  Servidor local
   (el proveedor lo                                          (tú te encargas
    gestiona todo)                                            de todo)
```

---

## 3. Tipos de licencias software

Una licencia de software es, según Labrador (2012), un contrato entre el desarrollador (sometido a propiedad intelectual y derechos de autor) y el usuario, donde se definen los derechos y deberes de ambas partes.

Además de libre, código abierto y propietario (vistas en el Tema 2), hay que conocer:

| Tipo de licencia | Qué significa |
|-------------------|-----------------|
| **Dominio público** | No tiene derechos de autor |
| **Laxa o permisiva** | Permite usar el código de cualquier forma |
| **Copyleft** | Si coges el código, lo modificas y lo distribuyes (lo compartes o vendes), tienes que hacer público tu código también — "si lo compartes, se comparte igual que te lo dieron |
| **GPL de GNU** (*General Public License*) | Es "la marca" concreta de copyleft de Linux y muchísimo software libre |
| **Comercial** | Desarrollado por una empresa que busca ganar dinero con su uso |

> 💡 **El núcleo de Odoo tiene licencia LGPLv3** — una licencia de protección débil (*weak copyleft*) que permite enlazar módulos privados al código y no obliga a difundir el código propio que use Odoo bajo esa licencia. Por eso Odoo puede tener a la vez una versión comunitaria libre y módulos empresariales de pago conviviendo en el mismo sistema.

---

## 4. Opciones de implantación en SAP

SAP S/4 HANA ofrece **cuatro opciones**, todas disponibles tanto en local (*on-premise*) como en la nube (*cloud*):

| Edición | Qué ofrece |
|---------|-------------|
| **Runtime Edition** | Plataforma restringida, solo para ejecutar aplicaciones SAP, con uso limitado de funciones avanzadas |
| **Express Edition** | Paquete simplificado y gratuito, hasta 32GB de memoria (ampliable de pago) |
| **Standard Edition** | Base de datos para casos de uso innovadores, con opciones flexibles avanzadas |
| **Enterprise Edition** | Plataforma sin restricciones, pensada para innovación en entornos híbridos modernos |

> 📌 **Caso práctico del libro — "Eligiendo la instalación de SAP":** se necesita una versión de SAP en local para Big Data, con integración de base (no opcional) con Hadoop y Spark, con todas las aplicaciones (no solo las de SAP), y optimizada para Big Data.
>
> | | Enterprise | Standard | Express | Runtime |
> |---|---|---|---|---|
> | Integración Hadoop/Spark | ✅ Sí | Opcional | ✅ Sí | Solo apps SAP |
> | Optimizado para Big Data | ✅ Sí | ✅ Sí | ❌ No | ✅ Sí |
>
> Solo la **Enterprise Edition** cumple los dos requisitos a la vez (integración de base + optimización Big Data), así que es la elegida.

---

## 5. Opciones de implantación en Odoo

Como vimos en el Tema 5, hay 4 formas de instalar Odoo: online (SaaS), instalador, código fuente, y Docker; y dos versiones (comunitaria y empresarial).

### 5.1. Versión online (SaaS)

Odoo ofrece una versión demo gratuita por horas, sin compromiso. La versión SaaS completa está totalmente gestionada por Odoo S.A., ofrece instancias privadas y usuarios ilimitados; empieza siendo gratuita con pocos módulos, y a partir de ahí se paga una mensualidad según el número de módulos. Ni la demo ni el SaaS requieren instalar nada — solo un navegador.

### 5.2. Versión con instalador

#### En Windows

Basta con descargar el instalador y seguir los pasos — instala todo lo necesario para trabajar con Odoo en local. Sirve tanto para la versión comunitaria como para la empresarial.

#### En Debian y RPM

Primero hay que instalar PostgreSQL en el mismo host:

```bash
# Debian/Ubuntu
sudo apt install postgresql -y

# RPM
sudo dnf install -y postgresql-server
sudo postgresql-setup --initdb --unit postgresql
sudo systemctl enable postgresql
sudo systemctl start postgresql
```

Después, Odoo se puede instalar de dos formas:

**a) Mediante repositorio oficial** (solo versión comunitaria), en Debian/Ubuntu como root:

```bash
wget -O - https://nightly.odoo.com/odoo.key | apt-key add -
echo "deb http://nightly.odoo.com/13.0/nightly/deb/ ./" >> /etc/apt/sources.list.d/odoo.list
apt-get update && apt-get install odoo
```

Y en RPM:

```bash
sudo dnf config-manager --add-repo=https://nightly.odoo.com/13.0/nightly/rpm/odoo.repo
sudo dnf install -y odoo
sudo systemctl enable odoo
sudo systemctl start odoo
```

**b) Mediante paquetes `.deb`/`.rpm`** (sirve para comunitaria y empresarial), descargados de la web oficial:

```bash
# Debian
dpkg -i <ruta_al_paquete>
apt-get install -f
dpkg -i <ruta_al_paquete>

# RPM
sudo dnf localinstall odoo_13.0.latest.noarch.rpm
sudo systemctl enable odoo
sudo systemctl start odoo
```

Ambas formas instalan Odoo como **servicio**, crean el usuario en PostgreSQL y arrancan el servidor automáticamente.

> ⚠️ Estos comandos usan el repositorio *nightly* de la versión 13.0 tal como aparece en el libro — en la práctica de clase usaremos Docker (apartado 6), que es más simple de reproducir y mantener actualizado en el aula.

#### Código fuente

No es realmente "instalar" Odoo, sino **ejecutarlo directamente desde el sistema** — la opción preferida por desarrolladores, porque el código queda más accesible.

**En Windows**, tras clonar el repositorio (`git clone https://github.com/odoo/odoo.git`) hacen falta Python 3.6+, PostgreSQL y el compilador de Visual Studio (herramientas de compilación C++):

```bash
cd \CommunityPath
pip install setuptools wheel
pip install -r requirements.txt
python odoo-bin -r dbuser -w dbpassword --addons-path=addons -d mydb
```

**En Linux/Mac**, además de las dependencias de Python, hacen falta dependencias nativas:

```bash
sudo apt install python3-dev libxml2-dev libxslt1-dev libldap2-dev libsasl2-dev
```

> 📌 **Caso práctico del libro — "Eligiendo la instalación correcta":** un usuario con Windows quiere usar Odoo solo como usuario final (no desarrollador), sin conocimientos de Git, Python, PostgreSQL ni el compilador de Visual Studio.
>
> **Solución:** sí puede usar Odoo, sin necesidad de nada de eso — la opción adecuada es el **ejecutable/instalador para Windows**, que instala todo lo necesario de un tirón y sirve tanto para la versión comunitaria como para la empresarial.

---

## 6. Docker vs. instalador: ¿por qué usamos Docker en el aula?

El instalador para Windows también empaqueta todo lo necesario (PostgreSQL, Python...) en un solo asistente, así que a primera vista se parece a Docker. La diferencia está en cómo se comporta cada uno después de instalarlo:

| | Instalador (Windows) | Docker |
|---|---|---|
| ¿Toca el sistema operativo? | Sí, instala PostgreSQL como servicio real, deja archivos y configuración permanentes | No, todo vive aislado dentro del contenedor |
| ¿Puedo tener varias versiones a la vez? | Difícil — chocan puertos y el mismo PostgreSQL del sistema | Sí, cada una en su propio contenedor, sin conflicto de puertos |
| ¿Se puede desinstalar "limpio"? | No siempre — puede dejar restos (servicios, carpetas) | Sí, se borra el contenedor y no queda nada |
| ¿Mismo resultado en cualquier equipo? | No garantizado — depende de qué tuviera antes ese Windows | Sí, el `docker-compose.yml` da siempre el mismo entorno |
| ¿Pensado para...? | Probarlo en tu propio PC, uso final | Desplegar en un servidor real (lo que se usa en producción) |

> 💡 Por eso practicamos con Docker sobre Ubuntu Server: es el escenario real de una implantación en empresa, no el de "probarlo en mi ordenador".

---


## 7. Instalación práctica: Odoo con Docker en Ubuntu Server

**Docker** es una herramienta que empaqueta una aplicación junto con todo lo que necesita para funcionar (dependencias, librerías, configuración) en una unidad aislada llamada **contenedor**. A diferencia de una máquina virtual, un contenedor no lleva un sistema operativo completo propio — comparte el del servidor donde corre —, por eso arranca en segundos y consume muchos menos recursos.

Recordando el Tema 5: **imagen** = plantilla de la app; **contenedor** = la imagen en ejecución; **docker-compose** = fichero que levanta varios contenedores relacionados a la vez (Odoo + su base de datos PostgreSQL).

### 7.1. Instalar Docker en Ubuntu Server

```bash
sudo apt update
sudo apt install docker.io docker-compose -y
sudo systemctl enable --now docker
sudo docker run hello-world
```

### 7.2. Crear el fichero docker-compose.yml

```bash
mkdir ~/odoo-docker && cd ~/odoo-docker
nano docker-compose.yml
```

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

### 7.3. Arranque

```bash
sudo docker-compose up -d
sudo docker ps
```

Deberían aparecer dos contenedores en marcha (`db` y `odoo`).

### 7.4. Verificar el arranque

Desde el navegador, en la misma red:

```
http://IP_de_tu_servidor:8069
```

Debería aparecer el asistente de Odoo para crear la primera base de datos — esa pantalla confirma que el arranque ha sido correcto.

> 💡 La práctica guiada completa (instalación + WinSCP + verificación) está en `bloque2/ejercicios/ex01-docker-odoo-winscp.md`.

---

## Resumen visual del tema

```
TEMA 6 — TIPOS DE INSTALACIONES DE ERP-CRM

  TIPOS DE INSTALACIÓN                    TIPOS DE LICENCIA
  SaaS → Hosting → Servidor local         Dominio público, Laxa, Copyleft,
  (de más a menos dependencia             GPL, Comercial
   del proveedor)                         (Odoo: núcleo LGPLv3)

                    │
                    ▼
         ┌─────────────────────┐
         │   SAP S/4 HANA         │  Runtime · Express · Standard · Enterprise
         └─────────────────────┘

         ┌─────────────────────┐
         │   ODOO                  │  SaaS · Instalador (Windows/Debian/RPM)
         └─────────────────────┘  · Código fuente · Docker (práctica del aula)
                    │
                    ▼
       docker-compose (Odoo + PostgreSQL) → arranque → localhost:8069
```

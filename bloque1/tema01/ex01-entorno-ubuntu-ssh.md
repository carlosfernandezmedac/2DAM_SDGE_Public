# Ejercicio 1 — Preparación del entorno: Ubuntu Server + SSH

> **Objetivo:** dejar preparada la máquina base sobre la que, en el Bloque 2, instalaremos y configuraremos un sistema ERP-CRM.

---

## Contexto

Antes de instalar un ERP-CRM (Bloque 2 — Temas 4, 5 y 6) necesitamos una máquina Linux funcionando y accesible por red. Este ejercicio prepara esa base: no forma parte todavía de los contenidos evaluables de Sistemas de Gestión Empresarial, pero es un requisito para poder hacerlos.

---

## Paso 1 — Crear la máquina virtual

1. Abre tu hipervisor (VirtualBox, VMware, Hyper-V o el que uséis en el aula).
2. Crea una nueva máquina virtual:
   - Tipo: Linux · Versión: Ubuntu (64-bit).
   - RAM: mínimo 2 GB (recomendado 4 GB si el equipo lo permite).
   - Disco: mínimo 20 GB.
   - Red: modo **adaptador puente**
3. Monta la imagen ISO de **Ubuntu Server 26.04.1 LTS**.

---

## Paso 2 — Instalar Ubuntu Server

Sigue el asistente de instalación:

1. Idioma y distribución de teclado.
2. Configuración de red: comprueba que la máquina obtiene una IP (por DHCP por el momento).
3. Particionado de disco: usa la opción guiada por defecto (todo el disco), no hace falta particionado manual para este ejercicio.
4. Configura el nombre dle equipo como serverXXX
5. Crea tu usuario y contraseña — PCXXX - Dav@nte
6. **Importante:** en la pantalla de selección de software (*Featured Server Snaps*), marca la opción **OpenSSH server** si aparece disponible. Si no aparece o tienes dudas, no pasa nada, lo instalamos a mano en el paso siguiente.
7. Completa la instalación, reinicia y retira el ISO cuando te lo pida.

---

## Paso 3 — Actualizar el sistema

Ya dentro de Ubuntu Server (login por consola con el usuario creado):

```bash
sudo apt update
sudo apt upgrade -y
```

---

## Paso 4 — Instalar y comprobar OpenSSH

Si no lo marcaste durante la instalación:

```bash
sudo apt install openssh-server -y
```

Comprueba que el servicio está activo:

```bash
sudo systemctl status ssh
```

Deberías ver `active (running)` en verde. Si no lo está:

```bash
sudo systemctl enable --now ssh
```

---

## Paso 5 — Averiguar la IP de la máquina

```bash
ip a
```

Busca la IP asociada a tu interfaz de red (normalmente algo como `192.168.x.x` o `10.0.x.x`). Apúntala.

---

## Paso 6 — Conectar por SSH

Desde tu máquina anfitriona (host) o desde otro equipo de la misma red, abre una terminal y conecta:

```bash
ssh tu_usuario@ip_de_tu_maquina
```

La primera vez te pedirá confirmar la huella (*fingerprint*) del servidor — escribe `yes`. Después, introduce tu contraseña.

**Si la conexión funciona correctamente**, verás el *prompt* de tu máquina Ubuntu Server dentro de la terminal desde la que te has conectado.

---

## Entrega

Haz una captura de pantalla donde se vea, a la vez:

- El comando `ssh usuario@ip` que has ejecutado.
- El *prompt* resultante ya dentro del servidor (por ejemplo, ejecuta `hostname` y `whoami` justo después de conectar para que se note claramente que estás dentro).

Enséñasela al profesor en clase para su revisión, o súbela donde se indique en el aula virtual.

---

## Checklist de autocomprobación

- [ ] La VM arranca y tiene Ubuntu Server 26.04.1 LTS instalado.
- [ ] `sudo apt update && sudo apt upgrade` se ejecuta sin errores.
- [ ] `systemctl status ssh` muestra el servicio activo.
- [ ] Conozco la IP de mi máquina (`ip a`).
- [ ] Puedo conectarme por SSH desde otro equipo/mi host y llegar al *prompt* del servidor.
- [ ] Tengo apuntados usuario, contraseña e IP para la próxima sesión en VirtualBox.

> 💡 **De cara al Bloque 2:** esta misma máquina será la que usemos para instalar el ERP-CRM en modo monopuesto o cliente-servidor, así que consérvala — no la borres ni la reinstales sin avisar.

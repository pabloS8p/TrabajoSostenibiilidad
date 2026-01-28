# Sockets & Dragons

Repositorio de prácticas de **PSP (Programación de Servicios y Procesos)**.

## Integrantes del grupo

- Pablo
- Miguel Ángel Varo
- Manuel Cañas

---

## Requisitos

- **Java 17+** (o la versión que uses en clase)
- Ejecutar en local (host: `localhost`)

---

## Estructura del repositorio

- [`Socket_Dragons_TCP_VPM/`](./Socket_Dragons_TCP_VPM) → Mensajes UTF (`DataInputStream/DataOutputStream`)
- [`Socket_Dragons_Oraculo_VPM/`](./Socket_Dragons_Oraculo_VPM) → Objetos (`ObjectInputStream/ObjectOutputStream`)

---

## Contexto

En esta entrega trabajamos con **sockets TCP en Java**.

Hay dos mini-proyectos independientes:

1) **Socket_Dragons_TCP_VPM** → comunicación por `DataInputStream/DataOutputStream` usando `readUTF()` / `writeUTF()`.
2) **Socket_Dragons_Oraculo_VPM** → comunicación por `ObjectInputStream/ObjectOutputStream` enviando un objeto `Numeros` (Serializable).

Cada proyecto incluye:
- **Servidor**
- **Clientes** (para probar cola/turno y respuestas)

---

## 1) Socket_Dragons_TCP_VPM

Carpeta: [`Socket_Dragons_TCP_VPM/`](./Socket_Dragons_TCP_VPM)

### Objetivo

- Practicar una comunicación TCP sencilla.
- El servidor recibe un mensaje (UTF) y lo devuelve en **MAYÚSCULAS**.
- El servidor controla:
  - **Turnos** (solo atiende a 1 cliente a la vez)
  - **Cola con timeout**
  - **Timeout por inactividad (AFK)**
  - Validación básica para no aceptar mensajes vacíos o demasiado largos

### Estructura (carpeta `Socket_Dragons_TCP_VPM/src`)

- `SocketServer.java` → servidor con cola/turnos.
- `SocketCliente.java` → cliente por consola.
- `SocketCliente2.java` → segundo cliente.
- `SocketClienteDemoQA.java` → demo segura (pocos clientes) para ver cola/turnos.
- `SocketClienteQA_CargaControlada.java` → prueba con carga controlada (usar con cabeza).

### Cómo ejecutar (desde terminal)

> Si usas IntelliJ/Eclipse, también puedes ejecutar con el botón Run.

Desde la raíz del repo:

1) Compilar:
- Windows (PowerShell / CMD):
  - `cd Socket_Dragons_TCP_VPM\src`
  - `javac *.java`

2) Ejecutar servidor:
- `java SocketServer`

3) Ejecutar cliente(s) en otra terminal:
- `java SocketCliente`
- `java SocketCliente2`
- (Opcional) `java SocketClienteDemoQA`

**Puerto por defecto:** `6000`.

---

## 2) Socket_Dragons_Oraculo_VPM

Carpeta: [`Socket_Dragons_Oraculo_VPM/`](./Socket_Dragons_Oraculo_VPM)

### Objetivo

- Practicar envío de objetos por sockets usando **serialización**.
- El cliente envía un objeto `Numeros` con un entero.
- El servidor calcula:
  - `cuadrado = n * n`
  - `cubo = n * n * n`
- Devuelve el mismo objeto con los resultados.
- El servidor usa **turnos** y **timeouts** para no quedarse bloqueado.

### Estructura (carpeta `Socket_Dragons_Oraculo_VPM/src`)

- `Numeros.java` → clase `Serializable` que viaja por la red.
- `SocketServer.java` → servidor "Oráculo".
- `SocketCliente.java` → cliente 1 por consola.
- `SocketCliente2.java` → cliente 2 por consola.

### Cómo ejecutar (desde terminal)

Desde la raíz del repo:

1) Compilar:
- Windows (PowerShell / CMD):
  - `cd Socket_Dragons_Oraculo_VPM\src`
  - `javac *.java`

2) Ejecutar servidor:
- `java SocketServer`

3) Ejecutar cliente(s) en otra terminal:
- `java SocketCliente`
- `java SocketCliente2`

**Puerto por defecto:** `6000`.

---

## Notas / problemas típicos

- Si el puerto `6000` está ocupado, cierra el proceso que lo use o cambia el puerto en servidor y clientes.
- En el proyecto de objetos, se crea primero `ObjectOutputStream` y luego `ObjectInputStream` para evitar bloqueos.
- Los timeouts están puestos para que en clase se vea bien la cola/turno y la expulsión por inactividad.

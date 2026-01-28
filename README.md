# Sockets & Dragons

Repositorio de prácticas de **PSP (Programación de Servicios y Procesos)**.

## Integrantes del grupo

- Pablo
- Miguel Ángel Varo
- Manuel Cañas

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

### Evidencias (capturas)

Pegado de imágenes (ejemplo):
- `![Servidor TCP funcionando](./imagenes/imagen.png)`

> Sugerencia: crea una carpeta `imagenes/` en la raíz del repo para guardar las capturas.

### Clientes de debug / QA (para qué sirven)

En este proyecto hay clientes "extra" pensados para **demostrar** y **comprobar** que la cola y los timeouts funcionan.

- `SocketClienteDemoQA.java`
  - Para qué sirve: demo rápida en clase.
  - Qué hace:
    - Lanza pocos clientes (por defecto) casi a la vez.
    - Te enseña en consola quién entra en cola y quién recibe el turno.
    - Puede simular 1 cliente "AFK" (no envía mensaje cuando le toca) para ver la expulsión.
  - Cuándo usarlo: cuando quieras una prueba visual, fácil y no pesada.

- `SocketClienteQA_CargaControlada.java`
  - Para qué sirve: prueba más larga pero controlada.
  - Qué hace:
    - Lanza muchos intentos de cliente (configurable) con un paralelismo limitado.
    - Cada cliente espera su turno, envía un mensaje y comprueba que vuelve en mayúsculas.
    - Saca por consola si fue OK/FAIL.
  - Cuándo usarlo: cuando quieras comprobar estabilidad durante más tiempo.
  - Importante: si subes demasiado el número de clientes, ya no es una demo, sería un estrés (úsalo con cabeza).

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

### Evidencias (capturas)

Añadir aquí capturas para demostrar que funciona.

Ejemplos de capturas recomendadas:
- Servidor "Oráculo" arrancado.
- Cliente enviando un número.
- Respuesta con cuadrado y cubo.
- Dos clientes: uno en cola y otro atendido.

Pegado de imágenes (ejemplo):
- `![Oráculo funcionando](./imagenes/oraculo_respuesta.png)`

### Clientes de debug / QA (para qué sirven)

En este proyecto no hay un cliente de carga especial como en el TCP.

Los clientes que hay (`SocketCliente` y `SocketCliente2`) sirven para:
- Probar el servidor con 1 cliente.
- Probar la cola/turno con 2 clientes a la vez.

Si quieres, se puede añadir un `SocketClienteDemoQA_Oraculo` parecido al del TCP (pero con objetos) para demo en clase.

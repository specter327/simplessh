# Previsualización del producto

## Visión

SimpleSSH es un sistema pequeño y directo para acceder a **terminales interactivas de múltiples dispositivos remotos** desde una interfaz WebGUI.

El servidor se despliega en un VPS GNU/Linux y centraliza la administración de las conexiones. El usuario accede desde un navegador, selecciona un dispositivo conectado y utiliza su terminal.

El objetivo no es construir una plataforma genérica de administración remota: el resultado que debe entregar el producto es una terminal interactiva, sencilla y fiable.

## Funcionamiento esperado

1. Contratar o disponer de un VPS GNU/Linux.
2. Desplegar SimpleSSH en el servidor.
3. Configurar el acceso administrativo y el direccionamiento.
4. Instalar o ejecutar el agente correspondiente en cada dispositivo autorizado.
5. Asignar al dispositivo un puerto de conexión mediante la API HTTP.
6. Abrir la WebGUI desde un navegador.
7. Seleccionar el dispositivo y utilizar su terminal interactiva.

## Componentes y tecnologías

<<<<<<< HEAD
> Quizas con BuildKit, o PyInstaller

Con un agente capaz de desplegarse, instalarse, y persistir con unos clics. Automatico, simple y fiable.
Capaz de asegurar persistencia, resiliencia de conexion, y ejecucion.
=======
- **Servidor:** Python 3 sobre GNU/Linux.
- **API administrativa:** FastAPI sobre HTTP/HTTPS. Se utiliza para la configuración y asignación de puertos, así como para las operaciones administrativas necesarias.
- **Comunicación operativa:** OpenSSH.
- **Reconexión:** AutoSSH para mantener o recuperar la conexión SSH.
- **Interfaz:** WebGUI compatible con navegadores de escritorio y móviles.
- **Agentes:** implementaciones específicas para Windows, GNU/Linux y Termux, según las necesidades de cada plataforma.
>>>>>>> 7be2d23dc7936eab05a657a64a0f113ef57ea346

La multiplexación se realizará mediante asignación de puertos. La API HTTP permitirá configurar y asignar esos puertos sin tener que modificar manualmente la configuración del servidor.

## Decisiones de implementación

No se reinventará SSH. SimpleSSH utilizará OpenSSH para el transporte y las sesiones remotas, y AutoSSH cuando se necesite recuperación automática de conexiones.

No se impondrá una abstracción multiplataforma. Si las diferencias entre sistemas operativos hacen más simple, fiable o mantenible disponer de agentes separados, se desarrollarán agentes especializados para Windows, GNU/Linux y Termux.

Tampoco se crearán capas, mecanismos de extensibilidad o abstracciones preventivas. Se elegirá la solución más sencilla que permita completar y consolidar el producto.

## Requisitos de operación y seguridad

- Comunicación cifrada mediante SSH y HTTPS.
- Autenticación y autorización para el acceso administrativo y los dispositivos.
- Asignación de puertos controlada por el servidor.
- Conexiones identificables y revocables.
- Instalación y persistencia mediante mecanismos normales y visibles de cada plataforma, con posibilidad de detener y desinstalar el agente.
- La interfaz pública no debe exponer la administración del sistema operativo anfitrión ni permitir accesos no autorizados.

## Resultado esperado

Un sistema que pueda desplegarse en un VPS, configurar desde una API HTTP y utilizarse desde un navegador para abrir terminales interactivas de los dispositivos autorizados.
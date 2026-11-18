# Propuesta de SimpleSSH

## 1. Propósito

SimpleSSH será una solución de acceso remoto cuyo objetivo funcional es ofrecer **terminales interactivas para dispositivos autorizados**, administradas desde un servidor central y consumidas mediante una interfaz WebGUI.

El producto debe ser simple de desplegar, configurar y utilizar. Su éxito se medirá por entregar una experiencia de terminal remota estable, no por ofrecer una arquitectura genérica o extensible.

## 2. Experiencia de uso

El flujo principal será:

1. Desplegar el servidor SimpleSSH en un VPS GNU/Linux.
2. Configurar el acceso administrativo y el direccionamiento.
3. Instalar o ejecutar un agente en cada dispositivo que se quiera administrar.
4. Registrar el dispositivo y asignarle un puerto de conexión mediante la API administrativa HTTP.
5. Abrir la WebGUI desde un navegador.
6. Seleccionar un dispositivo conectado.
7. Utilizar su terminal interactiva.

La operación cotidiana debe reducirse a seleccionar un dispositivo y trabajar en su terminal.

## 3. Arquitectura funcional mínima

### Servidor

Proceso central ejecutado en GNU/Linux, preferentemente en un VPS. Sus responsabilidades se limitan a:
- Mantener la configuración de los dispositivos registrados.
- Exponer la API administrativa HTTP.
- Asignar y administrar los puertos de conexión.
- Coordinar el acceso a las sesiones SSH.
- Servir la WebGUI.

### API administrativa

Se implementará con **FastAPI**. Será una API HTTP para las operaciones de administración y configuración, especialmente el registro de dispositivos y la asignación de puertos.

La API administrativa no sustituye el canal SSH utilizado para la terminal interactiva.

### Comunicación operativa

Se utilizará **OpenSSH** para establecer las conexiones SSH y proporcionar las terminales interactivas.

Se utilizará **AutoSSH** para supervisar y recuperar conexiones cuando sea necesario. No se implementará un protocolo SSH propio ni se reescribirá funcionalidad que ya proporcionan estas herramientas.

### Agentes

Se contemplan agentes para:
- Windows.
- GNU/Linux.
- Termux (Android).

No se requiere que todos compartan una implementación interna. Cuando las diferencias de plataforma lo justifiquen, cada agente tendrá una implementación especializada que utilice los mecanismos nativos y las herramientas disponibles en su entorno.

### WebGUI

Interfaz web accesible desde navegadores de escritorio y móviles. Su función principal será:
- Mostrar los dispositivos y su estado de conexión.
- Permitir seleccionar un dispositivo.
- Abrir y utilizar su terminal interactiva.

## 4. Multiplexación y asignación de puertos

La identificación y el encaminamiento de las conexiones operativas se resolverán mediante multiplexación por puerto.

La asignación de puertos será configurable desde la API HTTP de FastAPI. El servidor mantendrá la relación entre el dispositivo autorizado y el puerto que tiene asignado.

La asignación deberá validar que el puerto esté disponible y evitar conflictos entre dispositivos. La configuración efectiva deberá poder consultarse y modificarse mediante las operaciones administrativas autorizadas.

## 5. Decisiones tecnológicas

| Necesidad | Decisión |
|---|---|
| Servidor | Python 3 en GNU/Linux |
| API administrativa | FastAPI |
| Transporte y terminal remota | OpenSSH |
| Recuperación de conexión | AutoSSH |
| Interfaz | WebGUI |
| Agentes | Específicos por plataforma cuando convenga |

Las herramientas existentes se reutilizarán siempre que resuelvan correctamente la necesidad. El desarrollo propio se concentrará en la integración, configuración, administración de dispositivos y experiencia de uso.

## 6. Filosofía de desarrollo

SimpleSSH no pretende ser un framework, una biblioteca de transporte ni una plataforma extensible.

Por tanto:
- No se crearán capas de abstracción sin una necesidad demostrable.
- No se diseñarán puntos de extensión preventivos.
- No se impondrá una arquitectura multiplataforma común.
- No se desarrollará una implementación propia de SSH.
- No se añadirán subsistemas que no contribuyan directamente al producto funcional.

Se preferirán componentes concretos, integración directa y una estructura de código fácil de comprender y mantener.

La prioridad será completar un producto usable y consolidado. Cualquier complejidad adicional deberá justificarse por un requisito real de funcionamiento, seguridad o mantenimiento.

## 7. Seguridad y control

El acceso remoto estará limitado a dispositivos y usuarios autorizados.

Requisitos mínimos:
- SSH para proteger las sesiones operativas.
- HTTPS para proteger la API administrativa cuando se exponga por red.
- Autenticación y autorización de las operaciones administrativas.
- Identidad y credenciales individuales para los dispositivos, con posibilidad de revocación.
- Asignación de puertos validada y controlada por el servidor.
- Registro de operaciones administrativas relevantes.
- Instalación y persistencia transparentes, utilizando mecanismos normales de cada sistema operativo y permitiendo detener y desinstalar el agente.

La API administrativa no debe proporcionar acceso indiscriminado al VPS ni exponer credenciales privadas de SSH.

## 8. Alcance inicial del producto

El primer producto utilizable debe cubrir:

1. Despliegue del servidor GNU/Linux.
2. API FastAPI operativa.
3. Registro de un dispositivo y asignación de puerto.
4. Conexión SSH mediante OpenSSH.
5. Recuperación de conexión mediante AutoSSH.
6. Visualización del estado del dispositivo.
7. Terminal interactiva desde la WebGUI.
8. Pruebas de conexión, desconexión, reconexión y concurrencia básica.

Se priorizará una primera plataforma de agente para cerrar el flujo completo. Las demás se incorporarán mediante implementaciones específicas, sin retrasar el producto por intentar resolver anticipadamente todas las diferencias entre plataformas.

## 9. Criterio de finalización

SimpleSSH podrá considerarse un producto inicial consolidado cuando sea posible desplegarlo en un VPS, registrar un dispositivo autorizado, asignarle un puerto desde la API, mantener o recuperar su conexión y utilizar su terminal interactiva desde un navegador de forma segura y fiable.

La expansión de plataformas y mejoras posteriores no debe impedir alcanzar primero este flujo funcional completo.
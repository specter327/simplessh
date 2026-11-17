# Previsualizacion objetivo

Imaginamos al sistema como:

Un sistema capaz de desplegarse en un VPS de forma simple y automatica. En unos clics/comandos.
Compatible con el sistema operativo GNU/Linux Ubuntu, y Python3.

Capaz de configurarse para su uso, acceso y consumo publico y remoto.
Para poder utilizarlo desde mi celular, y mi computador, mediante un navegador. Con alta compatibilidad.

Configurable para utilizar direccionamiento con direccion IPv4/IPv6 publica y/o nombre DNS vinculado.

Capaz de configurarse para tener control de acceso mediante un solo perfil, bajo contraseña. Permitiendo la actualizacion de la contraseña unicamente desde la interfaz CLI (nunca expuesta a Internet) del sistema - solo accesible desde el VPS -
Para permitir un uso personal o compartido. Exigiendo contraseñas largas.

Comunicacion segura con HTTPS para su API administrativa y SSH para su comunicacion operativa. Para proteger ante intercepcion de comunicacion.

Capaz de simplemente fabricar una copia del agente de control remoto con unos clics, para los sistemas operativos soportados, auto-configurandose para conectarse al servidor. Con agentes fabricados en paquetes distribuibles como: ".exe", ".AppImage", ".py"

> Quizas con BuildKit, o PyInstaller

Con un agente capaz de desplegarse, instalarse, y persistir con unos clics. Automatico, simple y fiable.
Capaz de asegurar persistencia, resiliencia de conexion, y ejecucion.

> Al estilo: ejecuta, y olvida (desatendido).

Con una interfaz WebGUI y un selector para visualizar clientes conectados, y utilizar su terminal.

Para que su uso sea:
- Contratar un VPS
- Desplegar al servidor
- Configurar al servidor (autenticacion, direccionamiento, etc.)
- Fabricar un cliente
- Desplegar (ejecutar) el cliente
- Administrar al cliente (o los) conectado(s)

Robusto, simple, fiable, seguro.

El servidor puede desarrollarse y ejecutarse con Python3 interpretado, y el cliente puede desarrollarse en C++, o Python.
Podriamos utilizar por simplicidad un software cliente como OpenSSH o AutoSSH, para facilitar y reutilizar recursos (empaquetandolo con el software distribuido), o reimplementar el funcionamiento si resulta conveniente o necesario.
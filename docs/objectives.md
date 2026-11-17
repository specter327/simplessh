# Objetivos

## Objetivo funcional

El objetivo funcional de SimpleSSH es ofrecer **terminales interactivas remotas** para administrar dispositivos autorizados desde una interfaz centralizada.

El usuario debe poder:
- Desplegar el servidor en un VPS GNU/Linux.
- Registrar y administrar dispositivos remotos.
- Asignar a cada dispositivo un puerto de conexión mediante una API administrativa HTTP.
- Consultar qué dispositivos están conectados.
- Abrir y utilizar una terminal interactiva del dispositivo seleccionado desde la WebGUI.

## Alcance

- **Servidor:** ejecución en GNU/Linux, orientada a un VPS.
- **Administración:** API HTTP implementada con FastAPI para configurar y asignar puertos, y gestionar los dispositivos.
- **Comunicación operativa:** SSH mediante OpenSSH.
- **Persistencia de conexión:** AutoSSH para mantener o recuperar conexiones cuando corresponda.
- **Agentes:** agentes específicos para Windows, GNU/Linux y Termux cuando las diferencias de cada plataforma lo justifiquen.
- **Interfaz:** WebGUI accesible desde un navegador para seleccionar dispositivos y utilizar sus terminales.
- **Seguridad:** autenticación, autorización y comunicación cifrada. El acceso se limita a dispositivos y usuarios autorizados.

## Criterios de diseño

- Reutilizar OpenSSH y AutoSSH; no implementar un protocolo SSH propio.
- Mantener una solución directa, pequeña y enfocada en entregar un producto utilizable.
- Elegir implementaciones específicas por plataforma cuando sea más sencillo y fiable que forzar una implementación común.
- Priorizar la integración funcional, la estabilidad y la facilidad de despliegue.

## Fuera de alcance

No se busca construir un framework ni una plataforma genérica. No son objetivos del proyecto:
- Crear capas de abstracción, arquitecturas extensibles o sistemas de plugins sin una necesidad funcional concreta.
- Diseñar un protocolo de transporte propio o reinventar SSH.
- Unificar artificialmente las particularidades de Windows, GNU/Linux y Termux.
- Añadir funciones de administración remota que no sean necesarias para ofrecer terminales interactivas.

## Plataformas previstas

| Componente | Plataforma |
|---|---|
| Servidor | GNU/Linux |
| Agente | Windows |
| Agente | GNU/Linux |
| Agente | Termux (Android) |

La compatibilidad de cada agente se resolverá de forma específica para su plataforma.
# configuracion-central
Servicio que administra y centraliza las configuraciones de app y ambientes alimentandose de un repositorio remoto

# Configuración Centralizada de Propiedades con Spring Cloud y Git

Este proyecto utiliza Spring Cloud Config Server para implementar la configuración centralizada de propiedades desde un repositorio Git remoto.

## Archivo `application.properties`

```properties
spring.cloud.config.server.git.uri=https://github.com/uraken-5/server-config
spring.cloud.config.server.git.clone-on-start=true
spring.cloud.config.server.git.default-label=main
server.port=8888
logging.level.web=DEBUG


```Descripción de Propiedades:
spring.cloud.config.server.git.uri: Especifica la URL del repositorio Git remoto que contiene la configuración. En este caso, apunta al repositorio https://github.com/uraken-5/server-config.

spring.cloud.config.server.git.clone-on-start: Indica si el servidor de configuración debe clonar automáticamente el repositorio Git al iniciar. Está establecido como true, lo que significa que el repositorio se clonará al inicio del servidor.

spring.cloud.config.server.git.default-label: Establece la rama predeterminada (label) que se utilizará para obtener la configuración. En este caso, se usa la rama main.

server.port: Especifica el puerto en el que se ejecutará el servidor de configuración. Se ha configurado como 8888.

logging.level.web: Define el nivel de registro (logging) para las solicitudes web. En este caso, se ha establecido en DEBUG.
